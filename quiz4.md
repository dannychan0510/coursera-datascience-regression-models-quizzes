# Quiz 4

## Question 1
Consider the space shuttle data ?shuttle in the MASS library. Consider modeling the use of the autolander as the outcome (variable name use). Fit a logistic regression model with autolander (variable auto) use (labeled as "auto" 1) versus not (0) as predicted by wind sign (variable wind). Give the estimated odds ratio for autolander use comparing head winds, labeled as "head" in the variable headwind (numerator) to tail winds (denominator).

### Solution to Question 1
```
library(MASS)
head(shuttle)
shuttle2<-shuttle
shuttle2$use2<-as.numeric(shuttle2$use=='auto')
#shuttle2$wind2<-as.numeric(shuttle2$wind=='head')
#head(shuttle2)
fit<-glm(use2 ~ factor(wind) - 1, family = binomial, data = shuttle2)

#0.03181

#fit<-glm(use ~ wind, family = binomial, data = shuttle)
#anova(fit)
summary(fit)$coef
```


## Question 2
Consider the previous problem. Give the estimated odds ratio for autolander use comparing head winds (numerator) to tail winds (denominator) adjusting for wind strength from the variable magn.

### Solution to Question 2
```
fit<-glm(use2 ~ factor(wind) + factor(magn) - 1, family = binomial, data = shuttle2)
summary(fit)$coef

exp(coef(fit))

exp(cbind(OddsRatio = coef(fit), confint(fit)))

1.286 / 1.327
```


## Question 3
If you fit a logistic regression model to a binary variable, for example use of the autolander, then fit a logistic regression model for one minus the outcome (not using the autolander) what happens to the coefficients?

### Solution to Question 3
```
The coefficients reverse their signs.
```


## Question 4
Consider the insect spray data InsectSprays. Fit a Poisson model using spray as a factor level. Report the estimated relative rate comapring spray A (numerator) to spray B (denominator).

### Solution to Question 4
```
fit<-glm(count~factor(spray)-1,data=InsectSprays,family=poisson)
summary(fit)$coef
exp(coef(fit))
14.500  / 15.333
## [1] 0.9457
```


## Question 5
Consider a Poisson glm with an offset, t. So, for example, a model of the form glm(count ~ x + offset(t), family = poisson) where x is a factor variable comparing a treatment (1) to a control (0) and t is the natural log of a monitoring time. What is impact of the coefficient for x if we fit the model glm(count ~ x + offset(t2), family = poisson) where t2 <- log(10) + t? In other words, what happens to the coefficients if we change the units of the offset variable. (Note, adding log(10) on the log scale is multiplying by 10 on the original scale.)

### Solution to Question 5
```
fit<-glm(count ~ factor(spray), family = poisson,data=InsectSprays,offset = log(count + 1))
summary(fit)$coef
##                 Estimate Std. Error  z value Pr(>|z|)
## (Intercept)    -0.066691    0.07581 -0.87972   0.3790
## factor(spray)B  0.003512    0.10574  0.03322   0.9735
## factor(spray)C -0.325351    0.21389 -1.52114   0.1282
## factor(spray)D -0.118451    0.15065 -0.78625   0.4317
## factor(spray)E -0.184623    0.17192 -1.07389   0.2829
## factor(spray)F  0.008422    0.10367  0.08124   0.9352
fit2<-glm(count ~ factor(spray), family = poisson,data=InsectSprays,offset = log(10)+log(count+1))
summary(fit2)$coef
##                 Estimate Std. Error   z value   Pr(>|z|)
## (Intercept)    -2.369276    0.07581 -31.25290 2.039e-214
## factor(spray)B  0.003512    0.10574   0.03322  9.735e-01
## factor(spray)C -0.325351    0.21389  -1.52114  1.282e-01
## factor(spray)D -0.118451    0.15065  -0.78625  4.317e-01
## factor(spray)E -0.184623    0.17192  -1.07389  2.829e-01
## factor(spray)F  0.008422    0.10367   0.08124  9.352e-01
fit<-glm(count ~ factor(spray) + offset(log(count+1)), family = poisson,data=InsectSprays)
summary(fit)$coef
##                 Estimate Std. Error  z value Pr(>|z|)
## (Intercept)    -0.066691    0.07581 -0.87972   0.3790
## factor(spray)B  0.003512    0.10574  0.03322   0.9735
## factor(spray)C -0.325351    0.21389 -1.52114   0.1282
## factor(spray)D -0.118451    0.15065 -0.78625   0.4317
## factor(spray)E -0.184623    0.17192 -1.07389   0.2829
## factor(spray)F  0.008422    0.10367  0.08124   0.9352
fit2<-glm(count ~ factor(spray) + offset(log(10)+log(count+1)), family = poisson,data=InsectSprays)
summary(fit2)$coef
##                 Estimate Std. Error   z value   Pr(>|z|)
## (Intercept)    -2.369276    0.07581 -31.25290 2.039e-214
## factor(spray)B  0.003512    0.10574   0.03322  9.735e-01
## factor(spray)C -0.325351    0.21389  -1.52114  1.282e-01
## factor(spray)D -0.118451    0.15065  -0.78625  4.317e-01
## factor(spray)E -0.184623    0.17192  -1.07389  2.829e-01
## factor(spray)F  0.008422    0.10367   0.08124  9.352e-01

The coefficient estimate is unchanged
```


## Question 6
Consider the data
```
x <- -5:5
y <- c(5.12, 3.93, 2.67, 1.87, 0.52, 0.08, 0.93, 2.05, 2.54, 3.87, 4.97)
```
Using a knot point at 0, fit a linear model that looks like a hockey stick with two lines meeting at x=0. Include an intercept term, x and the knot point term. What is the estimated slope of the line after 0

### Solution to Question 6
```
x <- -5:5
y <- c(5.12, 3.93, 2.67, 1.87, 0.52, 0.08, 0.93, 2.05, 2.54, 3.87, 4.97)


knots<-c(0)
splineTerms<-sapply(knots,function(knot) (x>knot)*(x-knot))
xmat<-cbind(1,x,splineTerms)
fit<-lm(y~xmat-1)
yhat<-predict(fit)

summary(fit)$coef
##       Estimate Std. Error t value  Pr(>|t|)
## xmat   -0.1826    0.13558  -1.347 2.150e-01
## xmatx  -1.0242    0.04805 -21.313 2.470e-08
## xmat    2.0372    0.08575  23.759 1.049e-08
(yhat[10]-yhat[6])/4
##    10 
## 1.013
plot(x,y)
lines(x,yhat,col="red")
```
