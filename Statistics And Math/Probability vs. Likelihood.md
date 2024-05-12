Most of the information here is taken from [this](https://youtu.be/pYxNSUDSFH4?si=_x-JUWcmNvdIj3e7) and [this](https://youtu.be/XepXtl9YKwc?si=5vmHEg3uGCzqHq4m) awesome video. The example that is used here builds on hypothesized weight measures for mice, which are assumed to follow a normal distribution. The general concepts discussed translate to other continuous distributions as well.

However, for discrete distributions, quite a bit of stuff is different (e.g. probability density functions do not exist; probability mass functions are used to derive probabilities instead), which is not discussed here.
## Probability
The meaning of probabilities is rather intuitive: they tell us, how likely it is that we get a particular result or output value. However, for continuous variables, probabilities can only be expressed for a _value range_. The probability that we get a result in a particular value range is equivalent to the 'size of the area under the curve' of the [probability _density_ function](https://en.wikipedia.org/wiki/Probability_density_function) of the assumed probability distribution for that value range. To compute it, we need to use a definite integral whose upper and lower bounds are the boundary values of the range we are interested in.
![Probability](Probability.png)
To be exact, IIUC, when we compute probabilities for observing a certain range of values in real-world data, we always compute _conditional_ probabilities _under the assumption_ that they follow some distribution (as we cannot know what the _real_ distribution is). This assumed distribution needs to be defined further by specifying _parameters_.

For example, if we assume the weight of mice is normally distributed (with a mean of 32 and a standard deviation of 2.5), the calculation would look like this:

The expression on the left side of the `|` stands for the 'input' that is used for the computation of the probability, while the right hand side expresses the conditions for this probability (parameters for the assumed distribution, a normal distribution in this case).
## Likelihood
On the other hand, _likelihood_ tells us how likely it is that our assumed probability distribution is indeed correct, _given_ a particular observation. So, in a way we 'turn the question around'. Let's continue with the mouse weight measurement example to illustrate this:
![](Likelihood.png)
The expression and corresponding illustration show that the likelihood of a normal distribution with a mean of 32 and a standard deviation of 2.5 _given_ that we weighed a 34 gram mouse is 0.12. Notice that if we were to shift the mean of the normal distribution to the right, the likelihood would increase (similarly, it would decrease if the mean became smaller).

This single likelihood value on its own doesn't tell us much. It is merely a measure of the sample's support for the assumed model. Low values can either mean rare data or incorrect model!
## Connection to Maximum Likelihood Estimation
The last sentence from the previous paragraph already gives a hint to why  that more data can help us answer the question whether we are observing rare data or or the model for the distribution of the data is in fact incorrect. If we have a good model, low likelihood values should be very rare, even for larger sets of observations. Hence, if we manage to maximize the overall likelihood for our data, we can be confident that the model matches the data! That is why maximum likelihood estimation is very commonly used in various types of statistical models.
## More strict math notation
In more general math terms, we would denote the probability that a random variable $X$ assumes values between $a$ and $b$ as
$$\operatorname{Pr}[a \leq X \leq b]=\int_a^b f_X(x) dx$$
where $f_{X}$ is the probability density function (pdf) of $X$. IIUC, the suffix is often left out if it is clear what random variable the density function refers to, hence $f_{X}$ becomes just $f$.

In case of the normal distribution, the pdf is
$$f(x)=\frac{1}{\sigma \sqrt{2 \pi}} e^{-\frac{1}{2}\left(\frac{x-\mu}{\sigma}\right)^2}$$
However, if we want to emphasize the parameters that we assume for a given distribution, we would write
TODO: finish

## Key takeaway
In everyday conversations, 'probability' and 'likelihood' mean the same thing. However, in statistics, only 'probability' roughly coincides with that intuitive meaning we associate with the term. 

On the other hand, 'likelihood' is a measure that can tell us how well observed data fits the hypothesis that we have about its underlying distribution. It is closely associated with a core task in statistical modeling, which is identifying the 'correct' type of distribution for the observed data and finding 'optimal values' for its parameters.

