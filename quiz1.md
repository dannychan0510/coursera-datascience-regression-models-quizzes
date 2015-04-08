# Question 1
Consider the data set given below

`x <- c(0.18, -1.54, 0.42, 0.95)`

And weights given by

`w <- c(2, 1, 3, 1)`

Give the value of μ that minimizes the least squares equation

# Solution to Question 1

```
> x <- c(0.18, -1.54, 0.42, 0.95)
> w <- c(2, 1, 3, 1)
> optimize(function(u){ sum(w*(x-u)^2)}, interval=c(-100,100))
$minimum
[1] 0.1471429

$objective
[1] 3.716543
```

# Question 2
Consider the following data set
```
x <- c(0.8, 0.47, 0.51, 0.73, 0.36, 0.58, 0.57, 0.85, 0.44, 0.42)
y <- c(1.39, 0.72, 1.55, 0.48, 1.19, -1.59, 1.23, -0.65, 1.49, 0.05)
```
Fit the regression through the origin and get the slope treating y as the outcome and x as the regressor. (Hint, do not center the data since we want regression through the origin, not through the means of the data.)

# Solution to Question 2

```
> x <- c(0.8, 0.47, 0.51, 0.73, 0.36, 0.58, 0.57, 0.85, 0.44, 0.42)
> y <- c(1.39, 0.72, 1.55, 0.48, 1.19, -1.59, 1.23, -0.65, 1.49, 0.05)
> fit <- lm(y ~ x)
> coefficients(fit)
(Intercept)           x 
   1.567461   -1.712846 
```

# Question 3
Do `data(mtcars)` from the datasets package and fit the regression model with mpg as the outcome and weight as the predictor. Give the slope coefficient.

# Solution to Question 3

```
> data(mtcars)
> dB <- as.data.frame(mtcars)
> fit <- lm(mpg ~ weight, data = dB)
> fit <- lm(mpg ~ wt, data = dB)
> coefficients(fit)
(Intercept)          wt 
  37.285126   -5.344472 
```

# Question 4
Consider data with an outcome (Y) and a predictor (X). The standard deviation of the predictor is one half that of the outcome. The correlation between the two variables is .5. What value would the slope coefficient for the regression model with Y as the outcome and X as the predictor?

# Solution to Question 4
```

