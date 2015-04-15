# Question 1
Consider the following data with x as the predictor and y as as the outcome.
```
x <- c(0.61, 0.93, 0.83, 0.35, 0.54, 0.16, 0.91, 0.62, 0.62)
y <- c(0.67, 0.84, 0.6, 0.18, 0.85, 0.47, 1.1, 0.65, 0.36)
```
Give a P-value for the two sided hypothesis test of whether β1 from a linear regression model is 0 or not.

## Solution to Question 1
```
> x <- c(0.61, 0.93, 0.83, 0.35, 0.54, 0.16, 0.91, 0.62, 0.62)
> y <- c(0.67, 0.84, 0.6, 0.18, 0.85, 0.47, 1.1, 0.65, 0.36)
> fit <- lm(y ~ x)
> summary(fit)

Call:
lm(formula = y ~ x)

Residuals:
     Min       1Q   Median       3Q      Max 
-0.27636 -0.18807  0.01364  0.16595  0.27143 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)  
(Intercept)   0.1885     0.2061   0.914    0.391  
x             0.7224     0.3107   2.325    0.053 .
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 0.223 on 7 degrees of freedom
Multiple R-squared:  0.4358,	Adjusted R-squared:  0.3552 
F-statistic: 5.408 on 1 and 7 DF,  p-value: 0.05296
```


# Question 2
Consider the previous problem, give the estimate of the residual standard deviation.

## Solution to Question 2
```
0.223
```


# Question 3
In the `mtcars` data set, fit a linear regression model of weight (predictor) on mpg (outcome). Get a 95% confidence interval for the expected mpg at the average weight. What is the lower endpoint?

## Solution for Question 3
```
dB <- as.data.frame(mtcars)
fit <- lm(mpg ~ wt, data = dB)
```
