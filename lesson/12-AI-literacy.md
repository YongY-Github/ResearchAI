# Lesson 12 — AI Literacy: Prompting, Verification, Hallucinations, and Prompt Logs
*(from “asking questions” to reliable workflows; a taste of agentic loops)*

:::{admonition} Learning goals
:class: tip
By the end of Lesson 12, you should be able to:
1. Write effective prompts for analytics tasks (clarifying assumptions, requesting checks, and asking for alternatives).
2. Detect common failure modes of generative AI (hallucinations, fake citations, brittle code, overconfident claims).
3. Apply a verification workflow: sanity checks, reproducibility checks, and source checks.
4. Maintain a clear **prompt/workflow log** that documents how AI was used and how outputs were validated.
5. Use a simple “agent-like” loop (Plan → Execute → Check → Iterate) with **human-in-the-loop** control.
:::

## Why this matters (motivation)

By now you can:
- clean data,
- run regressions and clustering,
- build trees and text signals,
- and forecast with baselines.

Generative AI can help you do these tasks faster. But it can also:
- produce plausible but wrong explanations,
- invent references,
- write code that runs but answers the wrong question,
- or encourage overconfident conclusions.

This week makes sure you can use AI tools **responsibly and effectively**—in a way that faculty (and future employers) will accept.

:::{admonition} Reality check
:class: note
AI outputs are not evidence. They are suggestions that must be verified.
Your credibility comes from verification, transparency, and careful language.
:::

---

## Part A — What “AI literacy” means in this course

:::{admonition} Key idea
:class: important
AI literacy is the ability to:
1. Ask good questions (prompts)
2. Evaluate outputs critically (verification)
3. Document use transparently (prompt/workflow logs)
4. Communicate uncertainty responsibly (no overclaiming)
:::

### What AI is good at (in our workflow)
- drafting code scaffolds
- suggesting EDA checks and chart types
- summarizing text (when you cross-check)
- proposing alternative explanations or sensitivity checks
- turning messy notes into structured outlines (not final content)

### What AI is bad at (common risks)
- factual reliability without sources
- citations (often hallucinated)
- domain-specific judgment
- hidden assumptions in code
- causal claims without design
- overly confident “final answers”

---

## Part B — Prompting patterns that produce better work

### Pattern 1: Ask for assumptions first
Instead of:
> “Analyze this dataset.”

Try:
> “What assumptions do you need to make to analyze this dataset responsibly? List them and suggest checks.”

### Pattern 2: Ask for a plan, not a final product
> “Propose a step-by-step workflow (EDA → cleaning → model → diagnostics → communication) for this question.”

### Pattern 3: Ask for checks and failure modes
> “List the top 5 ways this analysis could be misleading and how to test each.”

### Pattern 4: Ask for alternatives
> “Give two alternative model specifications and explain when each is appropriate.”

### Pattern 5: Force careful language
> “Write conclusions using association language and include one limitation and one potential confounder.”

:::{admonition} Common pitfall
:class: warning
A prompt that requests “a perfect answer” encourages hallucination.
Prompts that request assumptions, steps, and checks encourage reliable work.
:::

---

## Part C — Verification: a practical checklist

:::{admonition} Key idea
:class: important
Verification is not optional. It is a workflow.
We verify outputs at three levels:
1. **Code verification**: does it do what it claims?
2. **Data verification**: are the data and units correct?
3. **Claim verification**: do results support the conclusion?
:::

### 1) Code verification (fast sanity checks)
- run on a small subset (e.g., first 100 rows)
- check shapes and dtypes before/after transformations
- compare results with a simpler method (baseline)
- print intermediate values (not only final plots)

### 2) Data verification
- confirm units (percent vs fraction; dollars vs thousands)
- check missingness patterns
- check ranges (impossible values)
- confirm time ordering (for forecasts)

### 3) Claim verification
- is the conclusion consistent with the chart/table?
- are you accidentally implying causality?
- does the result depend on one outlier or one subgroup?
- can you reproduce it from scratch?

---

## Part D — Hallucinations: what they look like in practice

### Hallucination type 1: Fake citations
AI may produce:
- plausible author names,
- plausible journals,
- and plausible titles
that do not exist.

**Rule:** only cite papers you can actually locate and verify.

### Hallucination type 2: Wrong-but-plausible code
AI code may:
- run but use the wrong column,
- silently drop missing values,
- shuffle time series,
- or leak test information into training.

### Hallucination type 3: Overconfident interpretation
AI often writes strong language:
- “X causes Y”
- “the model proves”
- “this confirms”
even when the analysis only supports association.

:::{admonition} Practical rule
:class: tip
If you cannot point to a table/plot and explain the logic yourself, you cannot submit the claim.
:::

---

## Part E — Prompt & Workflow Logs (the course standard)

:::{admonition} Key idea
:class: important
A prompt/workflow log is a short record showing:
- what you asked AI,
- what it returned,
- what you used vs changed,
- and how you verified it.
This protects you and makes grading fair.
:::

### Minimum required fields
1. Task context (what you were trying to do)
2. Prompt(s)
3. AI output snippet (short)
4. What you changed (edits)
5. Verification steps (sanity checks)
6. Final decision (what you accepted or rejected)

:::{admonition} Suggested format
:class: note
You can keep the log inside:
- a Markdown section of your notebook, or
- a separate one-page document attached to your submission.
:::

---

## Part F — A “taste” of agentic workflows (human-in-the-loop)

Many people use the term “agentic AI” to mean AI systems that:
- plan tasks,
- execute steps,
- check results,
- and iterate toward a goal.

In this course, we use a safe version:
**Plan → Execute → Check → Iterate**, where *you* execute the steps and approve changes.

:::{admonition} Agent-like loop (safe version)
:class: important
1. **Plan:** ask AI for an analysis plan + checks
2. **Execute:** you run the plan in Colab
3. **Check:** ask AI to review outputs + you verify with sanity checks
4. **Iterate:** refine (change model, add plot, revise interpretation)
:::

---

## Mini-lab (Google Colab)

:::{admonition} Colab link
:class: tip
Replace this with your real link:

- Week 12 notebook (AI literacy + verification): https://colab.research.google.com/drive/PASTE_NOTEBOOK_ID
:::

### In-class checkpoints (prompting)
1. Choose one task from your capstone workflow:
   - EDA checklist for your dataset
   - cleaning plan
   - regression specification
   - clustering plan
   - forecasting baseline plan
2. Write a “bad prompt” and a “good prompt” for the same task.
3. Compare outputs and explain why the “good prompt” is better.

### In-class checkpoints (verification)
4. Take one AI-generated code snippet and run it.
5. Perform at least 3 verification checks:
   - check shapes/dtypes
   - check missingness changes
   - check basic summary stats
   - compare to a baseline result
6. Identify at least one failure or risk (even if minor) and fix it.

### In-class checkpoints (hallucination hunt)
7. You will be given a short AI-generated paragraph (or code) that contains 2–3 issues.
8. Find and label issues (fake citation? wrong claim? leakage? wrong column?).
9. Rewrite the paragraph with correct language and at least one caveat.

### In-class checkpoints (agent-like loop)
10. Run one full loop:
   - AI proposes a plan
   - you execute in Colab
   - AI reviews
   - you implement one improvement

**Submission (after class)**
- Colab link (view permission) or PDF export.
- Include a prompt/workflow log with your prompts, edits, and verification steps.

---

## AI check (meta)

:::{admonition} AI check
:class: caution
This week’s goal is not “better AI prompts.”
It is “better verification habits.”
Your grade depends on:
- the quality of checks you ran,
- and the transparency of your documentation.
:::

---

## Review questions (quiz / reflection)

1. Name three common AI failure modes in data analysis.
2. What is one verification check you should always do after cleaning data?
3. Why is it risky to ask AI for citations?
4. What is the safe “agent-like loop” used in this course?

:::{admonition} Reflection prompt
:class: note
In ~200 words: Describe one time AI output could have misled you in your capstone.
What verification step would catch the problem, and how would you document it?
:::