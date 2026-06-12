# Lesson 7 — Data Visualization for Communication
*(chart choice, storytelling, interactive plots, and honest interpretation)*

:::{admonition} Learning goals
:class: tip
By the end of Lesson 7, you should be able to:
1. Choose an appropriate chart type for a specific question: comparison, trend, distribution, relationship, or composition.
2. Create clear, honest visualizations in Python (Google Colab) using `matplotlib` and Plotly.
3. Build a small “dashboard-like” set of visuals that supports a coherent narrative.
4. Build and interpret a **Gapminder-style visualizer** using income, life expectancy, population, and time.
5. Recognize common visualization pitfalls: misleading scales, aggregation traps, cherry-picking, clutter, and causal overinterpretation.
:::

## Why this matters

In business and economics, most decisions are made from:
- charts in slide decks,
- dashboards,
- short memos with figures,
- interactive visuals that allow users to explore patterns.

Even a correct model can be ignored if the story is unclear.  
And a misleading chart can create confidence in the wrong conclusion.

:::{admonition} Reality check
:class: note
Visualization is not decoration. It is an argument with evidence.
Your job is to make the evidence understandable **without exaggerating certainty**.
:::

---

## Today’s running example: Gapminder-style visualization

See https://www.youtube.com/watch?v=jbkSRLYSojo
Also https://ourworldindata.org/search?topics=Life+Expectancy&resultType=all

Today we use three Gapminder data files:

- [lex.csv](../files/lex.csv) — life expectancy  
- [gdp_pcap.csv](../files/gdp_pcap.csv) — GDP per capita / income per person  
- [pop.csv](../files/pop.csv) — population  

These files are in **wide format**: one row per country, with years stored as columns such as `1800`, `1801`, `1802`, and so on.

We will reshape them into long format, merge them into a country-year panel, and create a Gapminder-style visualizer.

:::{admonition} Colab link
:class: tip
Use the class notebook here:

- https://colab.research.google.com/drive/14BXPBiB0iOPpqDuvTjDUbvXT2_ZeoKfl?usp=sharing
:::

---

## The visualization mindset: “What question does this answer?”

:::{admonition} Key idea
:class: important
Every chart should answer a question that someone actually cares about.
Before plotting, write:
- **Question:** What do we want to know?
- **Audience:** Who will read it?
- **Decision:** What choice might change based on this plot?
- **Metric:** What is being measured? What are the units?
:::

### A practical checklist before plotting

1. **Unit of observation:** country-year? customer? firm? transaction?
2. **Aggregation rule:** sum, mean, median, rate, ratio?
3. **Comparability:** are groups measured in the same way?
4. **Missingness:** are you hiding missing values?
5. **Scale:** should the axis be raw or log?
6. **Uncertainty:** do you need sample sizes, bands, caveats, or confidence intervals?

---

## Chart chooser: matching chart to purpose

:::{admonition} Key idea
:class: important
Match the chart to the task:
- **Compare categories** → bar chart
- **Trend over time** → line chart
- **Distribution** → histogram, density, or boxplot
- **Relationship between two numeric variables** → scatter plot
- **Two-way comparison** → heatmap
- **Interactive exploration over time** → animated scatter / dashboard
:::

### Today’s chart types

In the Gapminder lab, we will create:

1. **Static scatter plot**  
   - Question: Are richer countries associated with longer life expectancy?
   - Example: life expectancy vs log GDP per capita in one year.

2. **Animated bubble chart**  
   - Question: How have income, health, and population changed over time?
   - Example: Gapminder-style animation from 1800 onward.

3. **Line charts for selected countries**  
   - Question: How did Japan, Thailand, and the United States evolve over time?
   - Example: life expectancy and GDP per capita over time.

---

## The Gapminder-style chart

A Gapminder-style chart typically uses:

- x-axis: GDP per capita / income per person
- y-axis: life expectancy
- bubble size: population
- animation: year
- hover label: country

This is powerful because it combines:
- **relationship**: income and life expectancy,
- **trend**: changes over time,
- **comparison**: countries moving differently,
- **scale**: population size.

:::{admonition} Key idea
:class: important
A Gapminder-style chart is not just a “pretty animation.”
It is a way to tell a story about development, health, inequality, and change over time.
:::

---

## Why use a log scale for GDP per capita?

GDP per capita is highly skewed. A few countries have very high income levels, while many others are clustered at lower income levels.

If we use raw GDP per capita on the x-axis, many countries may be squeezed into the left side of the graph.

Using a log scale makes the pattern easier to see.

:::{admonition} Interpretation note
:class: note
On a log scale, equal distances represent proportional changes.
Moving from $1{,}000$ to $2{,}000$ is treated similarly to moving from $10{,}000$ to $20{,}000$ because both are doublings.
:::

---

## Honest charts: common ways visualizations mislead

### 1. Misleading axes

A chart can exaggerate or hide differences depending on axis choices.

:::{admonition} Rule of thumb
:class: tip
- For bar charts, start the y-axis at 0 unless you have a strong reason not to.
- For line charts and scatter plots, choose scales that reveal the pattern without exaggerating it.
- If using a log scale, say so clearly.
:::

### 2. Aggregation traps

Averages can hide important variation.

For example:
- global life expectancy may rise,
- but some countries may stagnate or fall behind.

:::{admonition} Common pitfall
:class: warning
Always ask: “Would this conclusion still hold if I split by country, region, income group, or time period?”
:::

### 3. Cherry-picking time windows

Trends can look very different depending on start and end dates.

A country’s GDP per capita may look impressive from 2000 onward, but less so if we start from 1980.

### 4. Too much clutter

A chart with too many lines or labels can become unreadable.

Good options:
- show 3–5 selected countries,
- use interaction,
- create separate panels,
- or use a table only when exact values matter.

### 5. Causality by implication

A chart can quietly suggest a causal story even when it only shows association.

For example, a scatter plot of GDP per capita and life expectancy does **not** prove that income alone causes longer life. Health systems, education, public policy, conflict, and many other factors matter.

---

## Building a data story

:::{admonition} Key idea
:class: important
A data story is a structured argument:
1. **Headline** — one sentence claim
2. **Evidence** — 1–3 visuals
3. **So what** — why the pattern matters
4. **Caveat** — what the visual cannot prove
:::

### Caption template

A useful chart caption includes:

- **What:** what the chart shows
- **Pattern:** what stands out
- **Meaning:** why it matters
- **Caveat:** what we should be careful about

Example:

> “Countries with higher GDP per capita tend to have higher life expectancy, especially after 1950. However, the relationship is not perfectly linear, and the chart shows association rather than causation.”

---

## Mini-lab (Google Colab)

:::{admonition} Colab link
:class: tip
Use the class notebook here:

- https://colab.research.google.com/drive/14BXPBiB0iOPpqDuvTjDUbvXT2_ZeoKfl?usp=sharing
:::

### In-class checkpoints

**A. Load and inspect**

1 Load the three source files:  
    - `lex.csv`  
    - `gdp_pcap.csv`  
    - `pop.csv`  

2 Run basic checks:
    - shape,  
    - column names,  
    - missingness,  
    - year range.

**B. Reshape and merge**  
3. Convert each dataset from wide to long format.  
4. Keep both:  
    - `geo` = country code,  
    - `name` = country name.  
5. Merge into one country-year panel.  
6. Rename `name` to `country`.

**C. Static visualization**  
7. Choose one year, such as 2019.  
8. Create a scatter plot:  
    - x-axis: log GDP per capita,  
    - y-axis: life expectancy.  
9. Write a short interpretation of the pattern.

**D. Gapminder-style visualizer**  
10. Create an animated bubble chart:  
    - x-axis: GDP per capita,
    - y-axis: life expectancy,  
    - bubble size: population,  
    - animation: year,  
    - hover label: country.  
11. Use a log scale for GDP per capita.  
12. Set a sensible y-axis range, such as 0 to 100 years.  

**E. Story charts**  
13. Choose 3–5 countries.  
14. Produce:  
    - life expectancy over time,  
    - GDP per capita over time,  
    - Feel free to look at gender differences, or poor versus rich countries, etc. 
15. Write a mini data story:    
    - one headline,  
    - 2–3 evidence bullets,  
    - one caveat.

Submit here: https://docs.google.com/forms/d/e/1FAIpQLSdaRJKEtbf4kAbnNGXXbyBrwgxceYDjBjyzkXSJ-E27_50Gjg/viewform?usp=sharing&ouid=103851245469429210515

---

## Useful Python patterns

:::{admonition} Python patterns you will reuse
:class: note
Useful snippets from today’s notebook:

```python
# Find country names
country_names = sorted(panel["country"].dropna().unique())

# Search for country names
panel[panel["country"].str.contains("United", case=False, na=False)]["country"].drop_duplicates()

# Select countries
countries = ["Japan", "Thailand", "United States of America"]
sub = panel[panel["country"].isin(countries)].copy()

# Filter years
panel_1800_2025 = panel[(panel["year"] >= 1800) & (panel["year"] <= 2025)].copy()