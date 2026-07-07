<div align="center">

<h1>📊 Observable vs. Unobservable Variables</h1>

<h3><i>Fundamental Concepts in Panel Data Econometrics</i></h3>

<p>

<img src="https://img.shields.io/badge/Panel%20Data-Econometrics-blue?style=for-the-badge">
<img src="https://img.shields.io/badge/R-plm-276DC3?style=for-the-badge&logo=r">
<img src="https://img.shields.io/badge/Stata-Panel%20Models-1F5AA6?style=for-the-badge">

</p>

</div>

<hr>

<blockquote>

<b>Key Idea</b>

<br><br>

One of the primary motivations for panel data econometrics is to deal with variables that influence the outcome but cannot be directly observed.

</blockquote>

<hr>

<h2>📖 Introduction</h2>

<p>

In empirical research, we aim to understand how one or more variables affect an outcome.

Typical research questions include

</p>

<ul>

<li>Does education increase wages?</li>

<li>Does experience improve productivity?</li>

<li>Does a firm's reputation increase employee retention?</li>

</ul>

<p>

To answer these questions, researchers estimate econometric models using observable data.

However, not every important factor can be measured.

This distinction between <b>observable</b> and <b>unobservable</b> variables lies at the heart of modern econometrics.

</p>

<hr>

<h2>👀 Observable Variables</h2>

<p>

Observable variables are characteristics that can be measured and included directly in a dataset.

</p>

<table>

<tr>
<th>Variable</th>
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

<p>

Because these variables are observed, they can be included directly in a regression model.

</p>

<pre>

Wage = β₀ + β₁ Education + β₂ Experience + ε

</pre>

<hr>

<h2>🔒 Unobservable Variables</h2>

<p>

Unobservable variables influence the dependent variable but cannot be measured or are unavailable in the dataset.

</p>

<table>

<tr>
<th>Variable</th>
<th>Observable?</th>
</tr>

<tr><td>Ability</td><td>❌ No</td></tr>
<tr><td>Talent</td><td>❌ No</td></tr>
<tr><td>Motivation</td><td>❌ No</td></tr>
<tr><td>Ambition</td><td>❌ No</td></tr>
<tr><td>Personality</td><td>❌ No</td></tr>
<tr><td>Leadership Skills</td><td>❌ No</td></tr>
<tr><td>Firm Culture</td><td>❌ Usually No</td></tr>
<tr><td>Management Quality</td><td>❌ Often No</td></tr>

</table>

<p>

Although these variables cannot be directly measured, they often have a substantial influence on the outcome.

</p>

<hr>

<h2>⚠️ Why Are Unobservable Variables a Problem?</h2>

<p>

Suppose the true wage equation is

</p>

<pre>

Wage = β₀ + β₁ Education + β₂ Ability + u

</pre>

<p>

Unfortunately, <b>Ability</b> cannot be observed.

Therefore, researchers estimate

</p>

<pre>

Wage = β₀ + β₁ Education + ε

</pre>

<p>

If more able individuals also obtain more education, education and ability become correlated.

Consequently,

</p>

<ul>

<li>part of the effect of ability is mistakenly attributed to education;</li>

<li>the estimated effect of education becomes biased;</li>

<li>increasing the sample size does not solve the problem.</li>

</ul>

<p>

This phenomenon is known as <b>omitted variable bias</b>.

</p>

<hr>

<h2>📊 A Simple Example</h2>

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

<p>

Suppose ability cannot be observed.

A regression using only education would incorrectly attribute part of the wage differences to education rather than ability.

</p>

<hr>

<h2>📈 Why Panel Data Help</h2>

<p>

Panel data observe the same individuals repeatedly over time.

Instead of estimating

</p>

<pre>

yᵢ = βxᵢ + εᵢ

</pre>

<p>

panel data estimate

</p>

<pre>

yᵢₜ = αᵢ + βxᵢₜ + uᵢₜ

</pre>

<p>

where

</p>

<ul>

<li><b>i</b> = individual</li>

<li><b>t</b> = time</li>

<li><b>αᵢ</b> = time-invariant unobservable characteristics</li>

</ul>

<p>

Examples include

</p>

<ul>

<li>Ability</li>
<li>Intelligence</li>
<li>Personality</li>
<li>Family Background</li>
<li>Motivation</li>
<li>Permanent Work Ethic</li>

</ul>



<h2>🔄 Observable vs. Unobservable Variables</h2>

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

<td>Controlled by Fixed Effects</td>
<td>—</td>
<td>✅</td>

</tr>

</table>

<hr>

<h2>✅ Key Takeaways</h2>

<ul>

<li>Observable variables can be measured and included directly in econometric models.</li>

<li>Unobservable variables cannot be measured but may strongly influence the outcome.</li>

<li>Ignoring relevant unobservable variables leads to omitted variable bias.</li>

<li>Panel data methods, especially the Fixed Effects estimator, are designed to eliminate time-invariant unobservable characteristics.</li>

<li>This is one of the primary reasons why panel data are preferred over purely cross-sectional data.</li>

</ul>

<hr>

<h2>📝 Summary</h2>

<p>

Understanding the distinction between observable and unobservable variables is fundamental to panel data econometrics.

The main objective of panel estimators is not simply to improve efficiency but to obtain <b>consistent estimates</b> by controlling for <b>unobserved heterogeneity</b>.

</p>

<hr>

