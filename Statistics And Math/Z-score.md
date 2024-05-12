See also [Wikipedia](https://en.wikipedia.org/wiki/Standard_score)

Whenever we have observations that are assumed to be normally distributed with some mean $\mu$ and standard deviation $\sigma$, we can apply the standard score (also known as z-score). Usually, we use this score to conduct a Z-test.

It is obtained by standardizing a distribution using its population mean $\mu$ and standard deviation $\sigma$, like so:
$$
z = {x- \mu \over \sigma}
$$
Note, however, that in practice we can only estimate $\mu$ and $\sigma$ based on a sample of size $n$. , i.e. the sample mean $\bar{x}$ and sample standard deviation $s$. Therefore, in practical applications, they are commonly used instead:
$$
z = {x- \bar{x} \over s}
$$
If the sample size $n$ is small and we aren't confident that the observations are in fact normally distributed, the t-statistic (and related t-test) is a better choice.