this concept is related to correlation. It occurs when input variables are correlated with each other, but they aren't all directly correlated with the target.

## Example
Let's create an artificial dataset, illustrating the problem of correlated regressors.
```r
set.seed(123)
x1 <- runif(100)
y <- x1 + 0.5 * rnorm(100) # true model with some random noise
plot(x1,y)
#summary(lm(y ~ x1))

#x2 <- runif(100)
#plot(data.frame(y,x1,x2))
#summary(lm(y ~ x1 + x2))

#x3 <- x1 + 0.1 * runif(100)
#plot(data.frame(y,x1,x2,x3))
```