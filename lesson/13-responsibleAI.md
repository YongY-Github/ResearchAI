# Lesson 13 — Ethics, Fairness & Responsible AI
*(privacy, bias, explainability, and “should we deploy?” thinking)*

:::{admonition} Learning goals
:class: tip
By the end of Lesson 13, you should be able to:
1. Identify key ethical risks in analytics/AI projects: privacy, bias, discrimination, opacity, misuse, and overreach.
2. Explain (at a practical level) how bias can enter the pipeline: data → labels → features → objectives → deployment.
3. Use simple checks for fairness risk (group comparisons, error-rate differences) and interpret them cautiously.
4. Understand what model explainability tools (e.g., SHAP/LIME) aim to do, and their limitations.
5. Write a short “Responsible AI Checklist” for your capstone: what you will do, what you will not do, and what you must disclose.
:::

## Why this matters (motivation)

Analytics and AI are not only technical tools—they influence people.
Even “simple” models can affect:
- credit access,
- hiring and promotion,
- pricing and eligibility,
- education and opportunities.

Responsible AI means:
- using data legally and ethically,
- protecting privacy,
- avoiding unfair harms,
- and communicating limitations honestly.

:::{admonition} Reality check
:class: note
A model can be accurate and still be harmful.
Responsible AI asks: “Accurate for whom?” and “At what cost?”
:::

---

## Part A — What “responsible AI” means in this course

:::{admonition} Key idea
:class: important
Responsible AI (course version) means:
1. **Purpose:** the model supports a legitimate decision
2. **Data ethics:** data is collected/used appropriately and documented
3. **Fairness:** check for harm or unequal error patterns
4. **Transparency:** explain what the model does and what it cannot do
5. **Accountability:** humans remain responsible for decisions
6. **Safety:** avoid over-automation in high-stakes contexts
:::

### Two useful frameworks (light use)
- OECD AI Principles (high-level principles)
- NIST AI Risk Management Framework (risk-based approach)

We use these as *checklists*, not as heavy policy documents.

---

## Part B — Privacy and data governance (practical)

### What counts as sensitive in typical student projects?
Examples:
- personal identifiers (names, phone numbers, precise addresses)
- health information
- detailed location traces
- any data that can re-identify individuals
- high-risk attributes tied to discrimination concerns

In this course:
- prefer public datasets (e.g., OWID) or anonymized teaching datasets
- if using survey/interview text, remove personal identifiers

:::{admonition} Practical rule
:class: tip
If you do not need a variable to answer your question, do not collect it.
“Data minimization” reduces privacy risk and is good scientific practice.
:::

### Privacy basics to communicate in a report
- where the data came from
- what personal data is included (if any)
- how it was anonymized/aggregated
- who has access
- how long it is stored

---

## Part C — Fairness and bias: where problems enter

Bias can enter through multiple channels:

### 1) Target label problem
What is the label measuring?
- “loan default” may reflect economic shocks and unequal opportunity, not only “responsibility”
- “employee performance” can be influenced by manager bias

### 2) Feature and proxy problem
Some features act as proxies for sensitive attributes:
- zip code, language, school attended, device type, etc.

### 3) Sampling problem
Your dataset may not represent the population:
- missing rural groups
- missing small firms
- platform users only

### 4) Measurement problem
Errors may differ across groups:
- underreporting in some communities
- inconsistent definitions across countries

### 5) Objective problem
Optimizing overall accuracy can produce unequal harm.
Example: a model may reduce errors for majority groups while increasing errors for minority groups.

:::{admonition} Key idea
:class: important
Fairness is a question of *harm and error distribution*, not only overall performance.
:::

---

## Part D — Minimal fairness checks (what we can do at this level)

We keep fairness checks simple and transparent.

### Step 1: Choose a grouping variable (if available and appropriate)
Examples:
- region
- age bracket
- income bracket
- firm size category
- (avoid sensitive attributes unless clearly justified and ethically handled)

### Step 2: Compare performance by group
For classification (e.g., churn yes/no), compare:
- accuracy by group
- false positive rate by group
- false negative rate by group

For continuous outcomes (regression/forecasting), compare:
- MAE or RMSE by group
- systematic under/over-prediction by group

### Step 3: Interpret carefully
A difference does not automatically prove discrimination.
But it is a red flag that requires explanation and monitoring.

:::{admonition} Common pitfall
:class: warning
Students sometimes “prove fairness” by showing one metric is similar across groups.
Fairness is multi-dimensional and context-dependent.
At minimum, you should identify risks and propose monitoring.
:::

---

## Part E — Explainability: what it is and what it isn’t

Many real stakeholders ask: “Why did the model make this prediction?”

### Global vs local explainability (simple distinction)
- **Global**: what features matter overall? (feature importance)
- **Local**: why for this particular case? (SHAP/LIME style explanations)

:::{admonition} Key idea
:class: important
Explainability tools provide *model-based explanations*, not necessarily real-world causation.
They help with:
- debugging,
- communicating,
- and auditing.
But they do not magically make a model fair or causal.
:::

### Practical role in your capstone
You may use explainability to:
- identify surprising predictors,
- detect potential proxy features,
- explain predictions in a report.

But always include a caveat:
- “This explains the model, not the true causal mechanism.”

---

## Part F — “Should we deploy?” (a decision rubric)

Even if you are not actually deploying systems, this is a useful professional habit.

:::{admonition} Deployment rubric (student version)
:class: important
Before using a model for a real decision, ask:
1. What is the decision? Who is affected?
2. What happens if the model is wrong (FP vs FN costs)?
3. Is there a fairness risk? How will you monitor it?
4. Is the data appropriate and legally/ethically sourced?
5. Is the model interpretable enough for the context?
6. What human oversight exists?
7. What will you disclose in communication?
:::

---

## Mini case discussion (in class)

Choose one case:
1. Credit scoring
2. Hiring screening
3. Pricing / eligibility
4. Student risk prediction (education analytics)
5. Platform moderation or fraud detection

For the chosen case:
- identify risks in data, labels, features
- propose minimal fairness checks
- propose transparency statements

---

## Mini-lab (Google Colab)

:::{admonition} Colab link
:class: tip
Replace this with your real link:

- Week 13 notebook (Responsible AI checks): https://colab.research.google.com/drive/PASTE_NOTEBOOK_ID
:::

### In-class checkpoints (privacy & documentation)
1. Write a short “Data Governance Note” for your capstone dataset:
   - source, access date, unit of observation
   - what personal data exists (if any)
   - storage/access plan
   - limitations

### In-class checkpoints (fairness checks)
2. Choose a grouping variable (if available).
3. Compute and compare at least one metric by group:
   - classification: accuracy + FN rate (or FP rate)
   - forecasting/regression: MAE by group or by time period
4. Write 5–7 lines interpreting results and stating one risk.

### In-class checkpoints (explainability — concept + demo)
5. Use a simple explainability tool (or a simplified feature importance):
   - identify top features driving predictions
6. Identify at least one proxy risk or surprising feature, and describe what you would investigate next.

### In-class checkpoints (capstone checklist)
7. Draft your **Responsible AI Checklist** for the capstone (see below).

**Submission (after class)**
- Colab link (view permission) or PDF export.
- Include your Responsible AI Checklist and a short ethics note.

---

## Capstone Responsible AI Checklist (required)

:::{admonition} Deliverable
:class: important
Write a **Responsible AI Checklist** (about half a page) for your capstone. Include:

1. **Purpose**: What decision/question is your analysis supporting?
2. **Data provenance**: Where did the data come from? How is it measured?
3. **Privacy**: What personal data exists? How do you protect it? (or state “public aggregated data only”)
4. **Fairness risks**: What proxy variables or group disparities might matter?
5. **Validation**: What checks will you run to ensure reliability?
6. **Transparency**: What will you disclose in your report about limitations and AI assistance?
7. **Non-deployment clause (if appropriate)**: “This model is for educational analysis and should not be used for automated decisions without further evaluation.”
:::

---

## AI check (meta)

:::{admonition} AI check
:class: caution
AI tools can help draft checklists and rephrase text, but:
- you must ensure the checklist matches your project reality,
- and you must not claim you ran checks you did not actually run.
Document prompts and edits if you use AI for writing.
:::

---

## Review questions (quiz / reflection)

1. Give two ways bias can enter a model pipeline.
2. Why can an accurate model still be harmful?
3. What is the difference between explaining the model and explaining the real world?
4. Name one fairness check you can do at a basic level in this course.

:::{admonition} Reflection prompt
:class: note
In ~200 words: For your capstone project, identify:
- one privacy risk (or state why none applies),
- one fairness/proxy risk,
- and one disclosure statement you will include in your final report.
:::