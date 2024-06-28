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

### special features/functions
`asssumeNotNull`: define as non-nullable
`anyHeavy`: pick 'most common' (approximately!) value
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