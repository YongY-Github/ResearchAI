# Lesson 4 — Data Collection with APIs

:::{admonition} Learning goals
:class: tip
By the end of Lesson 4, you should be able to:
1. Explain the difference between **files**, **APIs**, and **web scraping** (and when each is appropriate).
2. Pull a dataset from **Our World in Data (OWID)** into Google Colab.
3. Create a clean “analysis-ready” table (filter, rename, basic checks).
4. Write a short **Data Source Note** that supports reproducibility and responsible data use.
:::

## Why this matters

Analytics and AI are only as good as the **data pipeline** behind them.
A large part of professional work is:
- finding the right dataset,
- documenting what it is and where it came from,
- and ensuring you can reproduce the same results later.

:::{admonition} Reality check
:class: note
If you cannot clearly explain where the data came from, you cannot defend the analysis.
:::

---

## Three ways to get data (concept map)

:::{admonition} Key idea
:class: important
1. **Download a file** (CSV/Excel): simplest; best when data is stable.
2. **Use an API**: structured access; best for reproducibility and automation.
3. **Web scraping**: last resort; fragile and can raise legal/ethical issues.
:::

### Today’s choice: OWID datasets (file-based, reproducible)
OWID offers high-quality public datasets with clear metadata and regular updates.
We will treat OWID as a model for good practice:
- clear variable names,
- country and time identifiers,
- and a public data pipeline.

---

## What to document (Data Source Note)

:::{admonition} Data Source Note (template)
:class: important
When you use a dataset, record:
- Source (organization + dataset name)
- How you accessed it (URL or API endpoint)
- Date accessed
- Key variables used
- Any filters/transformations you applied
- Known limitations (coverage, measurement, missingness)
:::

---

## Mini case: a business/econ question using OWID

Example questions (choose one):
- “How did inflation evolve across countries after 2020, and how different are country experiences?”
- “How does GDP per capita relate to CO₂ emissions per capita (and does that differ by region)?”
- “How did vaccination rates and excess mortality vary across countries over time?”

:::{admonition} Common pitfall
:class: warning
Country comparisons are sensitive to:
- missing data and reporting differences,
- definitions (e.g., CO₂ production vs consumption),
- and time coverage.
Always check metadata and missingness.
:::

---

## Mini-lab (Google Colab)

:::{admonition} Colab link
:class: tip
Replace this with your real link:

- Week 4 notebook (OWID data pull): https://colab.research.google.com/drive/PASTE_NOTEBOOK_ID
:::

**In-class checkpoints**
1. Load an OWID dataset into a DataFrame.
2. Filter for 3–5 countries and a time range.
3. Produce one plot and one summary table.
4. Write a Data Source Note and one limitation.

---

## AI check (responsible use)

:::{admonition} AI check
:class: caution
AI can help you:
- find relevant OWID datasets (by keyword),
- draft code scaffolding,
- suggest plots.

But you must:
1. verify the dataset matches your question (variables + units),
2. run sanity checks (missingness, ranges),
3. document prompts and edits in your workflow log.
:::

---

## Review questions (quiz / reflection)

1. When is an API better than downloading a CSV?
2. What must be included in a Data Source Note for reproducibility?
3. Give one limitation of cross-country comparisons using public datasets.

:::{admonition} Reflection prompt
:class: note
In ~150 words: Choose one OWID dataset and describe one question you could study with it, plus one limitation.
:::