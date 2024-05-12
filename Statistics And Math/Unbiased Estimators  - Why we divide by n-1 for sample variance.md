## Simpler, unsatisfying answer
Usually, the sample mean is always a bit off compared to the true population mean. So, if we compute the sum of squared distances of the sampled data to the sample mean (the numerator of the sample variance formula), this value will always be smaller than the sum of squared distances of the population data to the population mean. Hence, we divide by n-1 to make the sample variance a bit bigger

More details [here](https://www.youtube.com/watch?v=sHRBg6BhKjI)

## What is Bias?
To compute the _bias_ of any estimator is defined we subtract the true parameter value from the estimated value of the estimator:
$$\text{Bias}(\hat{\theta}) = \mathbb{E}(\hat{\theta}) - \theta$$
The concept is exactly the same for the (sample) mean and variance:
$$\text{Bias}(\overline{x}) = \mathbb{E}(\overline{x}) - \mu$$
$$\text{Bias}(s^2) = \mathbb{E}(s^2) - \sigma^2$$
If an estimator is _unbiased_, this just means that its bias is 0.

## Proof that $\bar{x}$ is an unbiased estimator of  $\mu$
It might be pretty obvious that by just taking _enough_ samples, we can be sure that for any variable that has a well-defined mean (such as age, height, etc.) we will eventually move closer to the true mean of the whole population. It might also sound pretty 

Let $x_1, x_2, \ldots, x_n$ be a random sample of size $n$ drawn from a population with a finite population mean $\mu$. The sample mean $\bar{x}$ is defined as:
$$
\bar{x} = \frac{1}{n} \sum_{i=1}^{n} x_i
$$
Now, we want to find the expected value (mean) of $\bar{x}$, denoted as $E(\bar{x})$.

Using the properties of expectation (linearity of expectation), we have:

$$
E(\bar{x}) = E\left(\frac{1}{n} \sum_{i=1}^{n} x_i\right)
$$

Since the random variables $x_1, x_2, \ldots, x_n$ are drawn from the same population, they have the same expected value, which is $\mu$.

Now, we can apply the linearity of expectation:
$$
E(\bar{x}) = \frac{1}{n} \sum_{i=1}^{n} E(x_i)
$$
Since each $x_i$ has the same expected value, the population mean $\mu$, we can write:
$$
E(\bar{x}) = \frac{1}{n} \sum_{i=1}^{n} \mu
$$
Now, we can simplify the summation:
$$
E(\bar{x}) = \frac{1}{n} \cdot n \cdot \mu
$$
The $n$ in the numerator and denominator cancel out:
$$
E(\bar{x}) = \mu
$$
Therefore, we have shown that the expected value of the sample mean $\bar{x}$ is indeed equal to the true population mean $\mu$.
## Why this result matters
This result is a fundamental property of sample means and is one of the key principles of statistical inference. It tells us that, on average, the sample mean is an unbiased estimator of the population mean, regardless of the sample size $n$.

We can use very similar approaches of just rearranging stuff to formally proof that estimators for other quantities are also unbiased. One of the more important ones is the proof that $s^2$, the unbiased estimator for the population variance $\sigma^2$,  is $\frac{1}{n-1}\sum_{i=1}^n(x_{i} -x)^2$ . For a proof, we would again rewrite things in terms of the expected value of $s^2$.

In a nutshell: If we started our proof plugging in $\frac{1}{n}\sum_{i=1}^n(x_{i} -x)^2$ for $s^2$ we would find out that things just don't work out. Only once we understand stuff like this we are probably ready to even start to try to understand other, more elaborate proofs. En example is the proof that the least squares linear regression coefficients estimate $\boldsymbol{\beta}_{j}$ is the best, linear, unbiased (BLUE) estimator of the true regression coefficients $\boldsymbol{\beta}$.

## Additional 'Fun-Fact'
While $s^2$ is an unbiased estimate for the population variance $\sigma^2$, $s=\sqrt{s^2}$ is [_not_ an unbiased estimate for the population standard deviation](https://en.wikipedia.org/wiki/Standard_deviation#Unbiased_sample_standard_deviation).

More details on the subject can be found [here](https://en.wikipedia.org/wiki/Unbiased_estimation_of_standard_deviation). But you should probably not worry about any of that as the referenced page states:

>Except in some important situations, outlined later, the task has little relevance to applications of statistics since its need is avoided by standard procedures, such as the use of [significance tests](https://en.wikipedia.org/wiki/Significance_test "Significance test") and [confidence intervals](https://en.wikipedia.org/wiki/Confidence_intervals "Confidence intervals"), or by using [Bayesian analysis](https://en.wikipedia.org/wiki/Bayesian_analysis "Bayesian analysis").

and 

>It also provides an example where imposing the requirement for [unbiased estimation](https://en.wikipedia.org/wiki/Bias_of_an_estimator "Bias of an estimator") might be seen as just adding inconvenience, with no real benefit.

lol

I could not find an explanation for the first claim on this site, but the [section on corrected sample standard deviation](https://en.wikipedia.org/wiki/Standard_deviation#Corrected_sample_standard_deviation) on the standard deviation page states that However, the same page also mentions that

>The bias may still be large for small samples (_N_ less than 10). As sample size increases, the amount of bias decreases.

So, I assume for any reasonable 'real-life' sample sizes, this 'issue' can safely be ignored