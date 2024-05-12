In statistics, BLUE stands for **B**est **L**inear **U**nbiased **E**stimator.

Best in this sense means smallest variance out of all types of estimates. Unbiased means that if we were to fit estimators $k$ times on different samples from the population, the averages of the $k$ estimates would move closer to the true population parameter as $k$ increases (cf. [Unbiased Estimators  - Why we divide by n-1 for sample variance](Unbiased%20Estimators%20%20-%20Why%20we%20divide%20by%20n-1%20for%20sample%20variance.md) and [Bias vs. Variance](Bias%20vs.%20Variance.md)).

## Example
In linear regression, [least squares estimators for the regression coefficients](1.%20Ordinary%20Least%20Squares%20Regression.md)  are BLUE.