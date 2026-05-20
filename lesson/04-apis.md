# Lesson 4 — Data Collection: Getting Data into Colab (Finance, WDI, OWID, News)

*(choose-one-track lab + course-standard sanity checks + data source note)*

:::{admonition} Learning goals
:class: tip
By the end of Lesson 4, you should be able to:
1. Explain the difference between **files**, **APIs**, and **web scraping** (and when each is appropriate).
2. Load data into Google Colab from at least one source (choose-one-track):
   - **yfinance** (market time series),
   - **World Bank WDI** (cross-country indicators),
   - **Our World in Data (OWID)** (public global datasets),
   - **News feed API (GDELT)** (for later text/NLP work).
3. Apply course-standard **sanity checks** (shape, missingness, and time window when relevant).
4. Produce **one plot** and **one summary table** that answer a clear question.
5. Write a short **Data Source Note** (source, access method, date accessed, variables used, filters, and one limitation).
:::

## Why this matters

Analytics and AI are only as good as the **data pipeline** behind them.
A large part of professional work is:
- finding the right dataset,
- documenting what it is and where it came from,
- and ensuring you can reproduce the same results later.

:::{admonition} Reality check
:class: note
If you cannot clearly explain where the data came from, you cannot defend the analysis.
:::

---

## Three ways to get data (concept map)

:::{admonition} Key idea
:class: important
1. **Download a file** (CSV/Excel): simplest; best when data is stable.
2. **Use an API**: structured access; best for reproducibility and automation.
3. **Web scraping**: last resort; fragile and can raise legal/ethical issues.
:::

---

## Today’s lab format: choose ONE track

You do **not** need to run everything. Choose **one** source and produce the same outputs.

**Track A:** Yahoo Finance (market time series)  
**Track B:** World Bank WDI (cross-country indicators)  
**Track C:** Our World in Data (OWID Grapher CSV)  
**Track D:** News feed API (GDELT, no API key)

:::{admonition} Submission (today)
:class: important
Submit:
1) **One plot** + **one summary table** (from your chosen track)  
2) **Data Source Note** (template at the end)  
3) **One limitation/caveat**  
If you use any AI tool, include the **Prompt & Workflow Log** section.
:::

---

## Colab notebook (live)

Use the class notebook here:

- https://drive.google.com/file/d/1oZC6dHbWaWoC1MiG4Bt-_vG_okcvbMHR/view?usp=sharing

---

## Course-standard sanity checks (use after loading data)

These checks help you avoid common mistakes:
- wrong types,
- unexpected missingness,
- wrong date range.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

pd.set_option("display.max_columns", 50)

def sanity_checks(df, time_col=None, name="df"):
    print(f"--- {name} ---")
    print("shape:", df.shape)
    print("columns:", list(df.columns)[:12], "..." if len(df.columns) > 12 else "")
    print("\nmissingness (top 10):")
    miss = df.isna().mean().sort_values(ascending=False).head(10)
    print(miss)
    if time_col is not None and time_col in df.columns:
        print("\n time_col:", time_col)
        print(" min:", df[time_col].min(), " max:", df[time_col].max())
    print("--------------\n")
````

---

# Track A — Yahoo Finance (yfinance)

**Use case:** market data time series (stocks/ETF/FX/crypto)
**Deliverable idea:** plot close price; compute a simple summary table (monthly average close).

```python
!pip -q install yfinance
import yfinance as yf
```

```python
ticker = "AAPL"   # try: "MSFT", "TSLA", "SPY", "BTC-USD", "^GSPC"
start_date = "2023-01-01"
end_date   = "2024-12-31"

px = yf.download(ticker, start=start_date, end=end_date, progress=False).reset_index()
px.head()
```

```python
sanity_checks(px, time_col="Date", name="prices")
```

**Plot (required):**

```python
plt.figure()
plt.plot(px["Date"], px["Close"])
plt.title(f"{ticker} Close Price")
plt.xlabel("Date")
plt.ylabel("Close")
plt.show()
```

**Table (required): monthly average close**

```python
px["month"] = px["Date"].dt.to_period("M").astype(str)
monthly = px.groupby("month")["Close"].mean().reset_index().rename(columns={"Close": "avg_close"})
monthly.head(10)
```

:::{admonition} Common pitfall
:class: warning
Market data can differ across providers (adjusted vs raw prices, splits/dividends, ticker conventions).
Always record the ticker and the exact date range.
:::

---

# Track B — World Bank WDI (wbgapi)

**Use case:** cross-country indicators (GDP per capita, inflation, population, etc.)
**Deliverable idea:** plot 3 countries over time + a simple “latest year” table.

```python
!pip -q install wbgapi
import wbgapi as wb
```

```python
indicator = "NY.GDP.PCAP.CD"  # try: "FP.CPI.TOTL.ZG" (inflation), "SP.POP.TOTL" (population)
countries = ["JPN", "THA", "USA"]  # ISO3 codes
years = range(2000, 2024)

wdi = wb.data.DataFrame(indicator, countries, time=years).reset_index()
wdi = wdi.rename(columns={"economy": "country_code", "time": "year", indicator: "value"})
wdi.head()
```

```python
sanity_checks(wdi, time_col="year", name="wdi")
```

**Plot (required):**

```python
plt.figure()
for c in countries:
    tmp = wdi[wdi["country_code"] == c].sort_values("year")
    plt.plot(tmp["year"], tmp["value"], label=c)

plt.title(f"WDI indicator: {indicator}")
plt.xlabel("Year")
plt.ylabel("Value")
plt.legend()
plt.show()
```

**Table (required): latest year value**

```python
latest = wdi.sort_values("year").groupby("country_code").tail(1)[["country_code", "year", "value"]]
latest
```

:::{admonition} Common pitfall
:class: warning
Cross-country indicators are sensitive to measurement differences and revision schedules.
Always record the indicator code and define the unit of comparison clearly.
:::

---

# Track C — Our World in Data (OWID Grapher CSV)

**Use case:** curated public datasets with consistent country/time structure
**Deliverable idea:** plot 3 countries + “latest year” table.

```python
url = "https://ourworldindata.org/grapher/co2-per-capita.csv"  # you can change the OWID slug
owid = pd.read_csv(url)
owid.head()
```

```python
sanity_checks(owid, time_col="Year", name="owid")
```

```python
countries = ["Japan", "Thailand", "United States"]  # adjust as needed
value_col = [c for c in owid.columns if c not in ["Entity", "Code", "Year"]][0]  # auto-pick
owid_sub = owid[owid["Entity"].isin(countries)].copy()
```

**Plot (required):**

```python
plt.figure()
for c in countries:
    tmp = owid_sub[owid_sub["Entity"] == c].sort_values("Year")
    plt.plot(tmp["Year"], tmp[value_col], label=c)

plt.title(f"OWID: {value_col}")
plt.xlabel("Year")
plt.ylabel(value_col)
plt.legend()
plt.show()
```

**Table (required): latest year by country**

```python
latest = (owid_sub.sort_values("Year")
          .groupby("Entity").tail(1)[["Entity", "Year", value_col]]
          .rename(columns={"Entity": "country"}))
latest
```

:::{admonition} Tip
:class: tip
Many OWID datasets are annual. That’s fine for trend comparisons and later forecasting baselines.
:::

---

# Track D — News feed API (GDELT, no key)

**Use case:** build a small headline dataset for later **text-as-data/NLP** work
**Deliverable idea:** 50 recent articles on a topic + basic counts by language/country.

```python
import requests

query = "inflation"  # try: "electric vehicles", "unemployment", "AI regulation"
url = (
    "https://api.gdeltproject.org/api/v2/doc/doc"
    f"?query={query}&mode=ArtList&format=json&maxrecords=50&sort=datedesc"
)

res = requests.get(url, timeout=30)
res.raise_for_status()
payload = res.json()

articles = pd.DataFrame(payload.get("articles", []))
news = articles[["seendate", "sourceCountry", "language", "title", "url"]].copy()
news.head(10)
```

```python
sanity_checks(news, name="news")
```

**Table (required):**

```python
news["language"].value_counts().head(10), news["sourceCountry"].value_counts().head(10)
```

**Optional: save for later NLP**

```python
news.to_csv("gdelt_news.csv", index=False)
print("Saved gdelt_news.csv")
```

---

:::{admonition} Common pitfall
:class: warning
News is not a neutral mirror of reality. It reflects editorial selection, language coverage, and platform bias.
Treat it as a corpus for text analysis, not “ground truth.”
:::

---

## AI check (responsible use)

:::{admonition} AI check
:class: caution
AI can help you:

* find relevant datasets,
* draft code scaffolding,
* suggest plots.

But you must:

1. verify the dataset matches your question (variables + units),
2. run sanity checks (missingness, ranges, time window),
3. document prompts and edits in your workflow log.
   :::

---

# Data Source Note (required)

Fill this in for your chosen track.

* **Dataset name:**
* **Source (organization / provider):**
* **Access method (URL / package / API endpoint):**
* **Date accessed:**
* **Unit of observation:** (e.g., country-year, day-price, article)
* **Variables used:**
* **Filters applied:** (countries, years, ticker, query terms, etc.)
* **Known limitations:** (coverage, missingness, definitions, comparability, API stability)

---

# Prompt & Workflow Log (only if you used AI tools)

If you used any AI assistance (e.g., ChatGPT) for code or writing, paste:

* prompts used,
* what you copied vs changed,
* how you verified correctness (sanity checks, reruns, spot checks).

If you did not use AI tools, write: “No AI assistance used.”

---

## Review questions (quiz / reflection)

1. When is an API better than downloading a CSV?
2. What must be included in a Data Source Note for reproducibility?
3. What is one limitation of cross-country comparisons using public datasets?
4. What is one bias risk when using news data as evidence?

## Mini-lab (Google Colab)

:::{admonition} Colab link
:class: tip
Complete the mini-lab using the class Colab notebook:

- https://colab.research.google.com/drive/1E9mkBPkGVxFb-DCSBosbynA02mZgDeo4?usp=sharing
:::

### In-class checkpoints (complete in the Colab notebook)

Choose **ONE** data source track in the notebook (OWID / WDI / yfinance / News-GDELT), then complete:

1. Load a dataset into a DataFrame.  
2. Apply a reasonable filter (e.g., **3–5 countries + time range**, **ticker + time range**, or **query + number of articles**).  
3. Produce **one plot** and **one summary table**.  
4. Write a **Data Source Note** and **one limitation**.

---

## Reflection prompt (submit via LMS)

After completing the mini-lab in the Colab notebook, submit brief answers in the link below to the following:

1. Which data source track did you choose (**OWID / WDI / yfinance / News-GDELT**) and why?  
2. What exactly did you analyze?  
   - OWID/WDI: dataset/indicator name (and code/slug if applicable), countries, time range  
   - yfinance: ticker(s), time range  
   - News-GDELT: query term(s), number of articles, time sorting/filters  
3. What is the **main pattern** shown in your plot (1–2 sentences)?  
4. What is **one limitation** of the dataset or your comparison (missingness, definitions, coverage, comparability, API bias, etc.)?  
5. Paste your **Data Source Note** (source, access method, date accessed, variables used, filters applied, limitation).

:::{admonition} Reflection prompt
:class: note
In ~150 words: Describe one dataset you pulled today. What question could it answer, and what is one important limitation?

Submit here:

- https://docs.google.com/forms/d/e/1FAIpQLSfvIZwuhIGTuIJmHsj9PpIk27El_51-Zmhq8i4Rk4dWDsuZYg/viewform?usp=publish-editor
:::

