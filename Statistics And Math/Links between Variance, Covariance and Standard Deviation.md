As with any statistical measure, the variance, covariance and standard deviation have formulas for their _true/population_ parameters and respective sample _estimates_. The latter are much more relevant for practical purposes and hence discussed here.
## Variance
Variance is a measure for 'dispersion' _within_ a certain random variable $X$. The formula for the sample variance $s^2$ is used all the time in statistics:
$$s^2=\hat{\sigma}^2(X)=\frac{1}{n-1}\sum_{i=1}^n(x_{i} -\bar{x})^2$$
As the calculation involves squared terms and $n$ needs to be at least 2, the variance can never be negative.
## Covariance
(Sample) covariance tells us if there is an observable 'trend' in the _relationship between two variables_ of sampled data. The formula for sample covariance is only slightly different, but _really_ intimidating and confusing as it is often expressed in terms of entries of the covariance matrix (like in the [Wiki article on covariance](Calculating_the_sample_covariance)). So, here's my take at expressing covariance more intuitively.

Imagine, we have $n$ observations of two (real) random variables $X$ and $Y$ with sample means $\bar{x}$ and $\bar{y}$. Then, every $i^{th}$ observation consists of the tuple $(x_i, y_i)$ and the sample covariance $\widehat{Cov}(X,Y)$ can then be computed like this:
$$
\widehat{Cov}(X,Y)=\frac{1}{n-1}\sum_{i=1}^{n}(x_{i}-\bar{x})(y_{i}-\bar{y})
$$
Contrary to variance, covariance can take on both positive and negative values. It has the following interpretation:
- If $\widehat{Cov}(X,Y)>0$  a large value in $X$ generally implies a larger value in $Y$
- If $\widehat{Cov}(X,Y)<0$, a large value in $X$ generally implies a smaller value in $Y$ is smaller
- $\widehat{Cov}(X,Y)=0$, there is no relationship between the values of $X$ and those of $Y$ at all

On its own, covariance is not really that meaningful. However, it is used behind the scenes by many important statistical methods, such as [PCR](Relevant%20topics%20(list%20given%20in%20lecture).md#PCR). Also, it is the stepping stone for computing [correlation](Covariance%20vs.%20Correlation.md) (spoiler: we also need the standard deviation).
## Link between variance and covariance
If we use the same variable the first and second parameter of the covariance function, we get the variance!
$$
\begin{align}
Cov(X,X)=\sigma^2(X) \\
\widehat{Cov}(X,X)=\hat{\sigma}^2(X)
\end{align}
$$
## Standard Deviation
The problem with both variance and covariance is that they are expressed in terms of _squared units_. To fix this, we can just take the square root of either of them, which gives us the standard deviation!

The standard deviation has another important role wrt. covariance: we need it as a stepping stone to compute [correlation](Covariance%20vs.%20Correlation.md)!



