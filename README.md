# Revenue Durability & Segmentation Intelligence Model

**Project Lighthouse: Revenue Durability at lightening.net**

---

## Overview

This project analyzes revenue durability for a SaaS platform (lightening.net) by moving beyond topline MRR and segmenting the drivers of retention, churn, and expansion.

The goal is to determine whether growth is durable (retention-driven) or acquisition-dependent.

This project combines:

* Data modeling (fact + dimension tables)
* Cohort retention analysis
* Segmented Net Revenue Retention (NRR)
* Activation analysis
* Forecast simulation
* Optional churn prediction modeling

---

## Core Business Questions

1. Which user segments drive compounding revenue?
2. Where is revenue leakage occurring?
3. Is growth durable or dependent on acquisition?
4. What metric should leadership monitor weekly?
5. Are recent metric shifts structural or noise?

---

## Data Architecture

### Fact Table

`fact_user_month`

**Grain:** one row per user per month

This table supports:

* MRR / ARR calculations
* Revenue bridge analysis
* Churn and contraction tracking
* Expansion tracking
* Cohort retention modeling

Key fields:

* user_id
* month
* plan_id
* mrr
* expansion_mrr
* contraction_mrr
* churn_mrr
* churned_this_month
* activation_within_7d
* usage_events
* deploys

### Dimension Tables

* `dim_user`
* `dim_plan`
* `dim_month`

The model follows a simple star schema design to prevent metric drift and ensure clean aggregation.

---

## Analysis Sections

### 1. Activation Analysis

* Time to first deploy
* Activation within 7 days
* Activation impact on churn probability

### 2. Cohort Retention

* Monthly cohort retention matrix
* Revenue retention by cohort
* Retention by plan type

### 3. Segmented NRR

* NRR by plan
* NRR by cohort
* NRR by activation status

Formula:
NRR = (Starting Revenue + Expansion − Contraction − Churn) / Starting Revenue

### 4. Forecast Simulation

Scenario A: Status Quo
Scenario B: Improved Activation
Scenario C: Acquisition Slowdown

Outputs:

* Projected MRR by quarter
* Projected ARR after 12 months
* LTV sensitivity to churn

### 5. Predictive Layer (Optional)

Logistic regression predicting churn probability using:

* activation behavior
* usage intensity
* plan type
* maturity bucket

---

## Key Metrics Defined

* MRR: Monthly recurring subscription revenue
* ARR: Annualized recurring revenue
* ARPU: Average revenue per paying user
* LTV: ARPU / churn rate
* NRR: Revenue retained and expanded from existing customers
* Logo churn: % of customers lost
* Revenue churn: % of revenue lost

---

## Strategic Insight Goal

This project aims to identify:

* Whether revenue is compounding
* Whether retention is concentrated in specific segments
* Whether growth is masking structural weaknesses
* What operational levers improve durability

---

## Tools Used

* Python (Pandas)
* SQL (warehouse-style logic)
* Tableau (optional visualization)

---

## Guiding Principle

Totals show direction.
Segmentation reveals truth.
Durable growth is retention-driven.
