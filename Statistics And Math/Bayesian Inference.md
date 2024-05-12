Bayesian inference is an approach that is very similar to the way humans think: We start out with some prior belief and update this belief based on our experience.

In Bayesian inference, we build models that also start with an initial assumed probability distribution (prior distribution) based on existing knowledge or beliefs. As new data is gathered, this prior distribution is updated to obtain a new probability distribution (posterior distribution) that reflects the updated beliefs in light of the new evidence.
## Bayes Theorem
Bayes theorem is frequently introduced in the realm of probability of events. The theorem can be summarized in this rather simple formula:
$$
P(A|B) = \frac{P(B|A) \cdot P(A)}{P(B)}
$$
- $P(A|B)$ represents the posterior probability of event $A$ given the occurrence of event $B$. It's what we want to find out after considering the new evidence $B$.
- $P(B|A)$ is the likelihood of event $B$ happening if we assume that event $A$ has occurred. It quantifies how likely $B$ is under the condition of $A$.
- $P(A)$ is the prior probability of event $A$, which reflects our initial belief in the probability of $A$ before considering any evidence from $B$.
- $P(B)$ is the marginal probability of event $B$, indicating the overall likelihood of event $B$ occurring, regardless of whether $A$ is true or not. Actually, this is a kind of _normalizing constant_, as only after dividing $P(B|A) \cdot P(A)$ with $P(B)$  it becomes a valid probability.

We can also choose to rewrite Bayes Theorem using words instead of mathematical symbols:
$$
\text{Posterior}=\frac{\text{Likelihood} \cdot \text{Prior}}{\text{Normalizing Constant}}
$$
## Applying Bayes Theorem
Here's a practical example for when Bayes theorem can be used to estimate probabilities of events given prior assumptions (credits to [Veritasium](https://youtu.be/R13BD8qKeTg?si=uzC4Ybhc5IebdZsh)):

Imagine you get diagnosed with a rare illness that only affects 0.1% of the population. After you ask the doctor, how certain she is that you indeed have this disease, she answers:

>"The test correctly identifies 99% of people that have the disease. Only 1% of people that don't have the disease are false positives."

What are the chances that you have the disease? Many people would intuitively assume the answer is 99%, but that is **wrong**. To answer the question, we can use Bayesian statistics:
$$
P(H|E) = \frac{P(E|H) \cdot P(H)}{P(E)}
$$
- $H$ denotes the hypothesized event, in this case 'having the disease'.
- $E$ stands for another event, in this case 'testing positive'.
- $P(H|E)$ represents the probability of the hypothesis $H$ given an event $E$. In the example, this is the probability of having the disease if you tested positive. This is the quantity we are interested in.
- $P(E|H)$ is the likelihood of event $E$ assuming the hypothesis $H$ is true. In the example, this is the likelihood of testing positive if you have the disease, which is given. $P(E|H)=99\%=0.99$.
- $P(H)$ is the prior probability of the hypothesis $H$, i.e. the initial belief about its probability (under no particular conditions). A reasonable value for the particular case would be the overall frequency of the disease in the population. We learned earlier that this is 1% of the population (i.e. one in a thousand), so $P(H)=\frac{1}{1000}=0.001$.
- $P(E)$ is the overall likelihood of testing positive, regardless of whether the hypothesis $H$ holds or not. Note that this is equivalent to the sum of the probability for being a _true positive_  $P(H)\cdot P(E|H)$ and the probability for being a _false positive_ $P(\neg H) \cdot P(E|H)$.

Let's compute the result:
$$
P(H|E) = \frac{P(E|H) \cdot P(H)}{P(E)} = \frac{P(E|H) \cdot P(H)}{P(H)\cdot P(E|H) + P(\neg H) \cdot P(E|H)} = \frac{0.99 \cdot 0.001}{0.001 \cdot 0.99 + 0.999 \cdot 0.01} \approx 0.09
$$

The answer is 9%, not 99. Note that we call this result we obtained here the _posterior_ probability, as we updated our _prior_ belief based on an observed event.

When visualizing things step-by-step, this makes total sense:
![](Pasted%20image%2020230918213151.png)

This grid of dots represents a random, representative sample of 1000 people from the population. The red dot is the 1 person out of 1000 that is expected to have the disease based on our prior probability $P(H)$. If all the 1000 people in the sample were tested, there's a 1% chance for a false positive as $P(\neg H |E)=1-P(H|E)=1-0.99=0.01=1\%$. This means that 10 people can be expected to be false negatives. This leaves us with 11 people that are expected to be positive, out of which one truly is positive. And, as you know, $\frac{1}{11} \approx 0.09 = 9 \%$. Isn't that remarkable? :)

![](Pasted%20image%2020230918215514.png)
## The idea of updating your belief
Let's continue the thought experiment from above:

You do another, independent test for the disease (in another lab with different methodology) and it also comes back positive. What is the new probability for having the disease, knowing that you tested positive twice?

For this, we can apply the exact same formula. However, now the posterior probability $P(H|E)$ takes the role of the prior probability $P(H)$. So, we just need to enter different values for $P(H)$
and $P(\neg H)=1-P(H)$:
$$
P(H|E) = \frac{P(E|H) \cdot P(H)}{P(E)} = \frac{P(E|H) \cdot P(H)}{P(H)\cdot P(E|H) + P(\neg H) \cdot P(E|H)} = \frac{0.99 \cdot 0.09}{0.09 \cdot 0.99 + 0.91 \cdot 0.01} \approx 0.9
$$
Notice how now the _posterior probability_ suddenly skyrocketed to 90%!
## 'Translating' Bayes Theorem for inference
With all the knowledge we collected, we are finally ready to connect things with statistical learning and Data Science. We can rewrite the initial Bayes Theorem formula, using parameters of some model $\theta$ instead of $A$ and observed data $D$ instead of $B$:
$$
P(\theta|D) = \frac{P(D|\theta) \cdot P(\theta)}{P(D)}
$$
Then, the interpretation is slightly different again:
- $P(\theta|D)$ represents the _posterior_ probability of the parameter(s) $\theta$ given the data $D$. This is what we want to compute—the updated probability distribution for the parameter(s) after observing the data.
- $P(D|\theta)$ is the likelihood function, which quantifies the probability of observing the data $D$ given a specific set of parameter values $\theta$. It measures how well the model with parameter values $\theta$ explains the observed data.
- $P(\theta)$ is the prior probability distribution for the parameter(s) $\theta$. It represents our initial beliefs or uncertainty about the parameter(s) before observing any data.
- $P(D)$ is the marginal likelihood or evidence, which is the probability of observing the data $D$ irrespective of any specific parameter values. It serves as a normalization constant to ensure that the posterior distribution integrates to 1.