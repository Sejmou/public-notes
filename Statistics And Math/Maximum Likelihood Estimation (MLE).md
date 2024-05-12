A prerequisite for this is an understanding of the difference between [probability and likelihood](Probability%20vs.%20Likelihood.md).

[This](https://towardsdatascience.com/probability-concepts-explained-maximum-likelihood-estimation-c7b4342fdbb1) article is pretty good. It also describes the general concept quite succinctly:

>Maximum likelihood estimation is a method that determines values for the parameters of a model. The parameter values are found such that they maximize the likelihood that the process described by the model produced the data that were actually observed.

An important assumption with MLE is that every data point is generated independently of the others. This allows us to simply multiply probabilities!
## Example: MLE for normal distribution
In this toy example, we have three measurements that are assumed to follow the normal distribution: 9, 9.5, and 11. Then, the joint probability density _given_ this data can be expressed as:
$$ P(9,9.5,11 ; \mu, \sigma) = \frac{1}{\sigma \sqrt{2 \pi}} \exp \left(-\frac{(9-\mu)^2}{2 \sigma^2}\right) \times \frac{1}{\sigma \sqrt{2 \pi}} \exp \left(-\frac{(9.5-\mu)^2}{2 \sigma^2}\right) \times \frac{1}{\sigma \sqrt{2 \pi}} \exp \left(-\frac{(11-\mu)^2}{2 \sigma^2}\right) $$

All we need to do is find values of $\mu$ and $\sigma$ that maximize the above expression. The easiest way to achieve that is to actually maximize the _log_-likelihood as this is equivalent to maximizing the likelihood itself _and_ comes with additional benefits such as numerical stability (e.g. the multiplication of multiple small values becomes the addition of logarithms, etc.).