<div align="center">

# 📊 Observable vs. Unobservable Variables

### *Fundamental Concepts in Panel Data Econometrics*

<img src="https://img.shields.io/badge/Panel%20Data-Econometrics-00599C?style=for-the-badge">
<img src="https://img.shields.io/badge/R-plm-276DC3?style=for-the-badge&logo=r">
<img src="https://img.shields.io/badge/Stata-Panel%20Models-1F5AA6?style=for-the-badge">

</div>

---

> [!NOTE]
>
> **One of the primary motivations for panel data econometrics is to control for variables that influence the outcome but cannot be directly observed.**

---

# 📖 Introduction

In empirical research, we seek to understand how different factors influence an outcome.

Typical research questions include:

- Does education increase wages?
- Does work experience improve productivity?
- Does firm reputation increase employee retention?

To answer these questions, we estimate econometric models using available data.

Unfortunately, **not every relevant variable can be observed**. This distinction between **observable** and **unobservable** variables is one of the fundamental motivations for panel data econometrics.

---

# 👀 Observable Variables

Observable variables are characteristics that can be measured and included directly in a dataset.

<table>

<tr>
<th width="60%">Variable</th>
<th>Observable?</th>
</tr>

<tr>
<td>Wage</td>
<td>✅ Yes</td>
</tr>

<tr>
<td>Age</td>
<td>✅ Yes</td>
</tr>

<tr>
<td>Years of Education</td>
<td>✅ Yes</td>
</tr>

<tr>
<td>Firm Size</td>
<td>✅ Yes</td>
</tr>

<tr>
<td>Work Experience</td>
<td>✅ Yes</td>
</tr>

<tr>
<td>Number of Promotions</td>
<td>✅ Yes</td>
</tr>

</table>

Because these variables are observed, they can be included directly in a regression model.

$$
\text{Wage}
=
\beta_0
+
\beta_1\text{Education}
+
\beta_2\text{Experience}
+
\varepsilon
$$

---

# 🔒 Unobservable Variables

Unobservable variables influence the dependent variable but cannot be measured or are unavailable in the dataset.

<table>

<tr>
<th width="60%">Variable</th>
<th>Observable?</th>
</tr>

<tr>
<td>Ability</td>
<td>❌ No</td>
</tr>

<tr>
<td>Talent</td>
<td>❌ No</td>
</tr>

<tr>
<td>Motivation</td>
<td>❌ No</td>
</tr>

<tr>
<td>Ambition</td>
<td>❌ No</td>
</tr>

<tr>
<td>Personality</td>
<td>❌ No</td>
</tr>

<tr>
<td>Leadership Skills</td>
<td>❌ No</td>
</tr>

<tr>
<td>Firm Culture</td>
<td>❌ Usually No</td>
</tr>

<tr>
<td>Management Quality</td>
<td>❌ Often No</td>
</tr>

</table>

Although these variables cannot be directly measured, they often have a substantial influence on the outcome.

---

# ⚠️ Why Are Unobservable Variables a Problem?

Suppose the true wage equation is

$$
\text{Wage}
=
\beta_0
+
\beta_1\text{Education}
+
\beta_2\text{Ability}
+
u
$$

Unfortunately,

**Ability** cannot be observed.

Therefore, researchers estimate

$$
\text{Wage}
=
\beta_0
+
\beta_1\text{Education}
+
\varepsilon
$$

If more able individuals also obtain more education,

then

$$
Cov(\text{Education},\text{Ability})\neq0
$$

The estimated coefficient of education now captures

- the true effect of education **plus**
- part of the effect of ability.

This phenomenon is called **Omitted Variable Bias (OVB).**

---

# 📊 A Simple Example

<table>

<tr>
<th>Worker</th>
<th>Education</th>
<th>Ability</th>
<th>Wage</th>
</tr>

<tr>
<td>Alice</td>
<td>16</td>
<td>High</td>
<td>High</td>
</tr>

<tr>
<td>Bob</td>
<td>16</td>
<td>Low</td>
<td>Medium</td>
</tr>

<tr>
<td>Carol</td>
<td>12</td>
<td>Medium</td>
<td>Medium</td>
</tr>

</table>

Suppose ability cannot be observed.

A regression using only education would incorrectly attribute part of the wage differences to education rather than ability.

---

# 📈 Why Panel Data Help

Panel data observe the **same individuals repeatedly over time.**

Instead of estimating

$$
y_i=\beta x_i+\varepsilon_i
$$

panel data models estimate

$$
y_{it}
=
\alpha_i
+
\beta x_{it}
+
u_{it}
$$

where

- **i** = individual
- **t** = time
- **αᵢ** = time-invariant unobservable characteristics

Examples of what αᵢ may contain include

- Ability
- Intelligence
- Personality
- Family Background
- Motivation
- Permanent Work Ethic

---

# 💡 The Key Idea of Fixed Effects

The Fixed Effects estimator removes

$$
\alpha_i
$$

by comparing **each individual with themselves over time.**

Instead of asking

> **Why does Alice earn more than Bob?**

it asks

> **How did Alice's wage change after gaining more experience?**

Because Alice's ability remains constant,

it disappears from the estimation.

Consequently, Fixed Effects controls for all **time-invariant unobservable characteristics.**

---

# 🔄 Observable vs. Unobservable Variables

<table>

<tr>
<th>Feature</th>
<th>Observable</th>
<th>Unobservable</th>
</tr>

<tr>
<td>Can be measured</td>
<td>✅</td>
<td>❌</td>
</tr>

<tr>
<td>Included directly in regression</td>
<td>✅</td>
<td>❌</td>
</tr>

<tr>
<td>Available in dataset</td>
<td>✅</td>
<td>❌</td>
</tr>

<tr>
<td>May cause omitted variable bias</td>
<td>—</td>
<td>✅</td>
</tr>

<tr>
<td>Controlled by Fixed Effects (if time invariant)</td>
<td>—</td>
<td>✅</td>
</tr>

</table>

---

# ✅ Key Takeaways

> [!IMPORTANT]
>
> - Observable variables can be measured and included directly in econometric models.
> - Unobservable variables cannot be measured but may strongly influence the outcome.
> - Ignoring relevant unobservable variables leads to **omitted variable bias**.
> - Panel data methods, especially the **Fixed Effects estimator**, are designed to eliminate the influence of **time-invariant unobservable characteristics**.
> - This is one of the main reasons why panel data are preferred over purely cross-sectional data.

---

# 📝 Summary

Understanding the distinction between **observable** and **unobservable** variables is fundamental to panel data econometrics.

The primary objective of many panel estimators is not simply to improve estimation efficiency, but to obtain **consistent estimates** by controlling for **unobserved heterogeneity** that would otherwise bias the estimated relationships.

---

<div align="center">

### ⬅️ Previous | 🏠 Home | Next ➡️

| Home | Next Topic |
|:----:|:----------:|
| [README](../README.md) | [Consistency of Estimators](02-Consistency.md) |

</div>
