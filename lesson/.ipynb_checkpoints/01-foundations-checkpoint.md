# Lesson 1 — Where Analytics & AI/ML/DS Fit in Business

:::{admonition} Learning goals
:class: tip
By the end of Lesson 1, you should be able to:
1. Explain what is **AI** and **Gen AI**. 
2. Explain the differences between **Analytics**, **Data Science**, **AI**, and **Machine Learning (ML)**.
3. Identify the **unit of observation**, **target/outcome**, and **features** in a dataset (using churn)
4. Describe a full workflow: **question → data → EDA → model → interpretation → decision**.
5. Set up and run a minimal Colab notebook (load data, preview, simple counts)
:::

## Why this matters

Many “AI projects” fail for simple reasons: unclear questions, weak data, and over-confident interpretation.
This course treats AI as part of an **evidence workflow**, not a shortcut.

:::{admonition} Reality check
:class: note
A powerful model cannot rescue a weak question, poor data, or unclear interpretation.
:::

## What is AI, Gen AI?

**Artificial Intelligence (AI):** Systems that can perform tasks that normally require human intelligence—such as recognizing patterns, making predictions, or recommending actions—by processing inputs (data, text, images) to produce outputs that support decisions.

**Generative AI:** A type of AI that can generate **new** content (text, code, images, etc.). 

In this course, AI is treated as a tool within an evidence workflow (data → analysis → evaluation → communication) and will be used mainly as an **assistant** for tasks like planning an analysis, drafting explanations, and scaffolding code. Outputs must be verified (run the code, check the data, confirm sources) and should not be copied into assignments without understanding and proper disclosure where required.

## The big picture: Analytics vs DS vs AI vs ML

:::{admonition} Key idea
:class: important
- **Analytics**: Describing and explaining data to support decisions (dashboards, KPIs, A/B testing).
- **Data Science**: Building reproducible data workflows and products (pipelines, prediction services).
- **AI**: A broad goal — machines performing tasks that normally require “intelligence.”
- **ML**: Methods that learn patterns from data (prediction, classification, clustering).
:::

### A simple map (think tasks)
- **Describe**: What happened? (EDA, visualization)
- **Explain**: Why might it have happened? (regression, causal thinking)
- **Predict**: What will happen next? (supervised ML)
- **Segment**: Are there different types of users/markets? (unsupervised ML)

:::{admonition} Key idea
:class: important
- **Supervised learning** uses labeled outcomes (e.g., churn = yes/no; sales next month).
- **Unsupervised learning** finds structure without labeled outcomes (e.g., customer segments).
:::

Later we’ll cover two learning modes: prediction with labels and pattern-finding without labels

## Mini example: a churn workflow (end-to-end)

1. **Question:** Who is likely to churn next month?
2. **Data:** usage, plan type, support tickets, past churn.
3. **EDA:** churn rates by segment; distribution plots.
4. **Model:** start simple (logistic regression), then consider trees if needed.
5. **Interpretation:** what features matter? what are the limitations?
6. **Decision:** targeted retention + measurement plan.

## Mini-lab (Google Colab)

:::{admonition} Colab link
:class: tip
- Week 1 notebook: https://colab.research.google.com/drive/17ZU_Hh7U5HzJaQUG9oL8g8rvMaP1iBsu?usp=sharing
:::

Churn Data: https://drive.google.com/file/d/1CcOCXyGM9GLFmzFbKfmIhioM-yLDkDqU/view?usp=sharing

<!--
**Submission (after class):**
- Share the Colab link (view permission) **or** export to PDF.
- Upload via LMS.

## AI check (responsible use)

:::{admonition} AI check
:class: caution
If you use an AI tool this week:
1. Keep a **prompt/workflow log** (what you asked, what you used, what you changed).
2. Verify code and claims by running the notebook and checking sources.
3. You must be able to explain your final result in your own words.
:::
-->

## Review questions (quiz / reflection)
1. Give one example each of analytics, data science, and ML in business.
2. What is the difference between supervised and unsupervised learning?
3. Why can a strong model still lead to bad decisions?

:::{admonition} Reflection prompt
:class: note
In ~150 words: What kind of business/econ question would you like to analyze this semester, and why?
:::
