# Lesson 11 — Scientific Research with AI in Social Sciences
*(literature mapping, evidence synthesis, qualitative coding, and Capstone Proposal v1)*

:::{admonition} Learning goals
:class: tip
By the end of Week 11, you should be able to:
1. Turn a broad interest into a focused, answerable **research question** suitable for social science.
2. Use AI tools to support a transparent **literature mapping** workflow (search → screen → cluster → summarize).
3. Identify themes, gaps, and plausible hypotheses **without overstating evidence**.
4. Perform a small qualitative coding exercise (manual vs AI-assisted) and reflect on reliability.
5. Draft a clear **Capstone Proposal v1**: question + data plan + method plan + verification plan + AI transparency plan.
6. Document your workflow (sources + prompts + decisions) so your research is verifiable and academically honest.
:::

## Why this matters (motivation)

AI tools can speed up:
- finding papers,
- organizing themes,
- drafting summaries,
- and coding text.

But social-science research is not “speed-writing.” Quality comes from:
- careful question design,
- transparent evidence handling,
- and critical interpretation.

This week also connects to what you have learned so far:
you now have multiple tool families (EDA/visualization, probability/simulation, regression, clustering/PCA, trees, text signals, and forecasting). The research challenge is choosing the **right tool for the question**—and justifying that choice with evidence and transparency.

:::{admonition} Reality check
:class: note
AI can help you move faster, but it cannot replace research judgment:
what counts as evidence, what is credible, and what is uncertain.
:::

---

## A research workflow (the course version)

:::{admonition} Key idea
:class: important
A simple scientific workflow that scales from small class projects to publishable work:
1. Research question (clear and answerable)
2. Literature mapping (what is known and debated)
3. Data plan and evidence strategy (empirical data and/or qualitative evidence)
4. Analysis + robustness checks (appropriate to your method)
5. Interpretation + limitations
6. Transparent reporting and reproducibility
:::

Today we focus on Steps 1–3 and practice a small piece of qualitative coding.

---

## Part A — Research questions: from topic to question

### Topic vs question
- Topic: “Remote work”
- Research question: “How is remote work associated with self-reported productivity and job satisfaction across industries?”

A good question has:
- a clear population/unit (who? what?)
- a clear outcome (what is measured?)
- a feasible strategy (what data or evidence?)

:::{admonition} Common pitfall
:class: warning
Many student projects stay at the level of “journalistic topics.”
A research question must be specific enough to be tested or evidenced.
:::

### A quick “question tightening” template
- **Population / setting:** (e.g., Thai firms, ASEAN consumers, university students)
- **Outcome:** (e.g., sales growth, job satisfaction, adoption probability, inflation)
- **Mechanism or channel (optional):** (e.g., flexibility, monitoring, cost savings)
- **Comparison:** (e.g., before/after, high/low exposure, group comparisons)
- **Feasibility:** data available? time constraints? permissions?

---

## Part B — Literature mapping with AI (transparent, not magical)

### What literature mapping is (and is not)
- It is not: “ask AI for 10 papers and copy the summary.”
- It is: a structured method to discover themes, debates, and gaps.

:::{admonition} Key idea
:class: important
Literature mapping workflow:
1. Generate search terms (human + AI-assisted)
2. Retrieve candidate papers (databases/APIs)
3. Screen (explicit relevance criteria)
4. Cluster or group (themes, methods, settings)
5. Summarize and identify gaps (with citations)
:::

### Recommended tools (choose your level)
- Semantic Scholar (search + metadata; API optional)
- Connected Papers (visual map; optional)
- Zotero (organize citations; optional)

AI usage: drafting search strings, summarizing abstracts, proposing a theme taxonomy — **but you must verify**.

:::{admonition} Practical rule
:class: tip
Your literature map should end with:
- 2–4 themes,
- 1–2 open questions/gaps,
- and a clear statement of what your project will contribute (even if small).
:::

---

## Part C — Evidence synthesis: writing “what we know”

A good synthesis does more than list papers.
It organizes evidence by:
- methods (survey, experiment, panel regression, text analysis, forecasting),
- context (country, industry),
- findings (consistent vs mixed),
- limitations (data, measurement, identification),
- and open questions.

:::{admonition} Practical rule for writing
:class: tip
Write synthesis in “claim + evidence + caveat” form.

Example:
“Several studies find X in context A (citations), but evidence is mixed in context B (citations), partly due to measurement differences (caveat).”
:::

---

## Part D — Qualitative coding with AI (and why we compare to manual coding)

### Why qualitative coding matters
Interviews, open-ended survey responses, policy documents, and news text are common evidence sources.

Coding turns text into:
- themes,
- categories,
- structured analysis.

### AI-assisted coding: promise and risk
Promise:
- speed,
- consistency,
- quick theme suggestions.

Risks:
- hallucinated themes,
- overconfident labels,
- bias/stereotypes,
- missing nuance (sarcasm, context).

:::{admonition} Key idea
:class: important
Treat AI as a “coding assistant,” not a judge.
The researcher defines the codebook and checks ambiguous cases.
:::

### A simple coding exercise (what we do today)
We code a small set of quotes using:
1) manual coding (small groups)
2) AI-assisted coding (structured prompt)
Then we compare:
- agreements/disagreements,
- where AI overgeneralized,
- where humans disagreed (coding ambiguity).

---

## Mini-lab (Google Colab)

:::{admonition} Colab link
:class: tip
Replace this with your real link:

- Week 11 notebook (Research mapping + coding): https://colab.research.google.com/drive/PASTE_NOTEBOOK_ID
:::

### In-class checkpoints (Literature mapping)
1. Choose a research question (provided list or your own).
2. Create a search query list (5–10 keywords/phrases).
3. Collect 10–15 candidate papers:
   - title + year + venue/source
   - abstract (if available)
4. Screen down to 6–8 “most relevant” papers using explicit criteria.
5. Group the final set into 2–4 themes and write a 150–200 word map.

### In-class checkpoints (Qualitative coding)
6. Use a small set of interview/open-ended responses (provided).
7. Define a codebook with 4–6 codes (short definitions).
8. Code the same set manually (group work).
9. Run AI-assisted coding using your codebook and compare results.
10. Write 5–7 lines:
   - where AI matched humans,
   - where it differed,
   - what you would do next to improve reliability.

---

## Capstone Proposal v1 (due after class)

:::{admonition} Deliverable
:class: important
Submit a **Capstone Proposal v1** (1–2 pages) including:

1. **Research question** (one clear sentence)
2. **Motivation** (why it matters; 3–5 sentences)
3. **Mini literature map**
   - 6–8 relevant papers
   - grouped into 2–4 themes
   - 1–2 gaps / open questions
4. **Data plan**
   - dataset(s) you will use (e.g., OWID, business dataset, survey text, etc.)
   - unit of observation and time period
   - key variables and any expected limitations
5. **Method plan (choose ONE main method)**
   - regression OR clustering/PCA OR decision tree OR text analysis OR forecasting
6. **Verification plan**
   - at least 3 checks you will run (e.g., missingness, outliers, baseline model, train/test split by time, manual spot-check of sentiment, robustness plot)
7. **AI transparency plan**
   - how you will keep prompt/workflow logs
   - how you will verify AI outputs and avoid fake citations
:::

**Submission format:** PDF or Markdown export via LMS. Include a short prompt/workflow log if AI tools were used.

---

## AI check (responsible use for research)

:::{admonition} AI check
:class: caution
AI can support research, but you must:
1. Cite real sources (do not cite AI-generated fake references).
2. Verify summaries against abstracts (and full text when possible).
3. Keep a prompt/workflow log: search terms, screening criteria, and AI prompts.
4. Avoid “paper laundering” (presenting AI text as if you wrote it without acknowledgment).
:::

**Good prompt examples**
- “Propose search terms for studies on remote work and job satisfaction across industries.”
- “Given these abstracts, group them into themes and explain your grouping logic.”
- “Here is my codebook. Apply these codes to the following quotes and flag ambiguous cases.”

**Bad prompt examples**
- “Write my literature review with citations” (risk of fake citations and shallow synthesis)
- “Decide the themes and final conclusions for me” (outsourcing research judgment)

---

## Review questions (quiz / reflection)

1. What makes a research question “answerable” rather than just a broad topic?
2. What are two risks of AI-assisted literature summaries?
3. Why do we compare AI coding to manual coding?
4. What is one transparency practice you will use in your capstone?

:::{admonition} Reflection prompt
:class: note
In ~200 words: Propose one research question for your capstone.
Then list:
- 2 likely themes you expect to find in the literature,
- 1 possible data source,
- and 1 limitation you anticipate.
:::