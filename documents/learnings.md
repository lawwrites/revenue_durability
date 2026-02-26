
Here is your structured plan in clean Markdown, ready to use in your notebook, README, or case study submission.

---

# Revenue Durability Investigation Plan

### Bolt.new Case Study – Built to Thomas Mickley’s Standards

---

## Guiding Principle

We are not “analyzing.”

We are investigating.

Thomas does not respect dashboards.
He respects disciplined curiosity.

The questions driving this work:

* Why is growth slowing?
* Which users are driving this spike?
* Is this structural or noise?

Totals show direction.
Segmentation reveals truth.

---

# Vocabulary

* **Topline Metric**: A high-level number (total MRR, total users).
* **Segmentation**: Breaking a metric into mutually exclusive groups.
* **Mutually Exclusive**: A user belongs to only one segment.
* **Collectively Exhaustive**: Every user belongs to some segment (including “Unknown”).
* **Cohort**: Users grouped by signup month.
* **Revenue Concentration Risk**: When growth depends heavily on one segment.
* **Structural Weakness**: A long-term issue masked by growth.
* **Revenue Bridge**: Decomposition of revenue movement (Expansion − Contraction − Churn).
* **Net Revenue Retention (NRR)**: Revenue retained and expanded from existing customers.

---

# Investigation Framework

## Step 1: Anchor the Narrative

**Question:** Is MRR trending up, flat, or slowing?

### Action

* Calculate total MRR by month.
* Plot the trend.

### Output

* Growth rate by month
* Month-over-month change

### Why This Matters

Topline establishes direction.
But direction without segmentation is incomplete.

We prepare the second layer before Thomas asks, “Why?”

---

## Step 2: Segment by Plan

Segment by:

* Month
* Plan type

### Analyze

* MRR by plan over time
* Churn rate by plan
* NRR by plan
* ARPU by plan

### Questions

* Is Pro growing faster than Free?
* Is Premium shrinking while Free grows?
* Is ARPU compressing?
* Is churn concentrated in one plan?

### Risk Signals

* Growth concentrated in lower-priced plans → Margin compression risk
* High churn in one tier → Pricing/packaging issue

---

## Step 3: Segment by Activation

Segment by:

* activation_within_7d (Yes / No / Unknown)
* Month

### Calculate

* Churn rate by activation status
* NRR by activation status
* Revenue contribution by activation segment

### Interpretation

If:

* Activated users → 120% NRR
* Non-activated users → 70% NRR

Then:

Revenue durability is concentrated in activated users.

That is not a metric.
That is a strategic lever.

---

## Step 4: Segment by Account Age

Create mutually exclusive buckets:

* 0–1 months
* 2–6 months
* 6+ months

### Analyze

* Churn rate by age bucket
* NRR by age bucket
* Revenue contribution by age bucket

### Questions

* Is churn front-loaded?
* Are mature users stable?
* Are recent cohorts retaining worse than older ones?

### Structural vs Noise

* Recent cohort degradation → Structural issue
* One-month anomaly → Likely noise

---

## Step 5: Revenue Bridge Analysis

For each month calculate:

Starting MRR

* Expansion
  − Contraction
  − Churn
  = Ending MRR

### Purpose

Identify the driver of revenue movement:

* Is decline caused by churn?
* Is downgrade behavior increasing?
* Is expansion slowing?

### Output

* Monthly revenue bridge table
* Contribution breakdown (% of total movement)

### Executive Insight Example

If:
Churn + downgrades > expansion

Then:

Revenue durability is weak.

---

## Step 6: Cohort Retention Matrix

Build:

* Logo retention by cohort
* Revenue retention by cohort

### Questions

* Are newer cohorts weaker?
* Are specific signup months underperforming?
* Is retention improving or degrading over time?

This distinguishes structural shifts from volatility.

---

# Quality Standards (Thomas-Level Thinking)

Before presenting results:

* Validate fact table grain (1 row = 1 user-month)
* Ensure segments are mutually exclusive and collectively exhaustive
* Include “Unknown” bucket in all segmentations
* Confirm no row explosion after joins
* Validate revenue reconciliation (bridge matches MRR delta)

---

# Deliverable Structure

## 1. Executive Summary (1 Page)

* Is growth durable?
* Which segment drives compounding revenue?
* Where is leakage concentrated?
* What metric should leadership monitor weekly?

## 2. Supporting Analysis

* Topline MRR trend
* Plan segmentation
* Activation segmentation
* Age segmentation
* Revenue bridge
* Cohort matrix

## 3. Strategic Recommendation

Identify:

* Primary operational lever
* Risk concentration
* Forecast implication if acquisition slows

---

# Expected Outcomes

You should be able to clearly answer:

* Which segment is driving growth?
* Which segment is leaking revenue?
* Is growth durable or acquisition-dependent?
* What is the single highest-leverage operational lever?

Be specific.

No vague answers.

---

# How This Meets Thomas’s Standard

This approach demonstrates:

* Structured investigation
* Segmented reasoning
* Business framing
* Metric integrity
* System-level thinking

Not dashboards.

Not surface metrics.

Durability intelligence.

---

You are not pretending.
You are training at the level of someone who scales revenue intentionally.

“Plans fail for lack of counsel, but with many advisers they succeed.” — Proverbs 20:18

Now visualize it:

Thomas asks, “Why is growth slowing?”
You pause.
You answer with segmented clarity.
You don’t rush.
You think structurally.

That $140K role isn’t aspirational.
It’s alignment.

---

# Vocabulary Words

* **Date Dimension (dim_month)**: A table that enriches raw month values with calendar logic (year, quarter, month index, etc.).
* **Calendar Logic**: Derived time attributes (Q1, fiscal year, month number).
* **Time Intelligence**: The ability to compare periods correctly (MoM, YoY, cohort aging).
* **Surrogate Key**: A stable internal key (like month_id) used instead of raw dates.
* **Metric Drift**: When calculations subtly change depending on query logic.

---

# Real-World Example

Let’s say your `fact_user_month` has a column:

```python
month = "2024-01"
```

You *could* group by that string and calculate MRR.

But what happens when you need:

* Quarter aggregation?
* Fiscal year logic?
* Month ordering?
* Cohort aging (Month 0, Month 1, Month 2 since signup)?
* Continuous month indexing for retention matrices?

If you skip `dim_month`, you’ll start writing messy logic like:

```python
df['year'] = df['month'].str[:4]
df['month_num'] = df['month'].str[5:]
```

That’s brittle.

A proper `dim_month` gives you:

* calendar_year
* calendar_quarter
* month_number
* month_index (critical for retention modeling)
* maybe fiscal flags

That’s not cosmetic.
That’s structural integrity.

---

# So What If You Don’t Join It?

You can absolutely skip it for:

* Simple MRR trend
* Simple churn rate
* One-off grouped analysis

But you lose:

1. Clean cohort aging
2. Accurate quarter rollups
3. Reliable month-over-month comparisons
4. Scalable production logic

And this matters because:

Thomas has run data platforms.
He cares about scalable metric logic.
Not just “it worked in my notebook.”

---

# When You SHOULD Join dim_month

Join it when:

* Building cohort retention matrices
* Calculating MoM or YoY growth
* Doing forecast simulation
* Building executive dashboards
* Creating production-grade metric tables

Do NOT join it just to join it.

Join it when you need time intelligence.

That’s disciplined.

---

# Lorraine’s Interview Answer

If asked:

“Why would you join dim_month?”

* **To standardize time logic and prevent ad hoc date parsing.**
* **To support cohort aging and month indexing cleanly.**
* **To enable consistent quarter and year aggregation.**
* **To avoid metric drift across analyses.**
* **To productionize durable time-based reporting.**

That answer signals platform maturity.

---

# Lorraine (STARR – 30 seconds)

**Situation:** Needed to build retention and revenue trend analysis.
**Task:** Ensure consistent time aggregation and cohort modeling.
**Action:** Joined dim_month to leverage standardized calendar attributes and month indexing.
**Result:** Enabled reliable MoM, YoY, and cohort retention reporting without fragile date parsing logic.

---

# The Real Strategic Question

Ask yourself:

Are you doing exploratory notebook work?

Or are you building something production-ready?

If exploratory → optional.

If production or executive-facing → join it.

That’s the difference between analyst and data platform thinker.

---

# Knowledge Check

1. Why is cohort aging difficult without a month index?
2. What risks occur if different analysts define quarters differently?
3. When would you intentionally NOT join dim_month?

**Python Question:**
How would you create a month_index column without dim_month?

**SQL Question:**
Write SQL to calculate quarterly MRR using dim_month.

---

Now I’ll challenge you:

For the lightening.net case study —
Are you trying to impress with analysis…

Or demonstrate you can think like someone who builds durable systems?

Answer that.

---

“Wisdom is the principal thing; therefore get wisdom.” — Proverbs 4:7

See yourself in that interview.
You explain why dim tables exist.
You’re not coding. You’re thinking structurally.
That’s how you step into that $140K role.


# Vocabulary Words

* Topline Metric: A high-level number (total MRR, total users).
* Segmentation: Breaking a metric into mutually exclusive groups.
* Mutually Exclusive: A user can belong to only one segment.
* Collectively Exhaustive: Every user must belong to some segment (including “unknown”).
* Cohort: Users grouped by signup month.
* Revenue Concentration Risk: When growth depends heavily on one segment.
* Structural Weakness: A long-term issue masked by growth.


Good.

You’re asking the right question.
`.apply()` and `lambda` are simple — but people misuse them constantly.

We’re going to make this clean and clear.

---

# Vocabulary Words

* **Function**: A reusable block of code that performs a task.
* **Lambda Function**: A small, anonymous (unnamed) function written in one line.
* **.apply()**: A Pandas method that applies a function to each column or row.
* **Vectorized Operation**: A faster way to operate on entire columns at once (preferred when possible).
* **Axis**:

  * `axis=0` → apply to each column
  * `axis=1` → apply to each row

---

# Real-World Explanation

Think of `.apply()` like this:

> “Take this function and run it on every column or every row.”

### Example 1 — Column-Wise (Default)

```python
df.apply(pd.to_datetime)
```

This says:

> For each column, run `pd.to_datetime()`.

Each column gets passed into the function.

---

### Example 2 — Row-Wise

```python
df.apply(lambda row: row['mrr'] * 12, axis=1)
```

This says:

> For each row, multiply the mrr value by 12.

Each row becomes a Series.
`row['mrr']` refers to that row’s value.

---

# What is a Lambda Function?

Normal function:

```python
def square(x):
    return x * x
```

Lambda version:

```python
lambda x: x * x
```

It’s just a shortcut.

Structure:

```python
lambda input: expression
```

No `return` keyword.
It automatically returns the expression.

---

# When Should You Use `.apply()`?

Use `.apply()` when:

* You need row-wise logic (combining multiple columns)
* You need custom transformation logic

Do NOT use `.apply()` when:

* You can use vectorized operations
* You’re just doing arithmetic on a single column

Vectorized example (better):

```python
df['annual_mrr'] = df['mrr'] * 12
```

Cleaner. Faster. More “Thomas-level.”

---

# Common Mistake You Made Earlier

You assumed:

```python
df.apply(lambda x: ...)
```

`x` = column name

Wrong.

`x` = entire column (Series).

That’s why your logic broke.

---

# Clear Mental Model

If you do:

```python
df.apply(lambda col: col.mean())
```

Each `col` is a full column Series.

If you do:

```python
df.apply(lambda row: row['mrr'] * 12, axis=1)
```

Each `row` is a row Series.

---

# Senior-Level Insight

Thomas will not care if you know `.apply()`.

He will care that you know:

* When NOT to use it.
* Why vectorized operations are faster.
* That row-wise apply is computationally expensive.

That’s system thinking.

---

# Quick Quiz (Answer Without Looking Back)

### 1.

If you run:

```python
df.apply(lambda x: x.sum())
```

Is `x` a row or a column?

---

### 2.

What does this do?

```python
df.apply(lambda row: row['mrr'] * row['usage_events'], axis=1)
```

---

### 3.

Which is better and why?

### A

```python
df['annual'] = df.apply(lambda row: row['mrr'] * 12, axis=1)
```

### B

```python
df['annual'] = df['mrr'] * 12
```

---

Answer those.

No guessing. Think it through.

---

You are sharpening fundamentals.

“And let us not grow weary of doing good, for in due season we will reap, if we do not give up.” — Galatians 6:9

See it clearly:
You understand the mechanics.
You explain calmly.
You code deliberately.
That $140K role isn’t about brilliance.
It’s about disciplined mastery.


Good. Strong answers.

You’re thinking correctly. Let’s refine one of them slightly and then I’ll explain vectorization clearly.

---

# Quick Feedback on Your Answers

## 1️⃣

> `x` is a column

Correct.
By default (`axis=0`), `.apply()` passes **each column (Series)** into the function.

---

## 2️⃣

You said:

> it multiplies the row data for each column

Small correction:

It multiplies **mrr × usage_events for each row**, because you used `axis=1`.

Each row is passed into the lambda as a Series.

So the more precise answer is:

> It calculates a new value per row by multiplying that row’s `mrr` by its `usage_events`.

Precision matters at senior levels.

---

## 3️⃣

> B, because B is a vectorized operation.

Correct.

Now let’s go deeper.

---

# What Is a Vectorized Operation?

A **vectorized operation** is when you apply a computation to an entire column (or array) at once — without looping through rows manually.

Instead of:

```python
df.apply(lambda row: row['mrr'] * 12, axis=1)
```

You do:

```python
df['annual'] = df['mrr'] * 12
```

### Why Is This Better?

Because Pandas is built on NumPy, which performs operations at the C level (low-level, highly optimized code).

So when you write:

```python
df['mrr'] * 12
```

You are telling the system:

> Multiply the entire column at once using optimized array math.

No Python-level loop.
No row-by-row processing.

It’s faster.
It’s cleaner.
It scales better.

---

# Mental Model

Think of it like this:

### ❌ `.apply()` (row-wise)

“Take each row… one by one… and run this function.”

Slower.
More overhead.
Python loop underneath.

---

### ✅ Vectorized Operation

“Take this entire column and perform math on it simultaneously.”

Faster.
Cleaner.
More production-ready.

---

# When Should You Use Each?

## Use Vectorization When:

* Doing arithmetic on one or more columns
* Comparing values
* Creating boolean masks
* Applying built-in Pandas functions

Example:

```python
df['high_value'] = df['mrr'] > 100
```

---

## Use `.apply()` When:

* Logic requires multiple columns
* You need custom conditional branching
* The logic cannot be expressed with built-in vectorized functions

Example:

```python
df['segment'] = df.apply(
    lambda row: 'High' if row['mrr'] > 100 and row['usage_events'] > 50 else 'Low',
    axis=1
)
```

---

# Why This Matters for Bolt / Thomas

Thomas will respect that you:

* Default to vectorization
* Use `.apply()` intentionally
* Understand computational cost
* Think about scalability

That’s data platform thinking.

---

# Final Clarity Check

Answer this in one sentence:

> Why is a vectorized operation faster than `.apply(axis=1)`?

---

You’re strengthening foundations right now.

“Wisdom is supreme; therefore get wisdom. Though it cost all you have, get understanding.” — Proverbs 4:7

Visualize it:
You’re explaining this calmly.
You’re not guessing.
You understand what’s happening under the hood.
That’s how you prepare for the $140K room — from clarity, not anxiety.
