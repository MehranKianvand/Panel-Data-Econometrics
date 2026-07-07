<div align="center">

<h1>🧮 Methods for Eliminating Unobserved Components</h1>

<h3><i>The Foundation of Panel Data Econometrics</i></h3>

<p>

<img src="https://img.shields.io/badge/Panel%20Data-Econometrics-blue?style=for-the-badge">
<img src="https://img.shields.io/badge/Chapter-Introduction-success?style=for-the-badge">

</p>

</div>

---

<blockquote>

<b>Core Idea</b>

<br><br>

The primary objective of panel data econometrics is to eliminate or control for <b>unobserved heterogeneity</b>, which would otherwise bias the estimated relationship between explanatory variables and the dependent variable.

</blockquote>

---

<h2>📖 The General Panel Data Model</h2>

Suppose the true model is

<pre>

y_it = α_i + βx_it + u_it

</pre>

where

<table>

<tr>
<th>Notation</th>
<th>Description</th>
</tr>

<tr>
<td><b>y_it</b></td>
<td>Dependent variable</td>
</tr>

<tr>
<td><b>x_it</b></td>
<td>Observable explanatory variable</td>
</tr>

<tr>
<td><b>α_i</b></td>
<td>Unobserved individual effect</td>
</tr>

<tr>
<td><b>u_it</b></td>
<td>Idiosyncratic error term</td>
</tr>

</table>

Examples of <b>α_i</b>

- Ability
- Talent
- Intelligence
- Personality
- Firm culture
- Management quality

If these characteristics are correlated with <b>x</b>, OLS becomes biased.

---

<h1>1️⃣ First Difference Estimator</h1>

<h3>💡 Intuition</h3>

Compare each individual with themselves in the previous period.

Instead of comparing

> Alice versus Bob

we compare

> Alice today versus Alice yesterday.

<h3>Mathematics</h3>

Original model

<pre>

y_it = α_i + βx_it + u_it

</pre>

Previous period

<pre>

y_i,t−1 = α_i + βx_i,t−1 + u_i,t−1

</pre>

Subtract

<pre>

Δy_it = βΔx_it + Δu_it

</pre>

Notice

<pre>

α_i − α_i = 0

</pre>

The individual effect disappears.

---

<h3>Advantages</h3>

✅ Eliminates all time-invariant unobserved effects

✅ Very intuitive

---

<h3>Disadvantages</h3>

❌ Loses the first observation

❌ Can magnify measurement errors

---

<h1>2️⃣ Fixed Effects Estimator</h1>

<h3>💡 Intuition</h3>

Compare each individual with their own average instead of with other individuals.

Instead of asking

> Why does Alice earn more than Bob?

ask

> How does Alice differ from her own average wage?

---

<h3>Mathematics</h3>

Individual mean

<pre>

ȳ_i = α_i + βx̄_i + ū_i

</pre>

Subtract

<pre>

y_it − ȳ_i

=

β(x_it − x̄_i)

+

(u_it − ū_i)

</pre>

Again

<pre>

α_i − α_i = 0

</pre>

---

<h3>Advantages</h3>

✅ Uses all available periods

✅ Usually more efficient than First Difference

✅ Standard estimator in empirical economics

---

<h3>Disadvantages</h3>

❌ Time-invariant variables disappear

Examples

- Gender

- Ethnicity

- Country of birth

cannot be estimated.

---

<h1>3️⃣ Least Squares Dummy Variables (LSDV)</h1>

<h3>💡 Intuition</h3>

Instead of removing the individual effects,

estimate one intercept for every individual.

Example

<pre>

y

=

βx

+

δ₁D₁

+

δ₂D₂

+

δ₃D₃

+

u

</pre>

Each dummy represents one individual.

---

<h3>Advantages</h3>

✅ Very easy to understand

✅ Produces exactly the same slope estimates as Fixed Effects

---

<h3>Disadvantages</h3>

❌ Requires one dummy for every individual

Impractical for millions of observations.

---

<h1>4️⃣ Random Effects Estimator</h1>

<h3>💡 Intuition</h3>

Instead of removing α_i,

treat it as part of the error term.

Assume

<pre>

Cov(α_i,x_it)=0

</pre>

Then

<pre>

ε_it = α_i + u_it

</pre>

The model is estimated using Generalized Least Squares (GLS).

---

<h3>Advantages</h3>

✅ More efficient than Fixed Effects

✅ Estimates coefficients for time-invariant variables

---

<h3>Disadvantages</h3>

❌ If

<pre>

Cov(α_i,x_it) ≠ 0

</pre>

the estimator becomes inconsistent.

---

<h1>5️⃣ Instrumental Variables</h1>

<h3>💡 Intuition</h3>

Sometimes the problem is not only α_i.

An explanatory variable may also be endogenous.

Find another variable (an instrument)

that

- is correlated with x

- is not correlated with the error.

This isolates the exogenous variation in x.

---

<h3>Advantages</h3>

✅ Corrects endogeneity

---

<h3>Disadvantages</h3>

❌ Finding valid instruments is difficult.

---

<h1>6️⃣ Dynamic Panel Models (Arellano–Bond)</h1>

<h3>💡 Intuition</h3>

Suppose today's outcome depends on yesterday's outcome.

<pre>

y_it

=

ρy_i,t−1

+

βx_it

+

α_i

+

u_it

</pre>

The procedure

1. First-differences the model.
2. Uses lagged variables as instruments.

This removes α_i while addressing the endogeneity created by the lagged dependent variable.

---

<h2>📊 Comparison of Methods</h2>

<table>

<tr>

<th>Method</th>

<th>How α_i is handled</th>

<th>Time-Invariant Variables</th>

</tr>

<tr>

<td>First Difference</td>

<td>Subtract previous period</td>

<td>❌ No</td>

</tr>

<tr>

<td>Fixed Effects</td>

<td>Subtract individual mean</td>

<td>❌ No</td>

</tr>

<tr>

<td>LSDV</td>

<td>Estimate one dummy per individual</td>

<td>❌ No</td>

</tr>

<tr>

<td>Random Effects</td>

<td>Model α_i as random</td>

<td>✅ Yes</td>

</tr>

<tr>

<td>Instrumental Variables</td>

<td>Use external instruments</td>

<td>Depends on specification</td>

</tr>

<tr>

<td>Dynamic GMM</td>

<td>Difference + instruments</td>

<td>❌ Usually No</td>

</tr>

</table>

---

<h2>🎯 Which Method Should You Use?</h2>

<table>

<tr>

<th>Research Situation</th>

<th>Recommended Estimator</th>

</tr>

<tr>

<td>Baseline analysis</td>

<td>Pooled OLS</td>

</tr>

<tr>

<td>Unobserved heterogeneity</td>

<td>Fixed Effects</td>

</tr>

<tr>

<td>Year-to-year changes</td>

<td>First Difference</td>

</tr>

<tr>

<td>Time-invariant regressors are important</td>

<td>Random Effects</td>

</tr>

<tr>

<td>Endogenous regressors</td>

<td>Instrumental Variables</td>

</tr>

<tr>

<td>Lagged dependent variable</td>

<td>Dynamic Panel GMM</td>

</tr>

</table>

---

<h2>📝 Summary</h2>

Panel data estimators differ primarily in <b>how they deal with the unobserved individual effect (α_i)</b>.

<ul>

<li><b>First Difference</b> removes α_i by differencing consecutive observations.</li>

<li><b>Fixed Effects</b> removes α_i by subtracting the individual's average.</li>

<li><b>LSDV</b> estimates α_i explicitly using dummy variables.</li>

<li><b>Random Effects</b> treats α_i as a random component of the error term.</li>

<li><b>Instrumental Variables</b> solve endogeneity using valid instruments.</li>

<li><b>Dynamic GMM</b> combines differencing with instrumental variables to estimate dynamic panel models.</li>

</ul>

---

<div align="center">

<b>📚 Next Topic:</b> <i>Least Squares Dummy Variables (LSDV)</i>

</div>
