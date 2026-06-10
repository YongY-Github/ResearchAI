# Lesson 6 — Correlation, Simple & Multiple Regression (interpretation for business/economics)

:::{admonition} Learning goals
:class: tip
By the end of Lesson 6, you should be able to:
1. Explain what correlation and regression are doing in plain language (summarizing relationships in data).
2. Recognize where regression fits in the course: **supervised learning** (predicting/estimating an outcome) vs **unsupervised learning** (segmentation without an outcome).
3. Construct analysis variables from raw columns:
   - `income_pc = gdp_pc / 1000`
   - `d_rate = divorce_rate / marriage_rate`
4. Fit and interpret **simple regression** and **multiple regression** in Python (Google Colab) using `statsmodels` (`import statsmodels.api as sm`).
5. Interpret coefficients carefully, including how the meaning can change when you add a control variable.
6. Understand key limitations (intuition): correlation vs causation, omitted variables, reverse causality, and extrapolation.
:::

## Why this matters

Regression is one of the most widely used tools in business and economics because it helps quantify relationships:

- Are countries with higher income associated with higher (or lower) divorce outcomes?
- Are higher prices associated with lower demand?
- Which factors are correlated with churn or customer satisfaction?

But regression is easy to misuse—especially when we confuse **association** with **causation**.

:::{admonition} Reality check
:class: note
A regression coefficient is not automatically a “causal effect.”
It is a numerical summary of a relationship **in your data**, under your model and measurement choices.
:::

---

## Where regression sits in the AI/ML/DS map

:::{admonition} Key idea
:class: important
- **Supervised learning:** we have an outcome $Y$ (e.g., divorce ratio) and we model $Y$ using predictors $X$.
  - Regression is supervised learning.
- **Unsupervised learning:** we do not have $Y$; we look for structure in $X$ (clustering/PCA).
  - That comes later (Lesson 8).
:::

---

## The regression mindset: from question to model

:::{admonition} Key idea
:class: important
Before running correlation/regression, be clear about:
1. **Outcome** $Y$: what you want to explain or predict
2. **Predictor(s)** $X$: what might be related to $Y$
3. **Unit of observation**: customer, firm-year, country-year, etc.
4. **Interpretation goal**: prediction, description, or (careful) causal language
:::

### Today’s running example (new dataset)

We use:
- [divorce-raw-1992.csv](../files/divorce_raw.csv) — divorce data

- Unit: **country (2019 cross-section)**
- Outcome $Y$: divorce–marriage ratio  
  `d_rate = divorce_rate / marriage_rate`
- Main predictor $X$: income (rescaled GDP per capita)  
  `income_pc = gdp_pc / 1000`
- Control candidate: GDP growth (`gdp_gr`)

---

## Step 0: Start with a picture (scatter plot)

Before any equation, draw the relationship.

- If the scatter is basically a cloud: the relationship may be weak or non-linear.
- If there is a visible upward/downward pattern: regression helps summarize it.

:::{admonition} Common pitfall
:class: warning
Do not interpret a regression coefficient outside the range of your observed $X$ values (extrapolation).
A “line” may not stay true beyond the data.
:::

---

## Step 1: Correlation (a warm-up)

Correlation is a standardized measure of linear association.

- It ranges from $-1$ to $+1$.
- It is symmetric: $\mathrm{corr}(X,Y)=\mathrm{corr}(Y,X)$.
- It does **not** tell you “how much $Y$ changes when $X$ changes” in units.

:::{admonition} Key idea
:class: important
Correlation is a **unit-free** summary.  
Regression gives a relationship **in units** (e.g., change in divorce ratio per $1{,}000$ dollars of GDP per capita).
:::

---

## Step 2: Simple regression (one predictor)

A simple regression estimates a line:

$Y = \beta_0 + \beta_1 X + \varepsilon$

- $\beta_1$ tells you how $Y$ changes (on average) with a one-unit change in $X$.
- $\varepsilon$ captures everything else not in the model.

### Our example (simple regression)
- $Y$: `d_rate`
- $X$: `income_pc`

Interpretation template:
> “A one-unit increase in `income_pc` (i.e., $1{,}000$ dollars of GDP per capita) is associated with a $\beta_1$ change in `d_rate`, on average, in this sample.”

---

## Step 3: Multiple regression (adding a control)

Multiple regression adds additional predictors:

$Y = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \varepsilon$

Now $\beta_1$ is interpreted as the association between $Y$ and $X_1$ **holding other included variables constant**.

### Why add controls?
To reduce confounding (informally):

- If both income level and macroeconomic conditions are related to divorce/marriage patterns, a simple regression may mix these relationships.

Today we add:
- `gdp_gr` (GDP growth) as a simple control.

:::{admonition} Reality check
:class: note
Controls can help, but they do not automatically create causality.
If important confounders are still missing, omitted variable bias may remain.
:::

---

## How to read regression output (what we focus on)

1) **Coefficients**
- sign (positive/negative association)
- magnitude (how much change in $Y$ per unit of $X$)
- units matter

2) **Uncertainty (standard errors / confidence intervals)**
- How precise is the estimate?

3) **Fit (R-squared)**
- How much of the variation in $Y$ is explained (in-sample)?
- Do not treat $R^2$ as “truth” or “usefulness” by itself.

---

## Regression and causality (a careful note)

Regression describes a relationship. Causal interpretation requires stronger assumptions/design.

Common threats:
- **Omitted variables**
- **Reverse causality**
- **Measurement error**
- **Selection bias**

:::{admonition} Practical rule
:class: tip
When writing conclusions, default to “is associated with” unless you have a clear causal design.
:::

---

## Mini-lab (Google Colab)

:::{admonition} Colab link
:class: tip
Here's the Lesson notebook:

- https://colab.research.google.com/drive/1VE5mAD1K9LCxJjp-EzPS0EXZz18w3OM_?usp=sharing
:::

### In-class checkpoints
1. Load `divorce_raw.csv` and filter to **year = 2019**.
2. Create:
   - `income_pc = gdp_pc / 1000`
   - `d_rate = divorce_rate / marriage_rate * 1000`
3. Make a scatter plot: `d_rate` vs `income_pc`.
4. Compute correlation between `d_rate` and `income_pc`.
5. Fit **simple regression**: `d_rate ~ income_pc` and interpret $\beta_1$.
6. Fit **multiple regression**: `d_rate ~ income_pc + gdp_gr` and interpret how $\beta_1$ changes (if it does).
7. Make one diagnostic plot (residuals vs fitted OR histogram of residuals).
8. Write a short “manager memo” (5–7 lines): headline + evidence + caveat.

### Submission (after class)
- Share the Colab link (view permission) or export to PDF.
- Include your memo + one caveat as Markdown.

---

## AI check (responsible use)

:::{admonition} AI check
:class: caution
AI can help with code scaffolding and explanation drafts, but you must:
1. Verify the regression specification and variables (units, missing values, filtering).
2. Avoid causal claims unless justified.
3. Document prompts and edits in your prompt/workflow log.
:::
