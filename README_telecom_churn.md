# Telecom Customer Churn Analysis
> End-to-end exploratory data analysis on 243,553 telecom customer records to identify churn drivers and recommend data-backed retention strategies.

---

## Project Overview

Customer churn is one of the most expensive problems in the telecom industry. This project performs a full-cycle data science analysis — from raw data cleaning through statistical hypothesis testing to executive-level business recommendations — on a large telecom dataset.

The goal: **find exactly when, why, and among whom customers churn**, then propose actionable fixes.

---

## Dataset

| Property | Detail |
|----------|--------|
| Records | 243,553 customer entries |
| Features | Usage metrics (data, SMS, calls), registration date, city, churn label |
| Target | `churn` (binary: 0 = active, 1 = churned) |
| Source | Telecom subscriber dataset (`telecom_churn.csv`) |

---

## Project Structure

```
telecom-churn-analysis/
│
├── Telecom_Churn_Analysis.ipynb   # Main analysis notebook
├── telecom_churn.csv              # Raw dataset (not tracked)
└── README.md
```

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| Python 3 | Core language |
| Pandas | Data manipulation & profiling |
| NumPy | Numerical operations |
| Matplotlib / Seaborn | Visualizations |
| SciPy (stats) | Hypothesis testing |

---

## Analysis Phases

### Phase 1 — Environment Setup
- Consistent plotting style configured (Seaborn whitegrid)
- Dataset loaded with initial shape and type inspection

### Phase 2 — Data Cleaning & Profiling
- Dropped redundant geographic columns (`state`, `zip_code`), retained `city` as primary location anchor
- Parsed `date_of_registration` to datetime format for tenure computation
- Corrected impossible negative values in usage columns (`data_used`, `sms_sent`, `calls_made`) by floor-bounding to 0

### Phase 3 — Feature Engineering
- **Tenure months:** Calculated from registration date to dataset's latest anchor date
- **Tenure cohorts:** Segmented customers into lifecycle stages (New, Early, Mid, Mature) for cohort-level analysis
- **Feature adoption score:** Flagged whether each customer actively used data, SMS, and calls (above-median = active user per service)

### Phase 4 — Exploratory Data Analysis
Three targeted business questions answered:

| # | Business Question | Method |
|---|---|---|
| Q1 | Which lifecycle stage has the highest churn? | Cohort churn rate aggregation |
| Q2 | Is there a usage threshold below which churn spikes? | Median comparison + distribution plots |
| Q3 | Which cities contribute most to churn volume? | City-level aggregation filtered by significance |

### Phase 5 — Statistical Hypothesis Testing

| Test | Question | Outcome |
|------|----------|---------|
| Chi-Square test | Does tenure cohort significantly affect churn? | Statistically significant relationship confirmed |
| Independent T-Test | Is the data usage gap between active/churned users real? | Statistically significant difference (not noise) |

### Phase 6 — Product Engagement Analysis
- Computed feature adoption score (0–3) per customer
- Proved that customers using multiple services churn at a significantly lower rate ("stickier" customers)

---

## Key Findings

- **Early-stage churn spike:** Customers in their first 90 days showed a distinct, elevated churn rate versus mid and mature customers
- **Usage drop-off thresholds:** Churned users showed median data and call usage significantly lower than active users — clear predictive signal
- **Geographic concentration:** A subset of cities contributed disproportionately to total churn volume, enabling targeted regional interventions
- **Feature stickiness:** Customers using all three services (data + SMS + voice) churned at substantially lower rates than single-service users

---

## Business Recommendations

1. **Targeted Onboarding (0–90 days):** Implement structured engagement workflow for new customers during the identified high-risk cohort window
2. **Automated Health Score Alerts:** Build real-time scoring model flagging customers whose usage drops below identified thresholds; trigger proactive outreach
3. **Multi-Feature Adoption Campaigns:** Incentivize single-service users to adopt additional services — data shows multi-feature users are significantly more retained

---

## Future Enhancements

- Train a supervised churn prediction model (Random Forest / XGBoost) for individual risk scoring
- Integrate high-risk customer lists into CRM for automated intervention workflows
- Build a live dashboard tracking cohort health and usage thresholds in real time

---

## ▶How to Run

```bash
# Clone the repository
git clone https://github.com/[your-username]/telecom-churn-analysis.git
cd telecom-churn-analysis

# Install dependencies
pip install pandas numpy matplotlib seaborn scipy

# Open the notebook
jupyter notebook Telecom_Churn_Analysis.ipynb
```

---

## Author

**Kumaran M** — Data Scientist & ML Mentor  
📧 kumaranm.ofcl@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/www.linkedin.com/in/mkumaran13) | [GitHub](https://github.com/kumaranm-official/forestfireproject)