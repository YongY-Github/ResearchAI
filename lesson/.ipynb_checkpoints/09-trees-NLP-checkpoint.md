# Lesson 9 — Decision Trees + Text-as-Data (NLP) + Ethical Implications
*(model reasoning, evaluation, bias risks, and careful interpretation)*

:::{admonition} Learning goals
:class: tip
By the end of Lesson 9, you should be able to:
1. Explain decision trees in plain language (a sequence of if–then splits that predict an outcome).
2. Fit and evaluate a simple decision tree model in Python (Google Colab).
3. Interpret tree “rules” (decision paths) and connect them to business reasoning.
4. Understand text-as-data basics: clean text, tokenize, compute a simple sentiment score, and interpret results cautiously.
5. Recognize where bias and ethical risks enter both structured-data models (trees) and text workflows (NLP).
6. Communicate results responsibly: performance + limitations + fairness/ethics caveats.
:::

## Why this matters (motivation)

Decision trees and text analytics are both popular in real-world analytics:
- Trees provide “explainable” rules used in credit, marketing, and operations.
- Text analytics summarizes customer feedback, reviews, and news—often the fastest signal available.

But both can go wrong:
- Trees can overfit and encode proxy bias.
- Sentiment tools can misread context, sarcasm, and domain-specific language.

:::{admonition} Reality check
:class: note
Interpretability is not the same as correctness or fairness.
A simple model can still make harmful or misleading recommendations.
:::

---

## Part A — Decision trees (intuition-first)

### What is a decision tree?
A decision tree is a flowchart-like model that repeatedly splits the data into smaller groups to make predictions.

:::{admonition} Key idea
:class: important
A decision tree learns rules like:
- “If usage < 2 hours/week → higher churn risk”
- “If income > threshold and no late payments → approve credit”
Each split tries to separate outcomes to improve prediction.
:::

### Trees are supervised learning
- **Classification tree:** predicts a category (e.g., churn yes/no)
- **Regression tree:** predicts a number (e.g., spending next month)

We focus mainly on classification today, because it fits many business decisions.

---

## How trees choose splits (high-level)

Trees try many candidate split points and choose the one that improves “purity” of outcomes.

- For classification: reduce impurity (e.g., Gini / entropy)
- For regression: reduce within-leaf error (e.g., squared error)

:::{admonition} You do not need the formula
:class: note
You should understand the logic:
splits separate outcomes, deeper trees are more flexible, and flexibility increases overfitting risk.
:::

---

## Overfitting (why trees are fragile)

Trees can keep splitting until they effectively memorize the training data.

Symptoms:
- high training accuracy
- much lower test accuracy
- many small leaves and complex rules

Controls (practical knobs):
- `max_depth`
- `min_samples_leaf`
- `min_samples_split`
- pruning (conceptual)

:::{admonition} Key idea
:class: important
Trees trade off:
- **simplicity** (generalization, interpretability)
vs
- **complexity** (better training fit, higher overfitting risk).
:::

---

## Evaluation: what we emphasize in this course

### Confusion matrix and error costs
For binary classification (e.g., churn yes/no):
- True positive (TP): correctly flagged churners
- False positive (FP): flagged but not a churner
- False negative (FN): missed churner
- True negative (TN): correctly not flagged

In business, FP vs FN have different costs:
- FP → wasted retention offer / unnecessary friction
- FN → lost customer / lost revenue

:::{admonition} Common pitfall
:class: warning
Accuracy can be misleading when classes are imbalanced.
If only 5% churn, predicting “no churn” gives 95% accuracy but is useless.
Always check class balance and consider precision/recall.
:::

### Minimal metric set (recommended)
- Accuracy (as a baseline only)
- Precision and recall (or F1)
- ROC-AUC (optional if you introduce it later)

We will keep this light and interpretable.

---

## Interpretation: reading tree rules as business logic

One advantage of trees is the ability to explain decision paths:
- “If A and B then predicted churn”
- “If C then predicted no churn”

But interpretation must be cautious:
- a rule can reflect confounding, not causality
- a rule can be unstable if it depends on small leaves

:::{admonition} Practical rule
:class: tip
If a rule depends on very few observations (tiny leaf), treat it as unreliable and likely overfitting.
:::

---

## Part B — Text as data (NLP) (practical and cautious)

### Why text matters in business/economics
Text appears everywhere:
- customer reviews and open-ended survey responses
- call-center notes, chat logs
- news articles and corporate reports
- policy documents

Text is rich but messy. We need a simple workflow to extract signals.

:::{admonition} Key idea
:class: important
A basic text workflow:
1. Collect text
2. Clean (normalize)
3. Tokenize
4. Convert to a numeric signal (counts / TF–IDF / sentiment score)
5. Analyze and validate by checking examples
:::

### Today’s focus: sentiment analysis (simple signal, not truth)
Sentiment tools label text as positive/negative/neutral.

Useful for:
- quick monitoring and coarse trends
- comparing product categories (with validation)
- identifying highly negative feedback to review manually

Weak for:
- sarcasm (“great, it broke again”)
- domain-specific language (“volatile” can be neutral in finance)
- mixed sentiment in one text
- multilingual or non-native writing (often common in international business settings)

:::{admonition} Common pitfall
:class: warning
Sentiment models are often trained on general English.
They can systematically mislabel finance/econ language or local expressions.
Always inspect misclassified examples and avoid overclaiming.
:::

---

## Part C — Ethical implications (trees + text)

Ethical risk is not an “extra topic”—it is embedded in the pipeline.

### Where bias enters (structured data)
1. **Target label** (what is “good/bad”?)
2. **Features** (proxy variables for sensitive attributes)
3. **Sampling** (who is represented?)
4. **Measurement** (errors differ across groups)
5. **Objective** (optimize accuracy only → harms minority groups)

Examples:
- credit: zip code can proxy socio-economic status
- hiring: “career gap” can proxy caregiving responsibilities
- customer scoring: region/language can proxy demographics

### Where bias enters (text)
- training data biases (what language/register is “normal”?)
- stereotypes encoded in word usage
- sentiment misreads certain dialects or non-native writing
- moderation/selection bias (who leaves reviews?)

:::{admonition} Key idea
:class: important
Fairness is not only technical.
It is also about:
- what decisions are being made,
- who is affected,
- and what errors are most harmful.
:::

### A simple “responsible presentation” checklist (course version)
When presenting model results, include:
1. What the model is for (decision context)
2. Performance summary (and what errors mean)
3. At least one limitation (data, measurement, generalization)
4. At least one fairness/ethics caveat (proxy risk, group disparity risk, monitoring need)
5. A statement about human oversight (not fully automated decisions in high-stakes contexts)

---

## Mini case 1: churn prediction with a tree (rules + evaluation)
**Question:** “Can we identify at-risk customers using simple, explainable rules?”

Workflow:
1. Choose outcome (churn yes/no)
2. Fit baseline tree
3. Evaluate on test set and interpret errors
4. Extract 2–3 decision rules and assess plausibility
5. Identify proxy risk and propose monitoring

---

## Mini case 2: review sentiment (text signal + error analysis)
**Question:** “What complaints are most negative, and what are we missing?”

Workflow:
1. Compute sentiment scores for reviews
2. Compare distributions by product category
3. Inspect examples:
   - top 5 most negative
   - 5 that look wrongly labeled
4. Write one limitation and propose a validation step

---

## Mini-lab (Google Colab)

:::{admonition} Colab link
:class: tip
Replace this with your real link:

- Week 9 notebook (Trees + Text + Ethics): https://colab.research.google.com/drive/PASTE_NOTEBOOK_ID
:::

### In-class checkpoints (Decision tree)
1. Choose a classification outcome (e.g., churn yes/no) and 5–10 predictors.
2. Split data into train/test (and optionally a validation split).
3. Train a baseline decision tree.
4. Control complexity:
   - try at least two settings (e.g., `max_depth` or `min_samples_leaf`)
   - compare train vs test results
5. Report:
   - confusion matrix
   - precision/recall (or F1)
6. Interpret:
   - extract at least two decision paths or rules
   - explain them in plain language (“If … then …”)
7. Short reflection:
   - what kind of mistake is more costly here (FP or FN)? why?

### In-class checkpoints (Text-as-data / sentiment)
8. Load a small dataset of text reviews (provided).
9. Preprocess text (light):
   - lowercase
   - remove obvious punctuation
10. Compute sentiment:
   - score each text
   - compare average sentiment by product/category
11. Error analysis:
   - inspect at least 5 examples where the sentiment seems wrong
   - write a short explanation (sarcasm? domain terms? mixed sentiment?)
12. Optional extension:
   - create a simple “negative review” flag and count by category/time.

### In-class checkpoints (Ethics)
13. Identify at least one potential proxy feature risk in your tree model.
14. Identify at least one bias risk in your text workflow (language, sampling, domain mismatch).
15. Write a short “responsible use note”:
   - how you would monitor model performance and harms in practice.

**Submission (after class)**
- Colab link (view permission) or PDF export.
- Include:
  - metrics + 2 rules + 1 limitation (tree)
  - 1 visualization + 5 inspected examples + 1 limitation (sentiment)
  - a brief ethics/fairness note
  - prompt/workflow log if AI tools were used

---

## AI check (responsible use)

:::{admonition} AI check
:class: caution
AI can help with code scaffolding and explanation drafts, but you must:
1. Verify model inputs and outputs by running the notebook.
2. Avoid “fairness claims” without evidence; use careful language.
3. Inspect examples for NLP results; do not trust sentiment scores blindly.
4. Record prompts and edits in your prompt/workflow log.
:::

**Good prompt examples**
- “Write sklearn code to train a decision tree with max_depth=3 and print a confusion matrix.”
- “How do I interpret precision and recall in a churn context with costly false negatives?”
- “Suggest a checklist for validating sentiment analysis outputs on product reviews.”
- “List potential proxy variables for sensitive attributes in churn/credit contexts.”

**Bad prompt examples**
- “Prove my model is fair.”
- “Write a persuasive story that the model should be deployed immediately.”
- “Summarize the reviews and tell me what customers ‘really think’ without showing examples.”

---

## Review questions (quiz / reflection)

1. Why do decision trees often overfit, and what are two ways to reduce overfitting?
2. Why can accuracy be misleading in imbalanced classification problems?
3. Give two reasons sentiment analysis might fail on business/econ text.
4. Name one point in the pipeline where bias can enter, and one monitoring step you would propose.

:::{admonition} Reflection prompt
:class: note
In ~200 words: Summarize your results from today:
- one tree rule that surprised you (and whether it seems plausible),
- one common error your tree made (FP or FN) and what it implies,
- one example where sentiment analysis failed and why,
- and one ethical/fairness caveat you would include in a report.
:::