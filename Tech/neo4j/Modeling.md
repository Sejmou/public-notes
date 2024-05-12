## Nodes
- the dominant **nouns**/entities in the application - stored in node **labels** (e.g. Person, Movie)
- **properties** are used to
	- uniquely identify a node
	- answer specific use case questions or
	- return data (`RETURN m.title`)
- notation:
	- `CamelCase` for nodes
	- `camelCase` for properties

### Relationships
- used for modeling **verbs** of the use cases
- can be directed or undirected (always directed in DB, but queries can be adapted to ignore direction)
	- undirected example: `MARRIED`
	- directed example: `FOLLOWS` (on social networks like Twitter)
- 'subject' and 'object' usually different nodes, but can also be same node (e.g. someone `LIKES` their own social media post)
- fanout: creating very dense nodes with lots of incoming or outgoing edges
	- usually not a good idea
	- can be useful to answer specific questions (e.g. who lives in the same city as ...)
- **properties** detail *how* nodes are related (e.g. `roles` of a person that `ACTED_IN` a movie, the exact `date` on which two `Person`s married)
- notation:
	- `ALL_CAPS` for type (i.e. name/verb)
	- `camelCase` for properties

## Scalability considerations
- goal: reduce size of the graph that is touched by a query
- tip: use `PROFILE` to view query plan
- adding properties vs. labels
	- labels always create an index (hence, all nodes without a particular label are skipped)
	- example: labels for each country (`US`, `UK`, etc.) vs. `country` with multiple possible values, including `US`: choice depends on how important country-related queries are
- [interesting discussion of tradeoffs](https://community.neo4j.com/t/heavy-relationships-vs-node-hops-which-is-better/4466/2)
- after rewrites/refactors, use case-related queries may need to be adapted to make use of them (or still be executable!)
- don't use labels for hierarchical relationships (inheritance)!
- make sure labels for each node are semantically orthogonal (i.e. they should not have anything to do with each other)