# Lesson 5 — Data Cleaning & Preprocessing (from raw to analysis-ready)

:::{admonition} Learning goals
:class: tip
By the end of Lesson 5, you should be able to:
1. Diagnose common data quality issues (missingness, duplicates, inconsistent categories, outliers, wrong data types).
2. Apply a clear, reproducible cleaning pipeline in Python (Google Colab).
3. Merge two datasets using appropriate keys and join types, and validate the merge (row counts, unmatched records, duplicates).
4. Create a small set of useful **features** (e.g., growth rates, flags, simple transformations).
5. Write a short **Cleaning Log** explaining what you changed (including merges) and why, and recognize when cleaning choices can introduce bias or distort comparisons.
:::

## Why this matters (motivation)

Most of the time in real analytics is spent **before modeling**:
- fixing inconsistent input formats,
- resolving category labels,
- handling missing values,
- and ensuring comparisons are meaningful.

Good cleaning is not “cosmetic.” It changes your results.

:::{admonition} Reality check
:class: note
A model trained on poorly cleaned data can look sophisticated while being fundamentally unreliable.
:::

---

## The cleaning mindset: "What would break trust?"

:::{admonition} Key idea
:class: important
Data cleaning is about **trustworthy measurement**.
Ask:
1. What does each variable mean in the real world?
2. What values are impossible or suspicious?
3. Is missingness random or systematic?
4. Will cleaning decisions change group comparisons?
:::

### A simple cleaning pipeline (the course standard)
1. **Type check**: numbers as numbers, dates as dates, categories as categories  
2. **Range check**: impossible values (negative sales, invalid ages, etc.)  
3. **Uniqueness check**: duplicates in IDs or key fields  
4. **Missingness check**: overall and by group (region/segment/time)  
5. **Consistency check**: category labels, units, and definitions  
6. **Document everything**: a short cleaning log

---

## Common cleaning problems (and practical fixes)

### 1) Data types and parsing
Examples:
- `date` stored as a string
- currency stored as `"1,200"` (string with commas)
- numeric column includes `"N/A"` or `"—"`

:::{admonition} Common pitfall
:class: warning
If numbers are stored as strings, operations may silently fail (sorting, comparisons, aggregations).
Always check `df.info()` and a few values.
:::

### 2) Missing values (what to do depends on why)
Missingness can be:
- **rare noise** (logging errors),
- **structural** (not applicable),
- **systematic** (missing more for a particular group).

:::{admonition} Key idea
:class: important
Before “filling” missing values, look at missingness by group:
- by region,
- by product category,
- by time period.
This often reveals whether missingness is random or systematic.
:::

**Practical options (in increasing strength):**
- leave missing values and be explicit about sample size,
- drop rows only if missingness is small and plausibly random,
- impute using simple rules (median, last observation, etc.) with justification,
- create a **missingness indicator** (a flag) when missingness itself is informative.

### 3) Duplicates and unit of observation
Always confirm the unit:
- customer-level?
- transaction-level?
- day-level?

Duplicates may be:
- exact duplicates (same row repeated),
- key duplicates (same `customer_id + date` repeated).

:::{admonition} Common pitfall
:class: warning
Duplicates can inflate totals and bias averages.
Always define keys and check whether they should be unique.
:::

### 4) Outliers (don’t delete automatically)
Outliers might be:
- true extreme behavior (high-value customers),
- measurement error,
- unit problems (e.g., 1,000 vs 1.000).

A good approach:
- flag outliers,
- inspect a small number of extreme cases,
- justify whether you keep, cap (winsorize), or exclude.

---

## Merging datasets (a core real-world skill)

In practice, “analysis-ready” data often requires combining multiple sources:
- customer profile + transactions
- sales + marketing spend
- macro indicators + outcomes
- (later) news text + market data

:::{admonition} Key idea
:class: important
A merge is only correct if the **keys** and the **unit of observation** are correct.
Before merging, answer:
1. What is one row? (customer? transaction? country-year?)
2. Which column(s) uniquely identify a row?
:::

### Join types (we keep this simple)
- **Left join** (recommended default): keep all rows from the main dataset and attach matching information from the second dataset.
- **Inner join**: keep only matched rows (risk: silently drops data).
- **Outer join**: keep all rows from both datasets (useful for diagnosing mismatches).

### Merge checks (required after every merge)
After merging, always check:
1. **Row count before vs after** (did it unexpectedly grow or shrink?)
2. **Unmatched records** (did you introduce missing values?)
3. **Duplicates created** (did a one-to-many merge happen by accident?)
4. **Key uniqueness still holds** (your merged unit of observation is still consistent)

:::{admonition} Common pitfall
:class: warning
Incorrect keys can cause:
- “data explosions” (one-to-many merge when you expected one-to-one), or
- silent data loss (inner join dropping many rows).
Always validate merges.
:::

### Minimal Python merge pattern (recommended)

# Example (safe default): left join + validation
merged = left.merge(right, on="customer_id", how="left", validate="one_to_one")

# Quick merge checks
print(left.shape, right.shape, merged.shape)
print(merged.isna().mean().sort_values(ascending=False).head(10))

---

## Feature engineering (simple and meaningful)

:::{admonition} Key idea
:class: important
Feature engineering means turning raw columns into variables that match your question.
Good features are:
- interpretable,
- stable,
- and aligned with business/econ logic.
:::

Examples:
- **growth rate**: `sales_growth = (sales_t - sales_{t-1}) / sales_{t-1}`
- **log transform** for skewed variables: `log_sales = log(1 + sales)`
- **flags**: `high_value_customer`, `promotion_period`, `missing_income_flag`
- **time features**: month/quarter, day-of-week (if relevant)

:::{admonition} Common pitfall
:class: warning
Do not engineer features that leak future information (e.g., using next month’s sales to predict this month’s churn).
:::

---

## Mini case: cleaning a “messy sales” dataset

**Scenario:** You have sales records with:
- inconsistent category labels (“BKK”, “Bangkok”, “Bangkok ”),
- dates stored as strings in mixed formats,
- missing marketing spend for some regions,
- extreme sales values.

**Goal:** Produce an analysis-ready dataset for regression and visualization later.

Deliverables from cleaning:
1. A cleaned `DataFrame` with correct types
2. A missingness summary (overall + by region/category)
3. A small outlier check
4. 2–3 engineered features (e.g., log_sales, growth, flags)
5. A short Cleaning Log

---

## Mini-lab (Google Colab)

:::{admonition} Colab link
:class: tip
Replace this with your real link:

- Week 5 notebook (Cleaning & preprocessing): https://colab.research.google.com/drive/PASTE_NOTEBOOK_ID
:::

**In-class checkpoints**
1. Run `df.info()` and identify at least **two** columns with incorrect types.
2. Produce a missingness table (overall and by one grouping variable).
3. Check duplicates using a defined key (e.g., `customer_id + date` or `store_id + date`).
4. **Merge exercise:** merge two datasets (or two tables) using a clearly stated key.
   - state your expected merge type (one-to-one? one-to-many?)
   - use a left join unless you have a reason not to
5. **Merge validation:** report
   - row counts before/after,
   - number of unmatched rows introduced,
   - whether duplicates were created.
6. Identify possible outliers and decide a rule (keep / flag / cap) with a brief justification.
7. Create at least **two** engineered features and show their distributions.

---

## AI check (responsible use for cleaning)

:::{admonition} AI check
:class: caution
AI can help propose cleaning steps, but you must:
1. Verify logic by checking small samples and summary stats before/after.
2. Avoid “blind imputation” suggested by AI without considering missingness patterns.
3. Record prompts and edits in your prompt/workflow log.
:::

**Good prompt examples**
- “Given these columns and common issues (mixed date formats, category typos), propose a cleaning checklist.”
- “Show pandas code to standardize category labels and parse dates safely.”
- “How can I summarize missingness by region and year?”

**Bad prompt example**
- “Clean my dataset and tell me the results” (without showing steps and checks)

---

## Review questions (quiz / reflection)

1. Why can dropping missing values change your conclusions?
2. Give one case where an outlier might be *real* and important (not an error).
3. What is the unit of observation in your dataset, and how does that affect duplicate checks?

:::{admonition} Reflection prompt
:class: note
In ~150 words: Describe one cleaning decision you made today (missing values, duplicates, outliers, or recoding).  
What was your rule, and what could go wrong if the rule is inappropriate?
:::