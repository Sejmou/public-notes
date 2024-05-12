## `UNWIND`
transform list to separate records
## `collect()`
collect records into a list
## [`WITH`](https://neo4j.com/docs/cypher-manual/current/clauses/with/)
it's a bit more complicated lol

## Example query
```cypher
MATCH (m:Movie)
UNWIND m.languages AS language // list of strings
WITH language, collect(m) AS movies // tuples of (language, movie)
MERGE (l:Language {name:language}) // create node for each language
WITH l, movies // records: tuples of language node and associated movie node list
UNWIND movies AS m 
WITH l,m // records: tuples of language and movie nodes
MERGE (m)-[:IN_LANGUAGE]->(l); // create relationship between each movie and lang

MATCH (m:Movie)
SET m.languages = null // remove redundant movie language prop
```

