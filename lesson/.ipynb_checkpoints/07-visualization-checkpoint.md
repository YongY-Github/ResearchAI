# Lesson 7 — Data Visualization for Communication
*(chart choice, storytelling, interactive plots, and honest interpretation)*

:::{admonition} Learning goals
:class: tip
By the end of Lesson 7, you should be able to:
1. Choose an appropriate chart type for a specific question (comparison, trend, distribution, relationship, composition).
2. Create clear, honest visualizations in Python (Google Colab) using matplotlib and/or Plotly.
3. Build a small “dashboard-like” set of visuals (2–4 charts) that support a coherent narrative.
4. Recognize common visualization pitfalls (misleading scales, aggregation traps, cherry-picking, clutter).
5. Write a short “data story” that connects visuals to decisions, including uncertainty and limitations.
:::

## Why this matters (motivation)

In business and economics, most decisions are made from:
- charts in slide decks,
- dashboards,
- short memos with figures.

Even a correct model can be ignored if the story is unclear.  
And a misleading chart can create confidence in the wrong conclusion.

:::{admonition} Reality check
:class: note
Visualization is not decoration. It is an argument with evidence.
Your job is to make the evidence understandable *without exaggerating certainty*.
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
- **Metric:** What is being measured (units, time, denominator)?
:::

### A practical checklist (before you plot)
1. **Unit of observation:** customer? transaction? month? firm?
2. **Aggregation rule:** sum, mean, median, rate per 1,000?
3. **Comparability:** are groups measured the same way?
4. **Missingness:** are you hiding missing values?
5. **Uncertainty:** do you need error bars, bands, or sample sizes?

---

## Chart chooser (fast and useful)

:::{admonition} Key idea
:class: important
Match the chart to the task:
- **Compare** categories → bar chart (sorted)
- **Trend** over time → line chart
- **Distribution** → histogram / density / boxplot
- **Relationship** between two numeric variables → scatter plot
- **Two-way comparison** (category × category) → heatmap
- **Composition** (parts of a whole) → stacked bars (use sparingly)
:::

### Common business questions and “good default” charts
- “Which product category grew the most?” → sorted bar chart of growth rates  
- “Is sales increasing over time?” → line chart (with smoothing optional)  
- “Are there segments of customers?” → scatter plot colored by cluster; or boxplots by segment  
- “Is marketing associated with sales?” → scatter plot + fitted line; or faceted by category  
- “Where are we missing data?” → missingness bar chart by variable or by group  

:::{admonition} Common pitfall
:class: warning
Pie charts often hide differences and make comparison hard.
If the audience must compare values, prefer sorted bars.
:::

---

## Honest charts: common ways charts mislead (often unintentionally)

### 1) Truncated axes
A bar chart with a y-axis that doesn’t start at 0 can exaggerate differences.

:::{admonition} Rule of thumb
:class: tip
- For **bar charts**, start at 0 unless you have a strong reason not to.
- For **line charts**, a truncated axis can be acceptable, but you must label clearly and avoid “dramatic” framing.
:::

### 2) Aggregation traps
Averages can hide important patterns:
- A rising average can be driven by a small number of extreme observations.
- Aggregating across regions/segments can hide opposite trends.

:::{admonition} Common pitfall
:class: warning
Always ask: “Would this conclusion still hold if I split by region/segment/time?”
This is where Simpson’s paradox can appear.
:::

### 3) Cherry-picking time windows
Trends can flip depending on start/end dates.

### 4) Too much ink / too many categories
Clutter weakens interpretation. If there are many categories:
- show top 10 + “other,” or
- facet into multiple charts, or
- allow interaction (filtering).

### 5) Causality by implication
A chart can quietly suggest a causal story (e.g., “marketing causes sales”) even if the analysis only shows correlation.

---

## Building a “data story” (how to present visuals)

:::{admonition} Key idea
:class: important
A data story is not a long essay.
It is a structured argument:
1. **Headline** (one sentence claim)
2. **Evidence** (1–3 charts)
3. **So what** (decision implication)
4. **Caveat** (limitation, uncertainty, missingness, confounding)
:::

### Template: chart caption that actually helps
- **What:** what the chart shows (variable + unit + time)
- **Pattern:** what stands out (trend, difference, outlier)
- **Meaning:** what this might imply for the decision

Example caption:
> “Sales in Category A increased steadily after 2021, while Category C declined. The change coincides with a shift in marketing spend; however, the relationship is correlational and may reflect seasonality or pricing differences.”

---

## Visualization and uncertainty (optional but powerful)

Sometimes “point estimates” are not enough. Options:
- confidence intervals / error bars (when you have sampling uncertainty),
- rolling averages (to reduce noise),
- showing sample size (n) explicitly,
- distribution plots instead of averages.

:::{admonition} Practical rule
:class: tip
If your audience might overreact to noise, show uncertainty or smooth sensibly.
But never smooth in a way that hides important changes.
:::

---

## Mini case: communicating a regression result visually

From Week 6, you may have estimated:
- sales ~ marketing + price + season controls

How to visualize for communication:
- Scatter plot of sales vs marketing with fitted line (simple picture)
- Facet by category or region if patterns differ
- Show time trend of sales and marketing side-by-side
- Boxplots of sales by season/quarter to highlight seasonality

:::{admonition} Common pitfall
:class: warning
A regression table is not a story for most audiences.
A single strong plot plus one careful caption often communicates more than a full table.
:::

---

## Mini-lab (Google Colab)

:::{admonition} Colab link
:class: tip
Replace this with your real link:

- Week 7 notebook (Visualization): https://colab.research.google.com/drive/PASTE_NOTEBOOK_ID
:::

### In-class checkpoints (core)
1. Create **one** chart for each purpose:
   - comparison (bar)
   - trend (line)
   - distribution (hist/box)
   - relationship (scatter)
2. For each chart, add:
   - title with variable and unit
   - readable axis labels
   - a short caption (“headline + meaning”)

### In-class checkpoints (storytelling)
3. Choose ONE question and build a mini “dashboard” (2–4 charts):
   - Example questions:
     - “Which category is growing and why?”
     - “Which segment has higher churn risk signals?”
     - “How did the key metric change before/after a policy/event date?”
4. Write a short narrative:
   - 1 headline sentence
   - 3 bullet points (evidence)
   - 1 caveat

### In-class checkpoints (optional extensions)
5. Add an uncertainty element:
   - show sample sizes
   - or show a distribution instead of an average
   - or add a rolling average line (time series)
6. Make an interactive Plotly version of at least one plot with hover labels and filters.

**Submission (after class)**
- Colab link (view permission) or PDF export.
- Include your 2–4 chart “dashboard” and written narrative.

---

## Tool box: minimal code patterns (for your notebook)

:::{admonition} Python patterns you will reuse
:class: note
- `df.groupby("category")["sales"].mean().sort_values()`
- `df.assign(log_sales=np.log1p(df["sales"]))`
- `df.query("country in @countries and year >= 2000")`
- `df.isna().mean().sort_values(ascending=False)`
:::

*(In your Colab notebook, you can include these as “snippets” for students to modify.)*

---

## AI check (responsible use for visualization)

:::{admonition} AI check
:class: caution
AI can help you brainstorm chart types and captions, but you must:
1. Verify that the chart answers the intended question.
2. Avoid causal language unless you have a causal design.
3. Check for misleading design (axes, aggregation, cherry-picking).
4. Record prompts and edits in your prompt/workflow log.
:::

**Good prompt examples**
- “Given this question and these columns, suggest 3 chart options and explain what each would show.”
- “Write a caption template that includes a caveat and avoids causal claims.”
- “What is a common visualization pitfall for comparing averages across groups?”

**Bad prompt example**
- “Write a persuasive story that marketing caused sales to rise” (without justification)

---

## Review questions (quiz / reflection)

1. Which chart type would you use for: (i) trend, (ii) distribution, (iii) relationship—and why?
2. What is one example of a misleading chart design choice and how to fix it?
3. Why can aggregation hide important patterns? Give one example from business/economics.

:::{admonition} Reflection prompt
:class: note
In ~150 words: Choose one of your charts and explain:
- what question it answers,
- what the main pattern is,
- and one limitation (missing data, aggregation, uncertainty, or comparability).
:::