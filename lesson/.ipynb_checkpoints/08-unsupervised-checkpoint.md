# Lesson 8 — Unsupervised Learning: Clustering & PCA
*(segmentation, dimensionality reduction, and interpretation for business/economics)*

:::{admonition} Learning goals
:class: tip
By the end of Lesson 8, you should be able to:
1. Explain (in plain language) what **unsupervised learning** is and when it is useful.
2. Use **clustering** (e.g., k-means) to create segments and interpret them responsibly.
3. Use **PCA** (principal component analysis) to reduce many variables into a few interpretable dimensions.
4. Decide what counts as “a good segmentation” in practice (stability, usefulness, interpretability).
5. Communicate results with clear visuals and a short, decision-oriented narrative (plus caveats).
:::

## Why this matters (motivation)

In business and economics, you often don’t have a labeled outcome:
- You may not know who will churn yet,
- You may not have a single measure of “customer value,”
- You might want to understand patterns in survey responses, behavior, or firm characteristics.

Unsupervised learning helps you:
- **discover structure** (segments, clusters),
- **compress information** (PCA),
- and generate hypotheses for later modeling or strategy.

:::{admonition} Reality check
:class: note
Unsupervised learning does not “discover truth.”
It creates *useful summaries* of patterns, which must be interpreted and validated.
:::

---

## What is unsupervised learning?

:::{admonition} Key idea
:class: important
- **Supervised learning:** you have a target label $Y$ (predict churn, predict sales).
- **Unsupervised learning:** you do **not** have $Y$; you look for structure in $X$ (segments, dimensions).
:::

### Two main tools today
1. **Clustering:** group similar observations into clusters (segments)
2. **PCA:** reduce many variables into a small number of components

---

## Part A — Clustering for segmentation

### 1) What clustering does (intuition)
Clustering groups observations based on similarity.

Typical business examples:
- customer segmentation (spend, frequency, categories)
- store segmentation (foot traffic, product mix)
- firm clustering (size, leverage, growth, productivity)

:::{admonition} Common pitfall
:class: warning
Clustering results depend strongly on:
- variable choice,
- scaling,
- outliers,
- and the chosen number of clusters.
Always treat clusters as *model outputs*, not facts.
:::

### 2) Scaling matters (a lot)
If one variable has a large numeric scale (e.g., income in dollars),
it can dominate distance calculations unless you standardize.

:::{admonition} Key idea
:class: important
Before k-means, standardize numeric variables (z-scores) unless you have a strong reason not to.
:::

### 3) Choosing the number of clusters (k)
There is no single “correct” k. Practical methods:
- **elbow method** (inertia vs k)
- **silhouette score** (separation/compactness)
- **interpretability and usefulness** (business reality check)

:::{admonition} Practical rule
:class: tip
Prefer a segmentation that is:
- stable across reruns/subsamples,
- easy to interpret,
- and actionable (it changes what you do).
:::

### 4) Cluster labeling (the “human step”)
Once you have clusters, you must interpret them:
- summarize each cluster (mean/median of key variables)
- compare sizes (how many customers in each)
- give a simple label (e.g., “high spend / low frequency”)

:::{admonition} Common pitfall
:class: warning
Avoid over-storytelling.
A cluster label is a short summary, not a personality description.
:::

---

## Part B — PCA for dimensionality reduction

### 1) Why PCA exists
When you have many variables, patterns are hard to see:
- many survey questions,
- many product categories,
- many macro indicators.

PCA creates new variables (“components”) that summarize variation.

:::{admonition} Key idea
:class: important
PCA finds directions in the data that explain the most variance.
- **Component 1** explains the most variance,
- **Component 2** explains the next most (subject to being orthogonal), etc.
:::

### 2) Interpreting PCA (variance explained + loadings)
Two things matter:
- **explained variance ratio**: how much information each component captures
- **loadings**: which original variables contribute strongly to each component

Interpretation idea:
- “Component 1 looks like an overall ‘economic development’ dimension”
- “Component 2 looks like ‘urbanization vs agriculture’”
(These labels are interpretive; you must justify them using loadings.)

:::{admonition} Common pitfall
:class: warning
PCA components are not guaranteed to be easily interpretable.
Sometimes PCA is useful mainly for visualization or as a preprocessing step.
:::

### 3) PCA and segmentation together
A practical workflow:
1. use PCA to reduce dimensions (e.g., 20 variables → 2–5 components)
2. cluster using the components
3. interpret clusters back in original variables

This often improves stability and makes plotting easier.

---

## Mini case: customer segmentation (typical structure)

**Dataset idea:** customer-level data with:
- spending (total, categories),
- frequency,
- recency,
- discounts used,
- returns,
- basic demographics (if available and appropriate)

**Question:** “Are there distinct segments, and what should we do differently for each?”

Segmentation outputs should lead to actions:
- targeted marketing,
- differentiated product bundles,
- pricing/discount strategy,
- service prioritization (but watch fairness concerns).

---

## Visual communication (what you should show)

For clustering:
- scatter plot of two features (or PC1 vs PC2) colored by cluster
- bar chart of cluster sizes
- table of cluster summaries (means/medians)

For PCA:
- explained variance plot
- loading table for first 2–3 components
- scatter of observations in PC space

:::{admonition} Reality check
:class: note
If you cannot summarize a cluster in 2–3 simple sentences, the segmentation is probably not useful (yet).
:::

---

## Mini-lab (Google Colab)

:::{admonition} Colab link
:class: tip
Replace this with your real link:

- Week 8 notebook (Clustering & PCA): https://colab.research.google.com/drive/PASTE_NOTEBOOK_ID
:::

### In-class checkpoints (Clustering)
1. Select 3–6 numeric variables for clustering and justify choice.
2. Standardize variables (or explain why not).
3. Run k-means for at least 3 candidate values of k (e.g., k = 2, 3, 4, 5).
4. Choose k using at least one diagnostic (elbow and/or silhouette) + a business argument.
5. Produce:
   - cluster sizes
   - cluster summary table (means or medians)
   - one visualization colored by cluster

### In-class checkpoints (PCA)
6. Run PCA on the same variables (standardized).
7. Report explained variance for the first components.
8. Interpret Component 1 and Component 2 using loadings (in words).
9. Plot data in PC1–PC2 space; optionally cluster in PC space.

### Submission (after class)
- Colab link (view permission) or PDF export.
- Include:
  - a short segmentation narrative (headline + evidence + action),
  - and one limitation/caveat.

---

## AI check (responsible use for unsupervised learning)

:::{admonition} AI check
:class: caution
AI can help you interpret cluster summaries and PCA loadings, but you must:
1. Verify interpretations against actual numbers (cluster tables, loadings).
2. Avoid making value judgments or stereotypes about groups.
3. Document prompts and edits in your prompt/workflow log.
:::

**Good prompt examples**
- “Given this cluster summary table, suggest neutral labels and 1–2 business actions per cluster.”
- “Given these PCA loadings, propose an interpretation for PC1 and PC2 and explain your reasoning.”
- “What checks can I run to test whether my clusters are stable?”

**Bad prompt example**
- “Tell me what these clusters ‘really mean’ about customers” (overclaiming)

---

## Review questions (quiz / reflection)

1. Why is standardization important for k-means clustering?
2. Why is there no single “correct” number of clusters?
3. What does “explained variance” mean in PCA?
4. What is one responsible caveat you should include when presenting clusters?

:::{admonition} Reflection prompt
:class: note
In ~150 words: Describe your segmentation result:
- how many clusters you chose (and why),
- one key difference between two clusters,
- and one action you would recommend (plus one limitation).
:::