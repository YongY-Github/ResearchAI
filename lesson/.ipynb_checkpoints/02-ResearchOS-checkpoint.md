---
kernelspec:
  name: jb2-env
  display_name: Python (jb2-env)
---

# Lesson 2A — Building a Research Workflow (Research OS)

:::{admonition} Learning goals
:class: tip

By the end of this lesson, you should be able to:

1. Explain why workflow and organization matter in AI-assisted research.
2. Create a simple directory structure for analytical projects.
3. Maintain:
   - prompt logs,
   - workflow notes,
   - and reflection logs.
4. Understand the idea of a lightweight “Research OS”.
5. Treat AI as part of a reproducible analytical workflow rather than an answer machine.

:::

---

# Why This Matters

Modern analytical work is increasingly workflow-driven.

In practice, research and analytics involve:
- collecting data,
- testing ideas,
- revising prompts,
- debugging code,
- interpreting results,
- documenting decisions,
- and revisiting earlier work.

Without organization, students often:
- lose useful prompts,
- forget what worked,
- repeat mistakes,
- restart workflows,
- and struggle to reproduce results later.

:::{admonition} Key idea
:class: important

Good workflow matters more than fancy tools.

:::

---

# AI Changes Workflow

AI tools can:
- generate code,
- explain concepts,
- summarize information,
- and accelerate experimentation.

However, AI also increases the importance of:
- verification,
- documentation,
- and organization.

:::{admonition} Reality check
:class: note

If you cannot explain:
- where your result came from,
- what prompt produced it,
- or what changes you made,

then your workflow is not reproducible.

:::

---

# The Research OS Idea

In this course, we gradually build a lightweight:

# “Research Operating System” (Research OS)

The goal is not perfection.

The goal is to create:
- continuity,
- organization,
- and reflective workflow habits.

The Research OS acts as:
- a memory system,
- a workflow system,
- and a research notebook.

---

# An Example Directory Structure

Create a folder called:

```text
ResearchAI/
```

Suggested structure:

```text
ResearchAI/

├── researchAI_brain.md
├── personal_log.md

├── prompts/
│   ├── useful_prompts.md
│   └── failed_prompts.md

├── datasets/
│   ├── raw/
│   └── cleaned/

├── notebooks/
│   ├── class01/
│   ├── class02/
│   └── class03/

├── exercises/
│   ├── class01/
│   ├── class02/
│   └── class03/

├── projects/

│   └── capstone_project/
│       ├── project_brain.md
│       ├── data/
│       ├── notebooks/
│       ├── outputs/
│       ├── references/
│       └── draft/

└── archive/
```

We will start slow and build up later on a need basis.

:::{admonition} Important
:class: caution

The exact structure is flexible.

The purpose is to build:
- consistency,
- organization,
- and workflow discipline.

:::

---

# The Two Core Files

## 1. researchAI_brain.md

This is your:
- evolving knowledge system,
- workflow notebook,
- and idea repository.

It may include:
- useful prompts,
- code snippets,
- workflow ideas,
- debugging notes,
- AI limitations,
- and important lessons.

Think of this as:

> “What do I want my future self to remember?”

---

# Example: researchAI_brain.md

```text
# Current Focus

# Important Lessons

# Useful Workflows

# AI Limitations Observed

# Good Prompt Patterns

# Mistakes to Avoid

# Interesting Datasets

# Research Ideas

# Questions to Explore

# Weekly Reflection
```

:::{admonition} Key idea
:class: important

Your brain file is not a polished report.

It is a living workflow system that evolves over time.

:::

---

## 2. personal_log.md

This is your:
- reflection journal,
- experiment log,
- and learning diary.

You can record:
- what you learned,
- what confused you,
- what worked,
- what failed,
- and what you want to explore later.

:::{admonition} Key idea
:class: important

Reflection is part of analytical thinking.

:::

---

# Example: personal_log.md

```text
# Lesson 2 Reflection (2026-05-13)

## What I learned
- how to inspect missing values,
- and why EDA matters before modeling.

## What confused me
- interpreting skewed distributions.

## What tools I explored
- DataMiner
- Orange

## Prompt experiments
- “Suggest 5 EDA checks for customer transaction data.”

## Things I want to explore later
- interactive plots,
- customer segmentation.

## Challenges

## Reflection
```

:::{admonition} Important
:class: caution

Do not aim for perfection.

The purpose of the log is:
- continuity,
- reflection,
- and gradual improvement.

:::

---

(OPTIONAL)

# Example: useful_prompts.md

## Useful EDA Prompt

Suggest:
- useful summary statistics,
- possible missing value checks,
- and appropriate visualizations

for a dataset containing:
- customer transactions,
- dates,
- categories,
- and revenue.

---

# Prompting as Structured Reasoning

:::{admonition} Key idea
:class: important

Prompting is not magic wording.

Prompting is a form of structured reasoning:
- describing the task,
- specifying the goal,
- and communicating useful context.

:::

Good prompts usually include:
- the task,
- relevant context,
- desired output,
- and constraints.

---

# AI Workflow Example

A typical workflow in this course might look like:

```text
question
→ prompt
→ AI-generated code
→ run code
→ inspect output
→ debug/revise
→ interpretation
→ reflection
→ save useful workflow
```

This process is iterative.

Researchers constantly revise:
- prompts,
- assumptions,
- code,
- and interpretations.

---

# Versioning and Iteration

Good analytical work evolves over time.

Do not expect:
- first prompts,
- first code,
- or first interpretations

to be perfect.

:::{admonition} Important
:class: caution

Iteration is normal.

Professional analytical workflows involve:
- testing,
- revising,
- debugging,
- and refining.

:::

---

# Responsible AI Use

AI can accelerate:
- coding,
- explanation,
- brainstorming,
- and experimentation.

However:
- AI can hallucinate,
- generate incorrect code,
- misinterpret outputs,
- or produce misleading explanations.

Humans remain responsible for:
- verification,
- interpretation,
- and judgment.

---

# Reflection Questions

1. Why does workflow organization matter more in the AI era?
2. What kinds of things should be saved in a prompt log?
3. Why is reflection useful in analytical work?
4. What might happen if analytical workflows are poorly documented?

---

# Homework

1. Create your:
   - `ResearchAI/` folder,
   - `researchAI_brain.md`,
   - and `personal_log.md`.

2. Add:
   - one useful prompt,
   - one reflection,
   - and one workflow insight.

3. Write a short reflection:

```text
What kind of workflow system do you think would help you most this semester?
```