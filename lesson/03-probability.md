# Lesson 3 — Probability Foundations in Context (with Simulation)

:::{admonition} Learning goals
:class: tip
By the end of Lesson 3, you should be able to:
1. Explain probability as a tool for **decision-making under uncertainty** (not just math).
2. Use simulation to approximate probabilities, expected values, and uncertainty.
3. Work with basic random variables (Bernoulli/binomial and “arrivals” intuition).
4. Communicate uncertainty clearly (what we know, what we don’t, and why).
:::

## Why this matters (motivation)

In business/economics, you rarely get certainty. You get **risk**:
- Will demand exceed capacity?
- Will a customer churn?
- Will a screening rule flag too many false positives?
- How much revenue variability should we expect next month?

Probability gives a disciplined way to think about these questions.

:::{admonition} Reality check
:class: note
Good decisions are often about managing the *distribution* of outcomes, not maximizing a single “best guess.”
:::

---

## Probability as a language for uncertainty

:::{admonition} Key idea
:class: important
Probability is a way to quantify uncertainty and compare strategies.
It helps you reason about:
- **likelihood** (“How often does this happen?”)
- **risk** (“How bad is it when it happens?”)
- **trade-offs** (“Which error is more costly?”)
:::

### Frequentist intuition (what we use today)
If you repeat a process many times (real or simulated),
probability is the **long-run proportion** of outcomes.

---

## Random variables (intuitive definitions)

:::{admonition} Key idea
:class: important
A **random variable** assigns a number to each uncertain outcome.
Examples:
- $X$ = number of customers who arrive in an hour
- $Y$ = whether a customer churns next month (1 = yes, 0 = no)
- $R$ = revenue from a marketing campaign
:::

### Two core quantities
- **Expected value**: the long-run average (“typical level”)
- **Variance / SD**: the typical spread (“how uncertain”)

---

## Common business distributions (light intuition)

### Bernoulli (yes/no outcomes)
- Example: customer churns (yes/no), email clicked (yes/no)

### Binomial (number of successes out of n)
- Example: out of 100 customers contacted, how many convert?

### Arrivals (count per time, intuition only)
- Example: customer arrivals per hour, website requests per minute
- We often model these as a “count process” with variability.

:::{admonition} Common pitfall
:class: warning
People confuse “expected value” with “most likely value.”
A distribution can have a mean that is not the most frequent outcome.
:::

---

## Simulation (Monte Carlo): your practical workhorse

:::{admonition} Key idea
:class: important
When exact calculation is hard (or when you want to test assumptions),
simulate the process many times and compute:
- estimated probabilities,
- expected outcomes,
- and uncertainty ranges.
:::

### Why simulation is powerful
- Works even when formulas are messy
- Makes assumptions explicit
- Helps build intuition quickly

---

## Mini case 1: Capacity planning (arrivals)

**Scenario:** A café has capacity for 40 customers per hour.  
You want to estimate: $P(\text{arrivals} > 40)$.

Steps:
1. Choose a simple model for arrivals (we’ll start with a reasonable assumption).
2. Simulate many hours.
3. Count the share of hours where arrivals exceed 40.

:::{admonition} Reality check
:class: note
The model is not “truth.” But it can still guide decisions if the assumptions are transparent and tested.
:::

---

## Mini case 2: Marketing conversion (binomial)

**Scenario:** Conversion rate is about 5%. You contact 200 customers.  
What is:
- expected conversions?
- probability conversions are below 5 (a disappointing campaign)?
- how variable is the outcome?

This is a binomial-style situation, and simulation gives quick answers.

---

## Mini-lab (Google Colab)

:::{admonition} Colab link
:class: tip
Replace this with your real link:

- Week 3 notebook (Probability + simulation): https://colab.research.google.com/drive/PASTE_NOTEBOOK_ID
:::

**In-class tasks (checkpoints)**
1. Simulate 10,000 Bernoulli trials and estimate a probability.
2. Simulate a binomial process (conversions out of $n$) and summarize the distribution.
3. Compute:
   - an estimated probability of a “bad outcome” (e.g., conversions ≤ threshold),
   - an expected value,
   - and a simple uncertainty summary (e.g., 5th–95th percentile).
4. Write a short interpretation in business language:
   - “What is likely?”
   - “What is risky?”
   - “What action would you take?”

**Submission**
- Colab link (view permission) or PDF export.

---

## AI check (responsible use for probability work)

:::{admonition} AI check
:class: caution
AI can help you draft simulation code, but you must:
1. Verify the logic by checking small cases (e.g., $n=10$) and sanity checks.
2. Confirm the distribution matches the story (e.g., conversions can’t be negative).
3. Record prompts and edits in your prompt/workflow log.
:::

**Good prompt examples**
- “Write Python code to simulate conversions with p=0.05 for n=200 repeated 10,000 times.”
- “How do I compute the probability conversions ≤ 5 from simulated results?”

**Bad prompt example**
- “Give me the final answer and interpretation without showing calculations.”

---

## Review questions (quiz / reflection)

1. What is the difference between **expected value** and **most likely outcome**?
2. Why can simulation be useful even when a formula exists?
3. In a conversion campaign, which risk matters more: unusually low conversions or unusually high conversions? Why?

:::{admonition} Reflection prompt
:class: note
In ~150 words: Describe one uncertainty problem in business/economics you care about. What would you simulate, and what decision would it inform?
:::