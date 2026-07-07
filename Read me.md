# Panel-Data-Econometrics
This repository explains important concepts in Panel data econometrics and summarizes all practical code to run panel data econometrics models in R and Stata


### file 1
lm() isn't a package — it's a built-in function in R (part of the base stats package that loads automatically). It fits linear models using ordinary least squares (OLS) regression.
Basic usage looks like this:

model <- lm(y ~ x1 + x2, data = mydata)       ### mydata is the dataset

summary(model)

The formula y ~ x1 + x2 means "regress y on x1 and x2". An intercept is included by default. summary() gives you coefficients, standard errors, t-statistics, p-values, R², and F-statistic.
Stata equivalent: regress (often abbreviated reg)

regress y x1 x2
