moderator, mediator, and confounder variables are relevant in causal inference. This includes any analysis that tries to answer the question whether some independent variable X influences an independent variable Y. 

## Confounder
A confounder variable C affects **both** X and Y. So any change in Y that we observe may be wrongly attributed to the change in X. This is an example for a 'spurious relationship'. It is closely associated with the common mistake of conflating correlation with causation.

(Made up) Examples:
- Preference for public transport for green vs. conservative voters (X = green/conservative, Y=frequency of use of public transport; C = place of residence): The fact that green voters predominantly live in cities while conservative voters live in rural areas may suggest that green voters are more conscious of the environment while in fact much of the 'observed effect' can be explained by the mere fact that cities have more green voters
![](Pasted%20image%2020250223221155.png)

**How to handle**: correct for them in you analysis!
## Mediator
A mediator variable M helps explain an observed effect of X on Y. M is a factor in the causal chain, i.e. it must be a causal result of X and causal antecedent of Y. 
![](Pasted%20image%2020250223220455.png)
Examples:
![](Pasted%20image%2020250223221359.png)

How to handle: 
## Moderator
A moderator variable M is NOT on the causal pathway between X and Y, but it _does_ affect the strength and/or direction of the X -> Y relationship.

Example: If present, distraction has a negative effect on learning and may hamper any positive effect of curiosity on learning.

![](Pasted%20image%2020250223174930.png)