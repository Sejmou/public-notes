A confounding variable C (also known as confounder) affects **both** X and Y. So, any change in Y that we observe may be wrongly attributed to the change in X. This creates a 'spurious relationship' (closely associated with the common mistake of conflating correlation with causation).

(Made up) Examples:
- Preference for public transport for green vs. conservative voters (X = green/conservative, Y=frequency of use of public transport; C = place of residence): The fact that green voters predominantly live in cities while conservative voters live in rural areas may suggest that green voters are more conscious of the environment while in fact much of the 'observed effect' can be explained by the mere fact that cities have more green voters
![](Pasted%20image%2020250223221155.png)

**How to handle**: correct for them in you analysis! This can be achieved via
- randomized experiment: if we are aware of the confounders by which participants are affected, we need to make sure to assign them to separate groups, ensuring that the confounders are equally distributed among them. Then we can be sure that observed differences between those groups are in fact treatment effects of X on Y. 
- ...