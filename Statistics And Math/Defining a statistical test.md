Statistical tests allow us to make statements about any larger (or even infinite?) population based on a smaller sample.

## Components of a statistical test
The core components of any statistical test are:
- a large (possibly infinite) _population_ of data we are interested to learn about
- (exactly!) two types of hypotheses about the population:
	1. the null hypothesis $H_{0}$ and the corresponding
	2. alternate hypothesis $H_{1}$
- A sample of data of size $n$ from the population that is used to verify these hypotheses
- a suitable test statistic for the hypotheses from which we can compute a p-value
- a (pre-defined!) significance level $\alpha$ for the p-value that we use as a 'decision boundary' for whether we can reject $H_0$ or not

## The general procedure
Note: This was put together with the help of ChatGPT

Every statistical test follows roughly the same procedure.
### 1. Define hypotheses, test statistic and significance level $\alpha$
The **null hypothesis $H_{0}$** is the default or status quo hypothesis, often stating that there is no effect, no difference, or no relationship in the population.

The **Alternative Hypothesis $H_{1}$** is the hypothesis we want to test, suggesting that there is a specific effect, difference, or relationship in the population.

Finally, we need to define a **test statistic** that measures the extent of the difference or effect we're testing. Then, we define a **significance level** $\alpha$ for the **p-value** that can be calculated from the test statistic.

The p-value will later give us the probability of obtaining a test statistic as extreme as, or more extreme than, the one we calculated, assuming that $H_{0}$ is true. 
### 2. Run calculations on sample
We then use a sample to compute the test statistic we are interested in. How this sample is obtained differs widely depending on the field.
### 3. Make conclusions
Now that we have the data, we can make the decision whether we can reject $H_{0}$ in favor of $H_{1}$ or not based on $\alpha$:
 - If the p-value is $\leq \alpha$ we can reject $H_{0}$. The observed effect is considered _statistically significant_, i.e. the observed data is highly unlikely given the assumption that $H_{0}$ holds.
 - Otherwise, we _fail to reject_ $H_{0}$. This does **not** mean that we 'accept' $H_{0}$. We only haven't found enough evidence that would allow us to reject it.

**Note**: It is crucial that we don't change $\alpha$ to our liking, just to make results statistically significant. If we were to do that, this would be highly 'unscientific'. It is related to a concept called [p-hacking](https://youtu.be/FLNeWgs2n_Q?si=R3Ta8Cns6yigWzKt).
## Caveat: implicit assumptions
With any statistical test, we make some assumptions about the population we sample from. Very often we assume that our measurements follow a certain distribution. Depending on how many assumptions we can reasonably make, we can formulate 'stronger' tests that give us more confidence. At the same time, if any of those assumptions are possibly violated, this also means that any results we obtain are less reliable.

A classic example of a stricter and less strict test are the t-test and z-test. We use both of them for conducting one- or two-tailed tests for observed sample means. The z-test is far easier to understand (for instance, we don't have to care about degrees of freedom).

However, the z-test is also not nearly as widely applicable as the t-test, as we make several assumptions, including:
- normal distribution
- known mean
- known variance

In practice, we can still often get away with using the z-test in many cases (cf. [Central Limit Theorem](Central%20Limit%20Theorem.md)). But still, we need to be careful