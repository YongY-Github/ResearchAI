# Lesson 14 — Capstone Presentations & Course Wrap-Up
*(end-to-end analysis, communication, and reflection)*

:::{admonition} Learning goals
:class: tip
By the end of Lesson 14, you should be able to:
1. Present an end-to-end analytics project clearly in **10 minutes** (question → data → method → results → implications → limitations).
2. Defend your choices: why this dataset, why this method, and what you verified.
3. Communicate results responsibly: avoid overclaiming, highlight uncertainty, and state ethical/fairness considerations.
4. Reflect on your learning: what you can now do independently and what you still need to practice.
:::

## Class plan (10-minute presentations)

Each group (or individual) presents for **10 minutes** + **3–5 minutes Q&A**.

Suggested structure (10 minutes total):
1. **Motivation and research question** (1 min)
2. **Data** (1–2 min)
3. **Method and workflow** (2 min)
4. **Results (key visuals/tables)** (3 min)
5. **Interpretation + implications** (1 min)
6. **Limitations + responsible AI note** (1 min)

:::{admonition} Practical advice
:class: tip
Your audience should understand the main result even if they do not know Python.
Use visuals and plain language.
:::

---

## What the capstone must contain (final submission)

:::{admonition} Capstone deliverables
:class: important
Your final capstone submission includes:

### 1) Slide deck (for presentation)
- 8–12 slides recommended
- include at least 2 clear visuals (charts/plots)
- include 1 slide on limitations + responsible AI

### 2) Written report (recommended 5–7 pages, excluding appendix)
**Required sections:**
1. Title + abstract (100–150 words)
2. Introduction (motivation, research question)
3. Data (source, unit of observation, time period, variables; data limitations)
4. Methods (what you did and why)
5. Results (visuals/tables + interpretation)
6. Discussion (implications; limitations; what you would do next)
7. Responsible AI and ethics note (privacy, fairness risks, disclosure)
8. Conclusion (2–4 key takeaways)

### 3) Colab notebook(s) (reproducible)
- clean and runnable
- includes key outputs/plots
- includes brief comments and headings

### 4) Prompt & workflow log (if AI tools were used)
- prompts used (or summary)
- what you accepted/modified/rejected
- verification steps you performed
:::

---

## Allowed scope (choose ONE main method; optional secondary analysis)

### Choose ONE as your main method
- Regression (simple/multiple)
- Unsupervised learning (clustering and/or PCA)
- Decision tree model (classification)
- Text-as-data (sentiment / simple NLP)
- Time series forecasting (baselines + evaluation)

Optional: you may add one secondary method briefly, but the project should remain focused and interpretable.

:::{admonition} Reality check
:class: note
A focused, well-explained project is better than a broad project with shallow results.
:::

---

## Expectations for quality (what “good” looks like)

### A good capstone shows:
- **Clear question** (not just a topic)
- **Clean data** with documentation (data source note + cleaning choices)
- **Appropriate method** with justification
- **Verification** (sanity checks, baselines, and/or robustness checks)
- **Communication** (good charts + clear narrative)
- **Responsible AI** (prompt log + no fake citations + honest limitations)
- **Ethics/fairness awareness** (at least one risk + one mitigation/monitoring idea)

### Verification examples (pick 3–5)
- missingness summary (overall and by group)
- outlier check and handling rule
- baseline comparison (for forecasting or classification)
- train/test split that avoids leakage (especially time series)
- sensitivity check (e.g., alternate variable definition, alternate k in clustering)
- manual spot-check for NLP outputs (inspect misclassified examples)

---

## Grading rubric (suggested)

:::{admonition} Capstone grading (example rubric)
:class: important
You can adjust weights to match your official grading scheme.

### A) Presentation (10 minutes) — 25%
- Clarity of story and structure (10%)
- Quality of visuals and explanation (10%)
- Q&A responses (5%)

### B) Report — 35%
- Research question and motivation (5%)
- Data description + limitations (10%)
- Method clarity and appropriateness (10%)
- Results interpretation (10%)

### C) Technical notebook quality — 20%
- Reproducibility (runs cleanly; outputs match report) (10%)
- Code clarity and organization (5%)
- Verification checks included (5%)

### D) Responsible AI & ethics — 20%
- Prompt/workflow log and transparency (10%)
- Verification of AI outputs / no hallucinated citations (5%)
- Ethical/fairness note: risk identification + mitigation/monitoring (5%)
:::

:::{admonition} Important policy note
:class: warning
Copy-pasting AI-generated text without verification or without disclosure is not acceptable.
If AI tools are used, you must include a prompt/workflow log and you must be able to explain your work.
:::

---

## Wrap-up discussion (in class)

We close the course with:
- “What skills are now in your toolkit?”
- “What surprised you about data work?”
- “Where did AI help, and where did it mislead?”
- “What would you learn next if you had 4 more weeks?”

---

## Final reflection (submit)

:::{admonition} Reflection prompt
:class: note
In ~250–400 words:
1. What is the most important skill you gained in this course?
2. Describe one mistake you made (or almost made) and how you caught it.
3. How will you use AI tools responsibly in your future work?
:::