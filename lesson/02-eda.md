# Lesson 2 — Data Literacy & Exploratory Data Analysis (EDA)

:::{admonition} Learning goals
:class: tip
By the end of Lesson 2, you should be able to:
1. Identify common **data types** (numeric, categorical, datetime) and typical data quality issues.
2. Produce and interpret core **descriptive statistics** (mean, median, SD, IQR).
3. Use EDA to answer: “**What’s going on in the data?**” before modeling.
4. Create a small set of clear plots and write a short **data story** for a business audience.
:::

## Why this matters (motivation)

Most mistakes in analytics happen **before** modeling:
- confusing data types (e.g., numbers stored as strings),
- ignoring missingness,
- trusting outliers without checking,
- using the wrong chart and telling the wrong story.

EDA is your “first conversation” with the data.

:::{admonition} Reality check
:class: note
If you skip EDA, you often end up fitting models to artifacts: missing data patterns, coding errors, or outliers.
:::

---

## The EDA mindset: what questions are we asking?

:::{admonition} Key idea
:class: important
EDA is not just “making charts.” It is a structured way to answer:
1. **What is the unit of observation?** (customer? transaction? day?)
2. **What do variables mean in practice?** (how measured? any caveats?)
3. **What is typical vs unusual?** (center and spread)
4. **Are there groups?** (segments, time periods, regions)
5. **What relationships look plausible?** (before causal claims)
:::

### A simple EDA checklist (what we do every time)
1. **Preview**: rows, columns, data types  
2. **Validate**: missing values, duplicates, impossible values  
3. **Summarize**: distributions (center + spread)  
4. **Compare**: by group (category, time, segment)  
5. **Visualize**: choose the right chart for the question  
6. **Write**: 3–5 plain-language insights + 1 caveat

---

## Data literacy essentials (types and pitfalls)

### Data types that matter
- **Numeric**: revenue, price, age
- **Categorical**: region, product category, plan type
- **Datetime**: purchase date, signup date
- **Identifiers**: customer_id (not a “number” you average)

:::{admonition} Common pitfall
:class: warning
Treating IDs as numeric features (e.g., averaging customer_id) is meaningless and can break models.
:::

### Missing values: what they *might* mean
Missingness can be:
- **random** (e.g., occasional logging failures), or
- **systematic** (e.g., income missing more for high-income respondents).

:::{admonition} Key idea
:class: important
Before choosing a “fix” for missing values, ask: *Why is it missing?*
A quick missingness table by group often reveals the story.
:::

---

## Descriptive statistics that students actually use

:::{admonition} Key idea
:class: important
Use **mean** when distributions are roughly symmetric; use **median/IQR** when there are outliers or skew.
:::

### Core summary numbers
- **Mean**: average level
- **Median**: typical value (robust to outliers)
- **Standard deviation (SD)**: overall spread
- **Interquartile range (IQR)**: spread of the middle 50%

### What to report (rule of thumb)
- If the histogram looks symmetric: **mean ± SD**
- If it looks skewed: **median + IQR**

---

## Visualization as a decision tool (not decoration)

:::{admonition} Key idea
:class: important
A good chart answers a specific question.
A great chart makes the conclusion obvious without overselling certainty.
:::

### Quick chart chooser (practical)
- Compare categories → **bar chart** (sorted)
- Trend over time → **line chart**
- Relationship between two numeric variables → **scatter plot**
- Distribution → **histogram** / **boxplot**
- Two dimensions (category × category) → **heatmap**

:::{admonition} Common pitfall
:class: warning
A chart can be “technically correct” but still misleading due to:
- truncated axes,
- too many categories,
- poor aggregation (mixing units),
- hiding uncertainty.
:::

---

## Mini case: “Sales and marketing” dataset (EDA story)

**Question:** “Which product categories grew, and is growth associated with marketing spend?”

EDA steps:
1. Check data types (date as datetime, spend as numeric)
2. Summarize missing values (overall + by category)
3. Plot distribution of sales (is it skewed?)
4. Plot sales over time (overall + by category)
5. Scatter: sales vs marketing (colored by category)
6. Write 3 insights + 1 caveat

:::{admonition} Example insights (what ‘good’ looks like)
:class: note
- “Category A shows steady growth after Q2, while Category C declines.”
- “Marketing spend correlates with sales within categories, but the relationship differs by category.”
- “Sales are highly skewed: a small number of transactions contribute a large share of revenue.”
Caveat: “Missing marketing data is concentrated in one region, which may bias comparisons.”
:::

---

## Mini-lab (Google Colab)

:::{admonition} Colab link
:class: tip
Replace this with your real link:

- Week 2 notebook (EDA): https://colab.research.google.com/drive/PASTE_NOTEBOOK_ID
:::

**In-class tasks (checkpoints)**
1. Print data types and basic shape
2. Create a missingness summary table
3. Produce: (i) histogram/boxplot, (ii) line chart, (iii) bar chart by category
4. Write **3 insights + 1 caveat** in markdown inside the notebook

**Submission**
- Upload the Colab link (view permission) **or** export to PDF.

---

## AI check (responsible use for EDA)

:::{admonition} AI check
:class: caution
AI can help you brainstorm EDA steps and plot types, but you must:
1. Verify plots and calculations by running the notebook.
2. Check for “confident but wrong” interpretations (especially causal language).
3. Record prompts and edits in your prompt/workflow log.
:::

**Good prompt examples**
- “Suggest 5 EDA checks for a dataset of customer transactions with dates, categories, and revenue.”
- “Given these columns, what plots best answer ‘which category is growing’?”

**Bad prompt example**
- “Write my EDA conclusions for me” (without your own verification and interpretation)

---

## Review questions (quiz / reflection)

1. When would you report **median and IQR** instead of mean and SD?
2. Give one example of **systematic missingness** in a business dataset.
3. Which chart would you choose to show: (i) trend, (ii) distribution, (iii) group comparison—and why?

:::{admonition} Reflection prompt
:class: note
In ~150 words: Describe one dataset you might analyze (real or imagined). What is the unit of observation, and what are two EDA questions you would ask first?
:::