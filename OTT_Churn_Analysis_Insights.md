# 🎬 OTT Platform Customer Churn Analysis — Project Insights

**A SQL + Python driven churn analytics project uncovering why subscribers leave an OTT streaming platform — and where the revenue risk hides.**

---

## 📌 Project Overview

Subscriber retention is the single biggest lever for profitability in the OTT/streaming business — acquiring a new subscriber costs far more than keeping an existing one. This project simulates a real-world OTT backend (customer profiles, subscription/billing records, and support tickets stored in a relational SQLite database) and builds a complete churn analytics pipeline: from raw, messy multi-table data → cleaned & merged master dataset → engineered churn features → exploratory analysis → actionable business insights.

**Goal:** Identify *who* is churning, *why*, and *how much revenue* is at stake — the way a Data/Business Analyst would for a streaming subscription business.

---

## 🗂️ Data Architecture

The raw data lived across **3 relational tables** inside a SQLite database (`customer_churn.db`), mirroring how a real OTT platform's backend is typically structured:

| Table | Contents |
|---|---|
| `db_customer` | Subscriber demographics — name, country, state, gender, DOB, interests |
| `db_subscription` | Plan type, contract type, billing, renewal/cancellation dates, CLTV, churn score |
| `db_support` | Complaint history, escalations, CSAT scores |

These were queried via SQL (`sqlite3` + `pandas.read_sql`), inspected with `PRAGMA table_info`, and merged into a single **852-row, 21-feature master dataset** for analysis.

---

## 🧹 Data Cleaning & Feature Engineering

Real subscriber data is never clean — this project handled the kind of inconsistencies analysts see daily:

- **Standardized categorical noise** — merged inconsistent gender labels (`Men`/`Women` → `Male`/`Female`)
- **Smart missing-value imputation** — filled missing `country` values using a `state → country` mapping instead of dropping rows
- **Date normalization** — converted subscription, renewal, cancellation, DOB, and complaint dates to proper `datetime` types
- **Churn labeling** — engineered a binary `churn_flag` from `cancellation_date` (churned vs. active)
- **Tenure calculation** — computed `tenure_days` for every subscriber (time active, or time-to-cancellation)
- **Risk segmentation** — bucketed subscribers into `low / medium / high` churn risk tiers based on `churn_score`
- **Support signal integration** — aggregated complaint counts and escalation flags per customer and joined them into the master table
- **Categorical encoding** — ordinal-encoded plan tier, contract type, and churn risk for correlation analysis

---

## 📊 Key Business Metrics

| Metric | Value |
|---|---|
| **Overall Churn Rate** | **14.08%** |
| **Retention Rate** | 85.92% |
| **ARPU (Avg. Revenue per User)** | $15.34/month |
| **Average Subscriber Tenure** | ~1,555 days |
| **Revenue at Risk (from churned users)** | $1,873.12K |
| **Support Escalation Rate** | 11.97% |
| **Avg. Complaints per Customer** | 0.81 |

### Churn Rate by Plan Type
| Plan | Churn Rate |
|---|---|
| Premium | 15.65% |
| Standard | 13.65% |
| Basic | 13.33% |

➡️ Counter-intuitively, **Premium subscribers churn the most** — a red flag that high-tier customers aren't seeing enough value for what they pay.

### Churn Rate by Acquisition Channel
| Channel | Churn Rate |
|---|---|
| Referral | 15.35% |
| Paid | 14.97% |
| Organic | 11.85% |

➡️ **Organic sign-ups are the stickiest**, while paid and referral acquisition bring in less loyal subscribers — a key input for marketing spend allocation.

### Churn Rate by Geography
State-level churn ranged from as low as **2.94% (Odisha)** to as high as **27.27% (Meghalaya)** — a nearly **9x variance** — revealing that regional service quality, content localization, or competitor presence likely play a major role in retention.

---

## 📈 Exploratory & Visual Analysis

Using **Matplotlib** and **Seaborn**, the project visualizes churn from multiple angles:

- 📉 **Monthly churn trend line chart** — tracking cancellations over time to spot seasonality/spikes
- 📊 **Churn rate by plan type & by state** — bar charts highlighting the highest-risk segments
- 🔥 **Correlation heatmap** — quantifying relationships between plan type, contract type, churn score, and churn risk
- 🔗 **Pairplot & category-faceted plots** — examining how monthly charges, plan type, and gender interact with churn risk tiers

---

## 💡 Business Recommendations

1. **Investigate the Premium tier experience** — with the highest churn despite the highest price point, this is the biggest revenue leak.
2. **Prioritize retention campaigns in high-churn states** (Meghalaya, Nagaland, Assam) where churn exceeds 20%.
3. **Proactively target "high churn-risk" subscribers** (churn score ≥ 70) with retention offers before they cancel.
4. **Rethink referral/paid acquisition incentives** — organic subscribers show meaningfully better retention.
5. **Tighten the support-to-retention loop** — with ~12% of subscribers escalating issues, faster resolution could directly reduce cancellations.

---

## 🛠️ Tech Stack

`Python` · `Pandas` · `NumPy` · `SQLite3` · `Matplotlib` · `Seaborn` · `SQL`

## 🚀 Skills Demonstrated

SQL data extraction from a multi-table relational database · data cleaning & imputation · feature engineering · churn labeling & risk scoring · cohort/segment analysis · correlation analysis · data visualization · business-focused storytelling

---

*This project reflects the end-to-end workflow of a Data Analyst supporting subscription/retention strategy for a streaming (OTT) business — from raw backend data to decision-ready insights.*
