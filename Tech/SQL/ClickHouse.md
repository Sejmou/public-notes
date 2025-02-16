## Client

### allow execution of multiple SQL statements at once
run `clickhouse client` with `-n`

### Custom config
will be used whenever `clickhouse client` is run

create/edit `.clickhouse-client/config.xml`:
```xml
<config>
	<user>asdf</user>
	<password>whatever</password>
	<host>some IP</host>
	<port>the port</port>
	<input_format_allow_errors_num>0</input_format_allow_errors_num>
	<input_format_skip_unknown_fields>1</input_format_skip_unknown_fields>
	<input_format_import_nested_json>1</input_format_import_nested_json>
</config>
```

## Query Syntax
### schema hints (for dynamic data like files stored in S3)
Add `SETTINGS schema_inference_hints='some_column DataType1, other_column DataType2'` (using actual column name(s) and [accepted datatypes](https://clickhouse.com/docs/en/sql-reference/data-types) instead)

## get NULL count for each column (dynamically!)
```sql
FROM db.table -- also works with s3(...), file(...) etc.!
SELECT COLUMNS('.*')
APPLY(col -> countIf(col IS NULL))
FORMAT Vertical;
```

### write to local CSV
```SQL
SELECT *  
FROM sometable  
INTO OUTFILE 'out.csv'  
FORMAT CSVWithNames
```

### format query results (alternatives to rendering table boxes on command line)
add `FORMAT FormatName` (replace `FormatName` with actual format name from [here](https://clickhouse.com/docs/en/interfaces/formats))

### get columns of ClickHouse table (doesn't work w/ S3 files)
```sql
SELECT name
FROM system.columns
WHERE table = 'table_name' AND database = 'db_name'
```

### get overview of auto-detected column types for S3 file
```sql
DESCRIBE TABLE
  s3(
    'https://s3.region-name.wasabisys.com/path-to-file.csv.gz',
    -- if required 
    -- 'access_key',
    -- 'secret',
    'CSVWithNames'
    -- replace above with JSONEachLine for JSON lines, CSV for CSV w/o headers
    );
```

### Get data from query logs
```sql
-- Gets log data for all insert queries involving two particular tables
SELECT event_time, query_id, query, tables
FROM system.query_log
WHERE type = 'QueryFinish' 
  AND query LIKE 'INSERT INTO%' 
  AND has(tables, 'db_a.table_x')
  AND has(tables, 'db_b.table_b')
-- vertical format makes it easier to read queries
FORMAT Vertical;
```

### fill missing values
[docs](https://clickhouse.com/docs/en/sql-reference/statements/select/order-by#order-by-expr-with-fill-modifier)

```sql
WITH example_data AS (
  SELECT toFloat32(number % 10) AS n, 'original' AS source  
  FROM numbers(10) WHERE number % 3 = 1  
)
SELECT n, source FROM example_data
-- FROM, TO and STEP are optional; STEP defaults to 1 for numeric data
ORDER BY n WITH FILL FROM 0 TO 5.51 STEP 0.5;
```

it also works with dates :)
```sql
SELECT
    toDate(number * 86400) AS d1,
    'original' AS source
FROM numbers(10)
WHERE (number % 3) = 1
ORDER BY
    d1 WITH FILL;
```

### Materialized views
#### Check for update status in refreshable materialized view
```sql
SELECT * FROM system.view_refreshes WHERE database = 'db' AND view = 'name_of_the_mv';
```

### Date Ranges

At the moment, ClickHouse has no built-in functions for creating date ranges (see also [discussion](https://github.com/ClickHouse/ClickHouse/issues/47041) on GitHub). So we have to create them manually.
#### First day of every month in date range (incl. start and end)


#### Daily date range (incl. start and end)
```sql
SET param_start = '2023-01-01';
SET param_end = '2023-12-04';
/*
 We add 24 hours to every date in the range and then jump to the start of that date.
 86400 is the number of seconds in a day.
 86400 = 24 * 60 * 60
 */
WITH toUnixTimestamp(
  toDateTime(
    toStartOfInterval(
      toDateTime({ start :String }),
      interval 1 day
    )
  )
) AS start,
toUnixTimestamp(
  toDateTime(
    toStartOfInterval(toDateTime({end :String }),
    interval 1 day
  )
)
) AS
end,
relevant_days AS (
  SELECT
    arrayJoin(
      arrayMap(
        x -> (
          toDate(
            toStartOfInterval(toDateTime(x), interval 1 day)
          )
        ),
        range(toUInt64(start), toUInt64(end) + 86400,
        86400
      )
    )
) AS day
)
SELECT
  *
FROM
  relevant_days;
```

#### Consecutive dates from some reference date
This example query creates a dates for `2024-07-07` and the 6 days before it, in ascending order:
```sql
WITH
toDate('2024-07-07') AS reference_date,
days AS (
    SELECT arrayJoin(
      reverse(
        arrayMap(x -> addDays(reference_date, -x), range(7))
        )
    ) AS date
)
SELECT *
FROM days
```
### special features/functions
`asssumeNotNull`: define as non-nullable
`anyHeavy`: pick 'most common' (approximately!) value

## Adding row numbers for result set
For this, we can use `rowNumberInAllBlocks()`

Example query:
```sql
SELECT priority, min(rowNumberInAllBlocks()) AS row_num FROM (SELECT * FROM to_fetch ORDER BY priority, popularity) GROUP BY priority;
/*
example output:
┌─priority─┬─row_num─┐
│        1 │       0 │
│        2 │   20517 │
└──────────┴─────────┘
*/
```

See also [this](https://github.com/ClickHouse/ClickHouse/issues/3353) discussion
## Reset Schema Inference Cache
For files, including files on S3, ClickHouse caches the inferred schemas. This means that sometimes we get back incomplete stuff from `DESCRIBE TABLE s3(...)` statements as the cache has stored an outdated schema.

To make inference run again, there's apparently no other solution than deleting the whole cache, which can be done by running
```sql
SYSTEM DROP SCHEMA CACHE FOR S3;
```
## Readable `DESCRIBE TABLE` (also works nicely for S3 files w/ deep nesting!)
```sql
DESCRIBE TABLE s3('...')
SETTINGS
  -- skips irrelevant columns (i.e. NOT colname/datatype)
  describe_compact_output = 1,
  -- uncomment if you're not that interested in nested columns
  -- adds another column 'is_subcolumn'; those with value 1 are actual subcolumns
  -- nullable columns are also printed as subcolumns (regular value and null)
  describe_include_subcolumns = 1
FORMAT TabSeparated;
```
## Create new DB user w/ sufficient permissions for regular ETL-tasks
```sql
CREATE USER username IDENTIFIED BY 'password';

GRANT
  SELECT,
  INSERT,
  -- clickhouse client shows error on connection to DB without this - not sure why it is needed exactly lol
  addressToLineWithInlines
  -- certain types of queries require this permission, don't remember exactly which ones
  CREATE TEMPORARY TABLE,
  -- needed for interacting with files in S3 storage
  S3
ON *.* TO username;
```

### S3Queue engine tables
#### Check recent imports
```sql
SELECT
  file_path,
  file_name,
  processing_start_time,
  processing_end_time
FROM system.s3queue ORDER BY processing_start_time DESC LIMIT 10;
```
#### Check recent imports for specific S3 paths
```sql
SELECT
  file_path,
  file_name,
  processing_start_time,
  processing_end_time
FROM system.s3queue
WHERE
  file_path LIKE '%s3_path_part%' AND
  -- to filter out irrelevant older attempts, optionally use this
  processing_start_time > 'YYYY-MM-DD hh:mm:ss'
ORDER BY processing_start_time DESC;
```
#### Get details for several imports
```sql
SELECT
  database,
  table,
  file_name,
  processing_start_time,
  processing_end_time,
  status, 
  exception
FROM system.s3queue_log
ORDER BY processing_start_time DESC
LIMIT 10;
```

#### Get details for imports for specific table
```sql
SELECT
  file_name,
  processing_start_time,
  processing_end_time,
  status, 
  exception
FROM system.s3queue_log
WHERE database = 'db'
AND table = 'table'
ORDER BY processing_start_time DESC;
```

#### Get import errors for specific table
```sql
SELECT
  file_name,
  processing_start_time,
  processing_end_time,
  status,
  -- limit exception length, otherwise things become totally unreadable
  substring(exception, 1, 255) AS exception
FROM system.s3queue_log
WHERE database = 'db'
AND table LIKE 'table'
AND length(exception) > 0
-- add this to prevent printing logs for previous attempts before logic was changed, substituting the timestamp components accordingly to reflect the time where you made the change
-- AND processing_start_time > 'YYYY-MM-DD hh:mm:ss'
ORDER BY processing_start_time DESC;
```
#### Get details for specific import (useful in case of exception)
```sql
SELECT
  database,
  table,
  file_name,
  processing_start_time,
  processing_end_time,
  status,
  -- limit exception length, otherwise things become quite unreadable
  substring(exception, 1, 255) AS exception
  -- uncomment this instead if more context is needed
  -- exception
FROM system.s3queue_log
WHERE database = 'db'
AND table LIKE 'table'
ORDER BY processing_start_time DESC
LIMIT 1
FORMAT Vertical;
```
## Server
### Run from Docker image 
with custom config, exposing all network ports (better performance than exposing selected ports with `-p`), AND persisting data

To start:
```bash
docker run -d \
  --network=host
  --name my-clickhouse-server \
  --ulimit nofile=262144:262144 \
  -v ./server-config.xml:/etc/clickhouse-server/config.xml clickhouse/clickhouse-server \
  -v $(realpath ./ch_data):/var/lib/clickhouse/ \
  -v $(realpath ./ch_logs):/var/log/clickhouse-server/ \
```

To stop:
```bash
docker stop my-clickhouse-server
docker rm my-clickhouse-server # not sure if safe to do without deleting data
```

additional info:
- `/var/lib/clickhouse/` - main folder where ClickHouse stores the data
- `/var/log/clickhouse-server/` - logs

see also [DockerHub](https://hub.docker.com/r/clickhouse/clickhouse-server/)

### S3 bucket/endpoint credentials config
Add the following to `/etc/clickhouse-server/config.xml`:
```xml
<clickhouse>
    <s3>
        <endpoint-name>
            <endpoint>https://s3.region-name.com/bucket-name/</endpoint>
            <access_key_id>id</access_key_id>
            <secret_access_key>secret</secret_access_key>
            <!-- <use_environment_credentials>false</use_environment_credentials> -->
            <!-- <header>Authorization: Bearer SOME-TOKEN</header> -->
        </endpoint-name>
		<!-- same tags/structure for any other endpoints/buckets -->
   </s3>
   ...
```

Adding a `s3.xml` in `/etc/clickhouse-server/config.d` with just the `<s3>` tag wrapped by `<clickhouse>` should also work (didn't work for me for some reason)

See also [ClickHouse S3 Credential Storage Docs](https://clickhouse.com/docs/en/integrations/s3#managing-credentials)