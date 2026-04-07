# Lesson 10 — Time Series for Business/Economics
*(trend, seasonality, forecasting baselines, and honest evaluation)*

:::{admonition} Learning goals
:class: tip
By the end of Lesson 10, you should be able to:
1. Recognize why time ordering matters (why we do not randomly shuffle time series data).
2. Decompose a time series into **trend**, **seasonality**, and **noise** (conceptually and in code).
3. Build and evaluate simple forecasting baselines (naïve, seasonal naïve, moving average).
4. Use appropriate evaluation for forecasts (train/test split by time; MAE/RMSE/MAPE).
5. Communicate forecasts responsibly, including uncertainty, limitations, and “what could break this forecast.”
:::

## Why this matters (motivation)

Business and economics are full of time-indexed questions:
- How will sales evolve next month?
- Is inflation accelerating or stabilizing?
- Are customer visits seasonal?
- Did a policy change coincide with a shift in a trend?

Time series analysis gives a disciplined way to:
- describe patterns over time,
- and forecast future values with transparent assumptions.

:::{admonition} Reality check
:class: note
Forecasting is never “certain.” The goal is to make uncertainty visible and make forecasts useful for decisions.
:::

---

## Time series mindset: time is not just another variable

:::{admonition} Key idea
:class: important
Time series data violates a core assumption many models rely on: independence.
Observations close in time are often correlated.
Therefore:
- we split train/test **by time**,
- we avoid random shuffles,
- and we are careful about leakage from the future into the past.
:::

### Unit of observation (again)
Be explicit:
- daily sales (store-day),
- monthly inflation (country-month),
- quarterly GDP (country-quarter).

This determines what “seasonality” means and what forecasts are useful.

---

## Describing time series: the three components

A useful conceptual decomposition:
\[
y_t = \text{trend}_t + \text{seasonality}_t + \text{noise}_t
\]
(or multiplicative forms when growth is proportional).

### Trend
Long-run movement (growth/decline).

### Seasonality
Regular cycles (day-of-week, monthly, quarterly).

### Noise (irregular component)
Random shocks, measurement noise, one-off events.

:::{admonition} Common pitfall
:class: warning
People often interpret noise as “signal,” especially when they zoom too far in.
Smoothing can help, but smoothing can also hide real changes.
:::

---

## Forecasting as a benchmark game

:::{admonition} Key idea
:class: important
Most forecasting mistakes come from skipping baselines.
Before using advanced models, compare against simple baselines:
- naïve forecast (tomorrow = today)
- seasonal naïve (this month = same month last year)
- moving average
If your “fancy” model can’t beat a baseline, it isn’t useful.
:::

### Baseline 1: naïve
\[
\hat{y}_{t+1} = y_t
\]

### Baseline 2: seasonal naïve
\[
\hat{y}_{t+h} = y_{t+h-s}
\]
where \(s\) is seasonal period (e.g., 12 for monthly with yearly seasonality).

### Baseline 3: moving average
Forecast using recent average:
\[
\hat{y}_{t+1} = \frac{1}{k}\sum_{i=0}^{k-1} y_{t-i}
\]

---

## How to evaluate forecasts (practically)

### Time-based splitting
- Train on early period
- Test on later period (“future”)

Example:
- Train: 2010–2019
- Test: 2020–2023

### Metrics (choose one or two and interpret)
- **MAE** (mean absolute error): easy to interpret in units
- **RMSE** (root mean squared error): penalizes large errors more
- **MAPE** (percentage error): intuitive but unstable when values near zero

:::{admonition} Practical rule
:class: tip
For business/econ communication, MAE is often the easiest:
“On average, we miss by about ___ units.”
:::

---

## Visual communication for time series

Minimum set of plots that actually helps:
1. **Line plot** of the series (with clear time axis)
2. **Rolling average** (optional) to show trend
3. **Seasonality view** (e.g., month-of-year average or day-of-week average)
4. **Forecast plot**: actual vs predicted for the test window

:::{admonition} Common pitfall
:class: warning
Do not draw a forecast line without showing how it performed in a past test window.
Always show at least one out-of-sample evaluation.
:::

---

## Mini case options (choose one)

### Option A (business): sales forecasting
- Weekly or monthly sales
- Forecast next month/quarter
- Use seasonal naïve if clear seasonality

### Option B (economics): OWID time series
Use an OWID dataset that is time-indexed (country-year, country-month, etc.).
Examples:
- CO₂ emissions per capita
- GDP per capita
- energy consumption
- inflation (if available in your chosen dataset)

Focus: describe trend/seasonality and create a baseline forecast.

:::{admonition} Note on OWID frequency
:class: note
Many OWID indicators are annual (yearly). Seasonality is less relevant there.
If you want seasonality, use:
- monthly/weekly business data, or
- another source with monthly frequency.
Annual data still supports trend + forecasting baselines.
:::

---

## Mini-lab (Google Colab)

:::{admonition} Colab link
:class: tip
Replace this with your real link:

- Week 10 notebook (Time series & forecasting): https://colab.research.google.com/drive/PASTE_NOTEBOOK_ID
:::

### In-class checkpoints (data preparation)
1. Load a time series dataset with a clear time column.
2. Sort by time and set the time column correctly (datetime or integer year).
3. Plot the full time series and write one sentence describing the main pattern.

### In-class checkpoints (decomposition / pattern checks)
4. Compute a rolling average (choose a window and justify).
5. If seasonal frequency exists (e.g., monthly), compute a seasonal profile:
   - average by month-of-year or day-of-week.

### In-class checkpoints (forecast baselines)
6. Create a train/test split by time (e.g., last 20% as test).
7. Implement at least two baselines:
   - naïve
   - moving average OR seasonal naïve
8. Plot predictions vs actual in the test window.

### In-class checkpoints (evaluation)
9. Compute MAE and RMSE for each baseline on the test window.
10. Choose the “best” baseline and justify using both:
   - metric evidence, and
   - business reasoning (what errors matter?).

### Submission (after class)
- Colab link (view permission) or PDF export.
- Include:
  - your forecast plot,
  - metric table,
  - and a short “forecast memo” (headline + caveat + what could break it).

---

## AI check (responsible use for time series)

:::{admonition} AI check
:class: caution
AI can help with code scaffolding and plot suggestions, but you must:
1. Ensure train/test split respects time order (no leakage).
2. Verify calculations by checking small segments manually.
3. Avoid overconfident claims (“this will happen”)—use probabilistic language.
4. Record prompts and edits in your prompt/workflow log.
:::

**Good prompt examples**
- “Write Python code to split a time series into train/test by date and compute MAE.”
- “Implement a seasonal naïve forecast for monthly data with period 12.”
- “Suggest a clear plot to compare forecasts vs actual in the test period.”

**Bad prompt example**
- “Pick the best model and guarantee the forecast is accurate.”

---

## Review questions (quiz / reflection)

1. Why should train/test splits be done by time for forecasting?
2. What is a naïve forecast, and why is it a strong baseline?
3. When might MAPE be misleading?
4. Give one factor that could cause a forecast to fail (structural break).

:::{admonition} Reflection prompt
:class: note
In ~200 words: Describe your forecasting results:
- which baseline performed best (and why),
- one pattern you observed (trend/seasonality/noise),
- and one “forecast risk” (event or change that could break the pattern).
:::