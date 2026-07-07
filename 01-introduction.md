# Chapter 1 — Why Panel Data? Unobserved Heterogeneity

## The problem

Suppose the true data-generating process is

```
y = α + βx + γz + ε
```

where `x` is observable but `z` is not. If we estimate the feasible model
`y = α + βx + ε` by OLS, our estimate of β is only consistent when `z` is
uncorrelated with `x`. Otherwise we have classic omitted-variable bias.

**Canonical example (Mundlak, 1961):** farm output depends on labor (`x`) and
soil quality (`z`). The econometrician can't observe soil quality — but the
farmer can, and chooses labor input accordingly. So `z` and `x` are
correlated and cross-sectional OLS is biased.

## The panel data escape hatch

Write the model for unit *n* at time *t*, splitting the error into a
time-invariant individual component and an idiosyncratic one:

```
y_nt = α + β'x_nt + (η_n + ν_nt)
```

If the unobserved heterogeneity `η_n` is **constant over time**, having
repeated observations per unit lets us eliminate it algebraically. Three
classic ways:

### 1. First differencing (FD)

Subtract each unit's t−1 observation from its t observation. Anything
time-invariant — the intercept and `η_n` — drops out:

```
Δy_nt = β'Δx_nt + Δν_nt
```

Estimate by pooled OLS on differenced data.

### 2. Least squares dummy variables (LSDV)

Give every unit its own intercept by adding N individual dummies. The dummy
absorbs each unit's `η_n`. Degrees of freedom fall to NT − N − K. β is
NT-consistent, but the individual intercepts are only T-consistent (they rely
on each unit's own time series) — usually we don't care about them anyway.

### 3. Fixed effects / within transformation

LSDV becomes computationally clumsy with many units. The equivalent shortcut:
**demean** every variable by its unit-level time average,

```
(y_nt − ȳ_n) = (x_nt − x̄_n)'β + (ν_nt − ν̄_n)
```

and run OLS on the demeaned data. The β estimates are *numerically
identical* to LSDV. This "within estimator" is the standard fixed effects
method.

**Key limitation of all three:** any regressor that is constant over time for
a unit (e.g., a state's geography, a person's birthplace) is wiped out along
with `η_n` — its coefficient cannot be estimated.

---

## Worked example: beer taxes and traffic deaths

The `Fatalities` dataset (Stock & Watson; US states 1982–1988) asks whether
higher beer taxes reduce the road death toll. It's a textbook illustration of
heterogeneity bias: naive estimates say higher taxes go with *more* deaths,
because states with worse drunk-driving problems adopt higher taxes. Fixed
effects flips the sign.

### Setup

**R**

```r
library("plm")
library("AER")
library("lmtest")

data("Fatalities", package = "AER")
Fatalities$frate <- with(Fatalities, fatal / pop * 10000)
fm <- frate ~ beertax
```

**Stata**

```stata
* after importing the data (e.g., from the AER package export)
gen frate = fatal / pop * 10000
encode state, gen(state_id)
xtset state_id year
```

### Single cross section (1982): nothing there

**R**

```r
mod82 <- lm(fm, Fatalities, subset = year == 1982)
summary(mod82)          # beertax ≈ +0.15, insignificant
```

**Stata**

```stata
reg frate beertax if year == 1982
```

### Pooled OLS: wrong sign, "significant"

**R**

```r
poolmod <- plm(fm, Fatalities, model = "pooling")
coeftest(poolmod)       # beertax ≈ +0.36, p < 0.001 — spurious!
```

**Stata**

```stata
reg frate beertax
```

### First differences

**R**

```r
fdmod <- plm(fm, Fatalities, model = "fd")
coeftest(fdmod)
```

**Stata**

```stata
reg d.frate d.beertax, nocons
```

*(Note: Stata's `d.` operator requires `xtset` first. `nocons` matches the
pure FD model with no drift; include a constant if you want to allow a common
time trend.)*

### LSDV: explicit state dummies

**R**

```r
lsdv <- lm(frate ~ beertax + state, Fatalities)
coeftest(lsdv)["beertax", ]   # ≈ −0.66, significant, sign flipped
```

**Stata**

```stata
reg frate beertax i.state_id
```

### Fixed effects (within estimator) — same β, no dummies

**R**

```r
femod <- plm(fm, Fatalities, model = "within")
coeftest(femod)               # identical beertax coefficient to LSDV
```

**Stata**

```stata
xtreg frate beertax, fe
```

---

## Command mapping cheat sheet

| Concept | R (`plm`) | Stata |
|---|---|---|
| Declare panel | `pdata.frame(df, index = c("state", "year"))` | `xtset state_id year` |
| Panel dimensions | `pdim(pdf)` | `xtdes` |
| Pooled OLS | `plm(..., model = "pooling")` | `reg y x` |
| First differences | `plm(..., model = "fd")` | `reg d.y d.x` |
| LSDV | `lm(y ~ x + factor(id))` | `reg y x i.id` |
| Within / FE | `plm(..., model = "within")` | `xtreg y x, fe` |
| Extract fixed effects | `fixef(femod)` | `predict eta, u` |

**Gotchas when comparing output across the two:**

- `xtreg, fe` reports an intercept (the average of the fixed effects);
  `plm(model = "within")` reports none. Slopes are identical.
- Stata's `xtreg, fe` R² "within" corresponds to the R² that `summary()`
  reports for a `plm` within model.
- Default standard errors in both are classical (non-robust). Robust and
  clustered SEs are Chapter 5 territory.

---

## Self-check questions

1. What assumption about the unobserved heterogeneity makes FD, LSDV, and FE
   valid? What kind of omitted variable would they *fail* to fix?
2. Why are LSDV and the within estimator numerically identical for β?
3. In the Fatalities example, tell the economic story for why pooled OLS gets
   the sign wrong.
4. Why can't a fixed effects model estimate the effect of a time-invariant
   regressor?
5. With T = 2, what is the relationship between the FD and FE estimators?

*(Answers to work out yourself first — the payoff of active recall.)*
