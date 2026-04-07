# Lesson 6 — Simple & Multiple Regression (interpretation for business/economics)

:::{admonition} Learning goals
:class: tip
By the end of Lesson 6, you should be able to:
1. Explain what a regression is doing in plain language (best-fitting line/plane for prediction and description).
2. Fit and interpret **simple regression** and **multiple regression** in Python (Google Colab).
3. Interpret coefficients, including how the meaning changes when you add control variables.
4. Understand (intuitively) key limitations: correlation vs causation, omitted variables, reverse causality, and extrapolation.
5. Write a short “manager memo” conclusion: headline result + evidence + caveat.
:::

## Why this matters (motivation)

Regression is one of the most widely used tools in business and economics because it helps quantify relationships:
- How is sales associated with marketing spend?
- Are higher prices associated with lower demand?
- Which factors are correlated with churn or customer satisfaction?

But regression is also easy to misuse, especially when people confuse association with causation.

:::{admonition} Reality check
:class: note
A regression coefficient is not automatically a “causal effect.”
It is a numerical summary of a relationship *in your data* under your model assumptions.
:::

---

## The regression mindset: from question to model

:::{admonition} Key idea
:class: important
Before running regression, be clear about:
1. **Outcome** ($Y$): what you want to explain or predict
2. **Predictor(s)** ($X$): what might be related to $Y$
3. **Unit of observation**: customer, transaction, month, firm-year, etc.
4. **Interpretation goal**: prediction, description, or (careful) causal language
:::

### Today’s scope
We focus on:
- fitting regressions,
- interpreting outputs,
- and communicating limitations.

We will **not** claim causality unless the design supports it.

---

## Simple regression (one predictor)

:::{admonition} Key idea
:class: important
A simple regression estimates a line:
\[
Y = \beta_0 + \beta_1 X + \varepsilon
\]
- $\beta_1$ tells you how $Y$ changes (on average) with a one-unit change in $X$.
- $\varepsilon$ captures everything else not in the model.
:::

### Example
$Y$ = monthly sales  
$X$ = marketing spend

Interpretation: if $\beta_1 = 2.5$, then an extra unit of spend is associated with +2.5 units of sales (on average), **in this dataset**.

:::{admonition} Common pitfall
:class: warning
Do not interpret $\beta_1$ outside the range of your observed $X$ values (extrapolation).
A “line” may not stay true beyond the data.
:::

---

## Multiple regression (controls)

:::{admonition} Key idea
:class: important
Multiple regression adds additional predictors:
\[
Y = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \cdots + \varepsilon
\]
Now, $\beta_1$ is interpreted as the relationship between $Y$ and $X_1$ **holding the other included variables constant**.
:::

### Why add controls?
To reduce confounding (informally):
- If both marketing spend and season affect sales, a simple regression might mix the two effects.

Example:
- $Y$ = sales  
- $X_1$ = marketing spend  
- $X_2$ = season indicator (e.g., Q4 = 1)  
- $X_3$ = price  

Now $\beta_1$ is the association between sales and marketing, **after accounting for season and price**.

:::{admonition} Reality check
:class: note
Controls can help, but they do not automatically create causality.
If important confounders are still missing, omitted variable bias may remain.
:::

---

## How to read regression output (what we focus on)

### 1) Coefficients
- sign: positive/negative association
- magnitude: “how much change in $Y$ per unit of $X$”
- units matter (e.g., dollars vs thousands)

### 2) Uncertainty (standard errors / confidence intervals)
We care about whether the estimate is precise enough to be actionable.

### 3) Fit (R-squared)
- R² tells you how much variation in $Y$ the model explains **in-sample**.
- A high R² does not guarantee good decision-making, and a low R² does not mean the model is useless.

:::{admonition} Common pitfall
:class: warning
Students often chase high R². In many business/econ contexts, the goal is **interpretation and decision support**, not perfect prediction.
:::

---

## Regression and causality (a careful note)

Regression describes a relationship. Causal interpretation requires stronger assumptions/design.

Common threats:
- **Omitted variables**: a third factor affects both X and Y
- **Reverse causality**: Y influences X (e.g., firms spend more on marketing when sales rise)
- **Measurement error**: X or Y is noisy or mismeasured
- **Selection bias**: data is not representative

:::{admonition} Practical rule
:class: tip
When writing conclusions, default to “is associated with” unless you have a clear causal design.
:::

---

## Mini case: sales, marketing, and seasonality

**Question:** Is marketing spend associated with sales after accounting for seasonality and price?

Steps:
1. EDA reminder: plot sales over time and by category/region
2. Fit simple regression: sales ~ marketing
3. Fit multiple regression: sales ~ marketing + price + season + category/region dummies (as appropriate)
4. Compare coefficient on marketing and discuss how the interpretation changes
5. Write a short manager memo with one caveat

---

## Mini-lab (Google Colab)

:::{admonition} Colab link
:class: tip
Replace this with your real link:

- Week 6 notebook (Regression): https://colab.research.google.com/drive/PASTE_NOTEBOOK_ID
:::

**In-class checkpoints**
1. Fit a **simple regression** and interpret $\beta_1$ in units.
2. Fit a **multiple regression** that adds at least 2 controls.
3. Compare the coefficient on your main variable (e.g., marketing) across the two models:
   - Did it change sign or magnitude?
   - Why might that happen?
4. Create one diagnostic plot (residuals vs fitted OR histogram of residuals).
5. Write a short “manager memo” (5–7 lines) in the notebook.

**Submission (after class)**
- Share the Colab link (view permission) or export to PDF.
- Include a short memo + one caveat as Markdown.

---

## AI check (responsible use for regression)

:::{admonition} AI check
:class: caution
AI can help with code scaffolding and explanation drafts, but you must:
1. Verify the regression specification and variables (units, missing values, filtering).
2. Avoid causal claims unless justified.
3. Document prompts and edits in your prompt/workflow log.
:::

**Good prompt examples**
- “Generate statsmodels code to run OLS of sales on marketing, price, and a season dummy, with a clear summary output.”
- “How should I interpret the coefficient on marketing when price and season are included?”
- “Suggest one diagnostic plot and explain what it checks.”

**Bad prompt example**
- “Write my conclusion that marketing causes sales to rise” (without a causal design)

---

## Review questions (quiz / reflection)

1. What changes about the interpretation of $\beta_1$ when you move from simple to multiple regression?
2. Give one example of an omitted variable that could bias your regression.
3. Why is “high R²” not the same as “good model”?

:::{admonition} Reflection prompt
:class: note
In ~150 words: Compare your simple and multiple regression results.  
Which coefficient changed the most, and what is one plausible explanation (in words) for that change?
:::