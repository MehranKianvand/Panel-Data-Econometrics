# Panel Data Econometrics: R & Stata Side by Side

Study notes on panel data econometrics, with every method implemented in both
**R** (`plm` and friends) and **Stata** (`xt` commands). Written while working
through Croissant & Millo, *Panel Data Econometrics with R* (Wiley, 2019),
with all explanations and code my own.

## Why this repo

Most panel data resources pick one language. In practice, applied economists
move between R and Stata constantly — replication packages, coauthors, and
journals differ in what they expect. These notes map each concept to its
implementation in both, side by side.

## Contents

| Chapter | Topic | Status |
|---|---|---|
| [01](chapters/01-introduction.md) | Introduction: unobserved heterogeneity, FD, LSDV, fixed effects | ✅ |
| 02 | The error component model: FE, RE, GLS | 🔜 |
| 03 | Advanced error components: two-way, nested, unbalanced | 🔜 |
| 04 | Testing: F tests, Hausman, LM tests | 🔜 |
| 05 | Robust inference: clustered and robust SEs | 🔜 |
| 06 | Endogeneity: IV, Hausman-Taylor | 🔜 |
| 07 | Dynamic panels: GMM, Arellano-Bond | 🔜 |
| 08 | Panel time series: unit roots, cointegration | 🔜 |
| 09 | Limited dependent variables: panel logit/probit, count data | 🔜 |
| 10 | Spatial panels | 🔜 |

## Software

- **R** ≥ 4.0 with `plm`, `AER`, `lmtest`
- **Stata** ≥ 15 (core `xt` commands; some later chapters use community
  packages such as `xtabond2` and `xsmle`, noted where relevant)

## Quick Rosetta Stone

| Task | R | Stata |
|---|---|---|
| Declare panel structure | `pdata.frame(df, index = c("id", "year"))` | `xtset id year` |
| Pooled OLS | `plm(y ~ x, data, model = "pooling")` | `reg y x` |
| Fixed effects (within) | `plm(y ~ x, data, model = "within")` | `xtreg y x, fe` |
| Random effects | `plm(y ~ x, data, model = "random")` | `xtreg y x, re` |
| First differences | `plm(y ~ x, data, model = "fd")` | `reg d.y d.x, nocons` |
