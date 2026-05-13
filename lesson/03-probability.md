---
kernelspec:
  name: jb2-env
  display_name: Python (jb2-env)
---

# Lesson 3 — Probability Foundations in Context

:::{admonition} Learning goals
:class: tip

By the end of this lesson, you should be able to:

1. Explain probability as a way to reason about uncertainty.
2. Use simulation to build intuition about probability distributions.
3. Use AI tools to help generate and modify Python code.
4. Interpret probabilities using visualization and relative frequencies.
5. Reflect critically on AI-generated outputs and workflow.

:::

:::{admonition} AI tools
:class: note

Any major LLM (Large Language Model) is acceptable for this course.

Examples include:
- ChatGPT,
- Claude,
- Gemini,
- Copilot,
- DeepSeek,
- and similar AI assistants.

However, ChatGPT is recommended as the default option because:
- it can generate Python code,
- explain concepts interactively,
- and (in some versions) execute Python code directly.

The goal of the course is not loyalty to a particular tool.

The goal is learning:
- analytical reasoning,
- workflow design,
- verification,
- and responsible AI-assisted research.

:::

---

# 1.0 Probability as a Language for Uncertainty

Probability helps us reason about uncertainty.

Examples:
- Will a customer make a purchase?
- How many users will visit a website?
- How variable are human heights?
- How likely is an unusually high or low outcome?

:::{admonition} Key idea
:class: important

Probability is a way to quantify uncertainty and compare outcomes.

:::

One useful interpretation is the **frequentist interpretation**:

If we repeat a process many times,
probability is the long-run proportion of outcomes.
Simulation allows us to approximate these long-run proportions computationally.

---

# 2.0 Human Heights and the Normal Distribution

Suppose human heights are approximately Normally distributed with:

```{math}
:enumerated: false
\mu = 170, \quad \sigma = 5
```

where:
- $\mu$ is the mean,
- $\sigma$ is the standard deviation.

This means:
- most observations should cluster near the mean,
- while extremely high or low values should be relatively rare.

---

## 2.1 AI Prompt for Python Code

Suppose we want to simulate human heights using Python.

One possible prompt is:

```text
Write Python code to:
- simulate 400 human heights,
- assuming heights follow a normal distribution with:
    mean = 170 cm
    standard deviation = 5 cm

Then:
1. print a few simulated heights,
2. plot a histogram using relative frequencies,
3. compute the proportion of heights between 170 and 175 cm.
```

:::{admonition} Important
:class: caution

Prompting is not magic wording.

Prompting is a form of structured reasoning:
- describing the problem,
- specifying the task,
- and communicating what output we want.

:::

---

## 2.2 AI-Generated Python Code

```{code-cell} python

import numpy as np
import matplotlib.pyplot as plt

# Set seed for reproducibility
np.random.seed(1001)

# Simulate heights
heights = np.random.normal(
    loc=170,
    scale=5,
    size=400
)

# Show first 20 heights
print(heights[:20])

print("...")

# Show last 20 heights
print(heights[-20:])

```

---

## 2.3 Histogram of Simulated Heights

```{code-cell} python

plt.hist(
    heights,
    bins=20,
    density=True,
    edgecolor='black'
)

plt.xlabel("Height (cm)")
plt.ylabel("Relative Frequency")
plt.title("Simulated Human Heights")

plt.show()

```

:::{admonition} Empirical Rule (68–95–99.7 Percent Rule)
:class: important

For a Normal distribution:

- about 68% of observations lie within 1 standard deviation of the mean,
- about 95% lie within 2 standard deviations,
- about 99.7% lie within 3 standard deviations.

This helps us understand:
- what is “typical,”
- what is “unusual,”
- and why extreme outcomes are relatively rare.

:::

---

## 2.4 Estimating a Probability from Simulation

We can estimate probabilities using simulated data.

For example:

> What proportion of individuals have heights between 170 and 175 cm?

```{code-cell} python

prop = np.mean(
    (heights >= 170) &
    (heights <= 175)
)

print("Proportion between 170 and 175 cm:", prop)

```

> Does the probability makes sense? Think about the empirical rule.


---

# 3.0 Reflection

Think about the following questions:

1. Why are most observations close to the mean?
2. Why are extremely high or low heights relatively rare?
3. What is the proportion between 165 and 175 cm for the above heights example? Verify this with Python code.
4. What happens if the standard deviation increases?
5. What happens if the sample size increases?
6. What did simulation help you understand about probability?

Hint: Try changing

```python
    scale=10,
```

```python
    size=1000
```

The distribution above is an example of a **Normal distribution**.

---

# 4.0 The Normal Distribution

:::{admonition} Example AI prompt for Explainer
:class: note

```text
Explain the Normal distribution in simple language suitable for beginner students.

Then provide:
1. a short intuitive explanation,
2. the Normal distribution formula in LaTeX,
3. explanations of:
   - mean,
   - standard deviation,
4. and some real-world example.
```

:::

The Normal distribution is one of the most important probability distributions in statistics and data science.

It is:
- symmetric,
- bell-shaped,
- and centered around a mean value.

Many real-world quantities are approximately Normally distributed, including:
- human heights,
- exam scores,
- measurement errors,
- and some economic variables.

The probability density function $PDF$ is:

```{math}
:enumerated: false
f(x)=\frac{1}{\sigma\sqrt{2\pi}}
\exp\left(
-\frac{(x-\mu)^2}{2\sigma^2}
\right)
```

where:
- $\mu$ is the mean (center of the distribution),
- $\sigma$ is the standard deviation (spread of the distribution).

:::{admonition} Key idea
:class: important

The mean determines the location of the distribution,
while the standard deviation determines how spread out the observations are.

:::

---

## 4.1 The Standard Normal Distribution

The **standard normal distribution** is a special case with:

```{math}
:enumerated: false
\mu = 0, \quad \sigma = 1
```

The Normal distribution appears frequently in:
- economics,
- finance,
- machine learning,
- and scientific measurement.

The standard normal distribution is useful because many probability calculations can be converted into this standardized form.

---

# 5.0 Coin Tossing and Bernoulli Trials

Suppose:
- Heads = 1
- Tails = 0

Each coin toss has:
- two possible outcomes,
- equal probability,
- and independent trials.

This type of process is called a **Bernoulli trial**.

---

## 5.1 AI Prompt for Python Code

```text
Write Python code to:
- simulate 100 fair coin tosses,
- display the number of heads and tails,
- and plot a histogram using relative frequencies.
```

---

## 5.2 AI-Generated Python Code

```{code-cell} python

# Simulate 100 fair coin tosses
tosses = np.random.choice([0,1], size=100)

# Count outcomes
print("Heads:", sum(tosses))
print("Tails:", 100 - sum(tosses))

```

---

## 5.3 Histogram of Coin Tosses

```{code-cell} python

plt.hist(
    tosses,
    bins=[-0.5,0.5,1.5],
    density=True,
    edgecolor='black'
)

plt.xticks([0,1], ['Tails','Heads'])

plt.xlabel("Outcome")
plt.ylabel("Relative Frequency")
plt.title("Histogram of Coin Tosses")

plt.show()
```

---

## 5.4 AI Prompt

```text
Explain the Binomial distribution in simple language suitable for beginner students.

Then provide:
1. a short intuitive explanation,
2. the Binomial probability mass function in LaTeX,
3. explanations of:
   - n
   - k
   - p
4. one real-world example.
```

## 5.5 The Binomial Distribution

The Binomial distribution models the number of successes obtained from repeated independent trials.

Examples include:
- number of customers who make a purchase,
- number of students who pass an exam,
- number of defective products,
- or number of heads in repeated coin tosses.

Suppose:
- each trial has only two outcomes,
  - success or failure,
- the probability of success remains constant,
- and trials are independent.

The Binomial distribution tells us:

> “What is the probability of getting exactly $k$ successes out of $n$ trials?”

The probability mass function is:

```{math}
:enumerated: false
P(X=k)=\binom{n}{k}p^k(1-p)^{n-k}
```

where:
- $n$ = number of trials,
- $k$ = number of successes,
- $p$ = probability of success on each trial.

:::{admonition} Key idea
:class: important

The Binomial distribution models repeated yes/no type outcomes,
such as:
- purchase or not,
- pass or fail,
- click or no click,
- heads or tails.

:::

---

## 5.6 Example: Marketing Conversion

Suppose:
- a company emails 200 customers,
- each customer has a 5% probability of purchasing.

The Binomial distribution can model:
- the probability of exactly 10 purchases,
- or the probability of unusually low conversions.

---

# 6.0 Other Useful Probability Distributions

## 6.1 Exponential Distribution

The Exponential distribution models waiting times between random events.

Examples include:
- time until the next customer arrives,
- waiting time between website visits,
- time until machine failure,
- or time between phone calls.

The probability density function is:

```{math}
:enumerated: false
f(x)=\lambda e^{-\lambda x}, \quad x \geq 0
```

where:
- $\lambda$ is the rate parameter,
- larger $\lambda$ means events occur more frequently.

:::{admonition} Key idea
:class: important

The Exponential distribution models waiting time.

If events occur frequently,
waiting times tend to be shorter.

:::

Example prompt:

```text
Write Python code to generate and plot an Exponential distribution with different parameters.
```

---

## 6.2 The Poisson Distribution

The Poisson distribution models the number of events occurring within a fixed interval.

Examples include:
- number of customer arrivals,
- number of website visits per minute,
- number of accidents per day,
- or number of emails received in an hour.

The probability mass function is:

```{math}
:enumerated: false
P(X=k)=\frac{e^{-\lambda}\lambda^k}{k!}
```

where:
- $\lambda$ is the average number of events,
- $k$ is the number of observed events.

:::{admonition} Key idea
:class: important

The Poisson distribution models counts of events.

Larger values of $\lambda$ imply more frequent events on average.

:::

Example prompt:

```text
Write Python code to simulate a Poisson distribution with different values of lambda and plot histograms.
```

---

# 7.0 Reflection on AI Workflow

AI can help us:
- generate code,
- explain concepts,
- and accelerate experimentation.

However, humans remain responsible for:
- interpretation,
- verification,
- and reasoning.

:::{admonition} Key takeaway
:class: important

AI reduces friction,
but does not replace thinking.

:::

---

# 8.0 Homework

1. Go through the Lesson again, running the code in Goolge Colab.
2. Make sure you fully understand the empirical rule.
3. Explore the Exponential distribution.
4. Explore the Poisson distribution.
6. Save useful prompts into:

```text
prompts/useful_prompts.md
```

5. Write a short reflection in:

```text
personal_log.md
```
---

# 9.0 Resources

:::{admonition} Colab link
:class: tip
- [Accompanying Google Colab: Week 3](https://colab.research.google.com/drive/1vifgaEUWu0JbBKNml9G0kxTdyOB_Dk9e?usp=sharing)
:::

[Ch6 Normal Disctibution](https://yongy-github.github.io/Stats101/Ch6.html)

## Optional
[Ch8 Binomial and Poisson Distribution](https://yongy-github.github.io/Stats101/Ch9.html)
[Ch9 Uniform and Exponential Probability Distribution](https://yongy-github.github.io/Stats101/Ch10.html)
