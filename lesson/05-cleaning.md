# Lesson 5 — Data Cleaning, Preprocessing, and Merging Datasets
*(from raw to analysis-ready)*

:::{admonition} Learning goals
:class: tip
By the end of Lesson 5, you should be able to:
1. Diagnose common data quality issues (missingness, duplicates, inconsistent categories, outliers, wrong data types).
2. Apply a clear, reproducible cleaning pipeline in Python (Google Colab).
3. Merge two datasets using appropriate keys and join types, and validate the merge (row counts, unmatched records, duplicates).
4. Create a small set of useful **features** (e.g., growth rates, flags, simple transformations).
5. Write a short **Cleaning Log** explaining what you changed (including merges) and why, and recognize when cleaning choices can introduce bias or distort comparisons.
:::

## Why this matters

Most of the time in real analytics is spent **before modeling**:
- fixing inconsistent formats,
- resolving category labels,
- handling missing values,
- ensuring the unit of observation is correct,
- and merging multiple data sources safely.

Good cleaning is not “cosmetic.” It changes your results.

:::{admonition} Reality check
:class: note
A model trained on poorly cleaned data can look sophisticated while being fundamentally unreliable.
:::

---

## Today’s lab datasets

We will use two CSV files:

- [divorce-rates-by-country-2026.csv](../files/divorce-rates-by-country-2026.csv)
- [gdp-per-capita-by-country-2026.csv](../files/gdp-per-capita-by-country-2026.csv)

Both files are essentially **country-level** data, but most variables are stored in **wide format** (years appear in column names such as `_2023`, `_2022`, etc.).  
To merge them properly, we will convert each file into a **country–year** panel.

### Intended unit of observation (after cleaning)
- **One row = one country-year**
- Key columns: `flagCode` + `year` (and `country` as a label)

---

## The course-standard cleaning pipeline

1. **Type check**: numbers as numbers, dates as dates, categories as categories  
2. **Range check**: impossible values (negative rates, nonsensical GDP values, etc.)  
3. **Uniqueness check**: duplicates in keys (`flagCode`, `year`)  
4. **Missingness check**: overall + by key variables  
5. **Consistency check**: country codes/names match across files  
6. **Document everything**: a short cleaning log  

---

## Wide vs long (why reshaping matters)

Many public datasets are reported in **wide form**:

- `DivorcesPer1kPop_2023`, `DivorcesPer1kPop_2022`, ...

But analysis (and merging) is usually easier in **long form**:

- `flagCode`, `country`, `year`, `DivorcesPer1kPop`, ...

:::{admonition} Key idea
:class: important
Wide form is common for reporting.  
Long (country–year) form is usually better for analysis, merging, and plotting.
:::

---

## Merging datasets (the professional habit)

In real projects, your analysis-ready dataset is often the result of a merge:
- outcomes + covariates,
- macro indicators + social indicators,
- business KPIs + external context.

:::{admonition} Key idea
:class: important
A merge is only correct if the **keys** and the **unit of observation** are correct.
Before merging, answer:
1) What is one row?  
2) Which columns uniquely identify a row?
:::

### Join types (keep it simple)
- **Left join** (recommended default): keep all rows from the main dataset and attach what matches from the other dataset.
- **Inner join**: keep only matched rows (risk: silent data loss).
- **Outer join**: keep all rows from both datasets (best for diagnosing mismatch).

### Merge validation (required)
After merging, always check:
1) Row count before vs after  
2) Unmatched records (new missing values created)  
3) Duplicates created unexpectedly  
4) Key uniqueness still holds  

---

## Mini-lab (Google Colab)

:::{admonition} Colab link
:class: tip
Use the class notebook here:

- https://colab.research.google.com/drive/1Y7kG9eYSZlg77AUxVJmj3MxiiGUQYNna?usp=sharing
:::

### In-class checkpoints

**A. Load and inspect**
1. Load both CSV files into DataFrames.
2. Run `df.info()` and identify at least **two** issues (types, missingness, column naming, etc.).

**B. Reshape divorce data to country–year**
3. Convert `divorce-rates-by-country-2026.csv` from wide to long so you have:
   - `flagCode`, `country`, `year`, and the variables:
     - `DivorcesPer1kPop`
     - `NumberOfDivorces`
     - `MarriagesPer1kPop`
     - `NumberOfMarriages`

**C. Reshape GDP per capita data to country–year**
4. Convert `gdp-per-capita-by-country-2026.csv` from wide to long so you have:
   - `flagCode`, `country`, `year`, and at least:
     - `GDPPerCapitaViaWB`
   *(Optional: also reshape PPP variables if you want.)*

**D. Merge**
5. Merge the two long datasets on `flagCode` + `year` (**left join** recommended).
6. Validate the merge:
   - row counts before/after,
   - unmatched rows introduced,
   - duplicates created,
   - key uniqueness.

**E. Feature engineering**
7. Create at least **two** features, for example:
   - `log_gdp_pc = log(GDPPerCapitaViaWB)`
   - `complete = 1` if both `DivorcesPer1kPop` and `GDPPerCapitaViaWB` are non-missing, else `0`
8. Produce a summary table:
   - number of observations,
   - number complete,
   - missingness of key variables.

**F. Cleaning Log**
9. Write a short cleaning log (template at the end) in your notebook.

---

## Python patterns (copy/paste)

### 0) Setup and loading

```python
import pandas as pd
import numpy as np
import re

div = pd.read_csv("divorce-rates-by-country-2026.csv")
gdp = pd.read_csv("gdp-per-capita-by-country-2026.csv")
````

### Quick checks you should always run

```python
div.shape, gdp.shape
div.isna().mean().sort_values(ascending=False).head(10)
gdp.isna().mean().sort_values(ascending=False).head(10)
```

---

### 1) Reshape the divorce dataset (wide → long panel)

The divorce file contains repeated year-suffixed columns for several variable stubs:

* `DivorcesPer1kPop_YYYY`
* `NumberOfDivorces_YYYY`
* `MarriagesPer1kPop_YYYY`
* `NumberOfMarriages_YYYY`

```python
div_year_cols = [c for c in div.columns if re.search(r"_\d{4}$", c)]

div_long = div.melt(
    id_vars=["flagCode", "country"],
    value_vars=div_year_cols,
    var_name="var_year",
    value_name="value"
)

div_long["year"] = div_long["var_year"].str.extract(r"(\d{4})").astype(int)
div_long["variable"] = div_long["var_year"].str.replace(r"_\d{4}$", "", regex=True)
```

Pivot to one row per country-year:

```python
div_panel = (div_long.pivot_table(
    index=["flagCode", "country", "year"],
    columns="variable",
    values="value",
    aggfunc="first"
).reset_index())
```

Key validation:

```python
div_panel.duplicated(subset=["flagCode", "year"]).sum()
```

---

### 2) Reshape the GDP dataset (wide → long panel)

The GDP file has columns like:

* `GDPPerCapitaViaWB_YYYY`
* `GDPPerCapitaPPPIntViaWB_YYYY` (optional)

Start with GDP per capita (WB):

```python
gdp_year_cols = [c for c in gdp.columns if c.startswith("GDPPerCapitaViaWB_")]

gdp_long = gdp.melt(
    id_vars=["flagCode", "country"],
    value_vars=gdp_year_cols,
    var_name="var_year",
    value_name="GDPPerCapitaViaWB"
)

gdp_long["year"] = gdp_long["var_year"].str.extract(r"(\d{4})").astype(int)
gdp_panel = gdp_long[["flagCode", "country", "year", "GDPPerCapitaViaWB"]].copy()
```

Key validation:

```python
gdp_panel.duplicated(subset=["flagCode", "year"]).sum()
```

---

### 3) Merge + validation

```python
merged = div_panel.merge(
    gdp_panel,
    on=["flagCode", "year"],
    how="left",
    validate="one_to_one",
    suffixes=("", "_gdp")
)

# Keep a clean country name (prefer divorce country if present)
if "country_gdp" in merged.columns:
    merged["country"] = merged["country"].fillna(merged["country_gdp"])
    merged = merged.drop(columns=["country_gdp"])
```

Merge checks:

```python
print("div_panel:", div_panel.shape, "gdp_panel:", gdp_panel.shape, "merged:", merged.shape)

print("\nTop missingness after merge:")
print(merged.isna().mean().sort_values(ascending=False).head(12))

print("\nDuplicates on key flagCode-year:", merged.duplicated(subset=["flagCode", "year"]).sum())
```

---

### 4) Feature engineering

```python
merged["log_gdp_pc"] = np.log(merged["GDPPerCapitaViaWB"])

merged["complete"] = (
    merged["GDPPerCapitaViaWB"].notna() &
    merged["DivorcesPer1kPop"].notna()
).astype(int)
```

Quick summary table:

```python
summary = pd.DataFrame({
    "n_rows": [len(merged)],
    "n_complete": [merged["complete"].sum()],
    "share_complete": [merged["complete"].mean()]
})
summary
```

---

## Cleaning Log (required)

Copy this into your notebook and fill it in:

* **Files used:**
* **Unit of observation:** (before / after reshape)
* **Key columns used for merge:**
* **Cleaning steps performed:** (bullets)
* **Reshaping performed?** (wide→long; how?)
* **Join type used + why:**
* **Merge validation results:** (row counts; unmatched; duplicates)
* **Features created:**
* **One limitation / risk:** (e.g., missingness, comparability, measurement)

---

## AI check (responsible use)

:::{admonition} AI check
:class: caution
AI can help propose cleaning and merge steps, but you must:

1. Verify logic with before/after checks (row counts, missingness, duplicates).
2. Avoid blind transformations without checking keys and units.
3. Record prompts and edits in your prompt/workflow log.
   :::

---

## Review questions (quiz / reflection)

1. Why can an inner join silently change your conclusions?
2. What checks would reveal a one-to-many “merge explosion”?
3. Why is long form often easier for analysis than wide form?
4. What is one way cleaning choices can introduce bias?
