See also [this](https://youtu.be/xZ_z8KWkhXE?si=pd8u3HBIz83bQkX3) video
## Why correlation is more useful than covariance
[Covariance](Links%20between%20Variance,%20Covariance%20and%20Standard%20Deviation.md#Covariance) only tells us if there is a 'general trend' in the relationship between two variables $X$ and $Y$. However, covariance alone is not a very useful metric, as it is sensitive to the scale of the compared variables. 

Correlation, specifically the [Pearson correlation coefficient](https://en.wikipedia.org/wiki/Pearson_correlation_coefficient) essentially corrects for differences in scales and gives us a metric that can take on any value in the interval $[-1, 1]$. When applied to a population, it is commonly denoted with $\rho$, while $r$ is typically used for the sample correlation.
## Interpretation
A quick written interpretation:
- $r=1$ implies perfect positive correlation, i.e. clear positive relationship between $X$ and $Y$.
- Vice versa, $r=-1$ implies perfect negative correlation (clear negative relationship).
- $r=0$ implies no correlation, i.e. no relationship between values of $X$ and $Y$ at all.

Visual interpretation is easier. We can plot variables against each other. Then, perfect positive correlation means that a line with $k>0$ can be drawn through all the points $(x_{1}, y_{1}), \cdots (x_{n}, y_{n})$. Similarly, for perfect negative correlation, the line would have a slope $k<0$. 
![perfect correlation](Pasted%20image%2020230920151315.png)
As correlation decreases, the observations move further away from the line of closest fit to the data (on average):
![](Pasted%20image%2020230920153522.png)
![](Pasted%20image%2020230920153709.png)
![](Pasted%20image%2020230920153954.png)
As long as the correlation is not 0, the line can still be used for inferences, but predictions get increasingly worse, the closer it moves to 0.
## Computation
Pearson's correlation coefficient for the population is defined as:
$$
\rho_{X, Y}=\frac{\operatorname{cov}(X, Y)}{\sigma_X \sigma_Y}
$$
where $cov$ is the covariance and $\sigma_{X}$ and $\sigma_{Y}$ are standard deviations of $X$ and $Y$.

In practice, one would compute the sample correlation coefficient $r_{xy}$ by replacing the true parameters with sample estimates in the formula above. After some [simplifications](pearsons_r_derivation.excalidraw.md), we get the following expression for $r_{x y}$ (given paired data $\left\{\left(x_1, y_1\right), \ldots,\left(x_n, y_n\right)\right\}$ consisting of $n$ pairs):
$$
\begin{align}
r_{x y}=\frac{\sum_{i=1}^n\left(x_i-\bar{x}\right)\left(y_i-\bar{y}\right)}{\sqrt{\sum_{i=1}^n\left(x_i-\bar{x}\right)^2} \sqrt{\sum_{i=1}^n\left(y_i-\bar{y}\right)^2}}
\end{align}
$$
where
- $n$ is the sample size
- $x_i, y_i$ are the individual sample points indexed with $i$
- $\bar{x}=\frac{1}{n} \sum_{i=1}^n x_i$ (the sample mean); and analogously for $\bar{y}$.

There are multiple other ways to express $r_{x y}$, one them being the following definition as the mean of the products of the standard scores:
$$
r_{x y}=\frac{1}{n-1} \sum_{i=1}^n\left(\frac{x_i-\bar{x}}{s_x}\right)\left(\frac{y_i-\bar{y}}{s_y}\right)
$$where 
- $s_x=\sqrt{\frac{1}{n-1} \sum_{i=1}^n\left(x_i-\bar{x}\right)^2}$ is the sample standard deviation of $x$ (and analogously for $s_y$).
- $\left(\frac{x_i-\bar{x}}{s_x}\right)$ is the standard score (and analogously for the standard score of $y$).
## Caution: Correlation != Causality
Note that even with high correlation we still haven’t answered the question of causality! I.e., we cannot say anything about whether $X$ _causes_ changes in $Y$ or vice versa. They just _change together_.