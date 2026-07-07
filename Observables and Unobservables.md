# Panel-Data-Econometrics
This repository explains important concepts in Panel data econometrics and summarizes all practical code to run panel data econometrics models in R and Stata

# Observable vs. Unobservable Variables in Econometrics

> *One of the primary motivations for panel data econometrics is to deal with variables that influence the outcome but cannot be directly observed.*

---

## Introduction

In empirical research, we aim to understand how one or more variables affect an outcome. For example, we may want to answer questions such as:

- Does education increase wages?
- Does experience improve productivity?
- Does a firm's reputation increase employee retention?

To answer these questions, we estimate regression models using observable data. However, not every factor influencing the outcome can be measured. This distinction between **observable** and **unobservable** variables lies at the heart of modern econometrics.

---

## Observable Variables

Observable variables are characteristics that can be measured, collected, and included in a dataset.

### Examples

| Variable | Observable? |
|-----------|-------------|
| Wage | ✅ Yes |
| Age | ✅ Yes |
| Years of education | ✅ Yes |
| Firm size | ✅ Yes |
| Work experience | ✅ Yes |
| Number of promotions | ✅ Yes |

Because these variables are observed, they can be included directly in a regression model.

For example,

\[
\text{Wage} = \beta_0 + \beta_1 \text{Education} + \beta_2 \text{Experience} + \varepsilon
\]

---

## Unobservable Variables

Unobservable variables affect the dependent variable but cannot be measured or are unavailable in the dataset.

Examples include:

| Variable | Observable? |
|-----------|-------------|
| Ability | ❌ No |
| Talent | ❌ No |
| Motivation | ❌ No |
| Ambition | ❌ No |
| Personality | ❌ No |
| Leadership skills | ❌ No |
| Firm culture | ❌ Usually No |
| Management quality | ❌ Often No |

These variables exist and may have a substantial impact on the outcome, but the researcher cannot directly include them in the model.

---

# Why Are Unobservable Variables a Problem?

Suppose we are interested in estimating the effect of education on wages.

The true relationship is

\[
\text{Wage}
=
\beta_0
+
\beta_1 \text{Education}
+
\beta_2 \text{Ability}
+
u
\]

Unfortunately, **ability** is unobservable.

Therefore, the researcher estimates

\[
\text{Wage}
=
\beta_0
+
\beta_1 \text{Education}
+
\varepsilon
\]

If more able individuals tend to obtain more education, education and ability become correlated.

As a result,

- part of the effect of ability is mistakenly attributed to education,
- the estimated coefficient of education becomes biased,
- increasing the sample size does **not** solve the problem.

This is known as **omitted variable bias**.

---

# A Simple Example

Imagine three workers.

| Worker | Education | Ability | Wage |
|---------|-----------|----------|------|
| Alice | 16 | High | High |
| Bob | 16 | Low | Medium |
| Carol | 12 | Medium | Medium |

Suppose ability cannot be observed.

If we estimate wages using only education,

we may conclude that education explains all wage differences,

when, in reality, part of the difference is caused by ability.

---

# Why Panel Data Help

Panel data observe the **same individuals repeatedly over time**.

Instead of writing

\[
y_i=\beta x_i+\varepsilon_i
\]

we write

\[
y_{it}
=
\alpha_i
+
\beta x_{it}
+
u_{it}
\]

where

- \(i\) denotes the individual,
- \(t\) denotes time,
- \(\alpha_i\) captures all **time-invariant unobservable characteristics**.

Examples of what may be included in \(\alpha_i\):

- innate ability
- intelligence
- personality
- family background
- motivation
- permanent work ethic

---

# The Key Idea of Fixed Effects

The Fixed Effects estimator removes

\[
\alpha_i
\]

from the model by comparing each individual **with themselves over time** rather than comparing different individuals.

Instead of asking

> "Why does Alice earn more than Bob?"

it asks

> "How did Alice's wage change when her experience increased?"

Since Alice's ability is constant over time,

it is eliminated from the estimation.

This allows us to estimate the effect of observable variables without bias from time-invariant unobservable characteristics.

---

# Observable vs. Unobservable Variables

| Feature | Observable | Unobservable |
|----------|------------|--------------|
| Can be measured | ✅ | ❌ |
| Included directly in regression | ✅ | ❌ |
| Available in dataset | ✅ | ❌ |
| May bias estimates if omitted | — | ✅ |
| Can be controlled by Fixed Effects (if time-invariant) | — | ✅ |

---

# Key Takeaways

- Econometric models rely on observable variables, but important determinants are often unobservable.
- Ignoring relevant unobservable variables can lead to omitted variable bias.
- Panel data methods, especially the Fixed Effects estimator, are designed to eliminate the influence of **time-invariant unobservable characteristics**.
- This is one of the main reasons why panel data are often preferred over purely cross-sectional data.

---

## Summary

Understanding the distinction between observable and unobservable variables is fundamental to panel data econometrics. The central goal of many panel estimators is not merely to estimate relationships more efficiently, but to obtain **consistent estimates** by controlling for unobserved heterogeneity that would otherwise bias the results.

### file 1
lm() isn't a package — it's a built-in function in R (part of the base stats package that loads automatically). It fits linear models using ordinary least squares (OLS) regression.
Basic usage looks like this:

model <- lm(y ~ x1 + x2, data = mydata)       ### mydata is the dataset

summary(model)

The formula y ~ x1 + x2 means "regress y on x1 and x2". An intercept is included by default. summary() gives you coefficients, standard errors, t-statistics, p-values, R², and F-statistic.
Stata equivalent: regress (often abbreviated reg)

regress y x1 x2
