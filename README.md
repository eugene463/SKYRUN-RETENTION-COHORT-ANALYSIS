# SkyRun Inc. - Customer Retention Analysis

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-orange)
![Status](https://img.shields.io/badge/Status-Draft%20for%20feedback-yellow)

Cohort-based analysis of customer retention for SkyRun Inc., an e-commerce company. The project measures repeat purchasing, finds where customers drop off, segments customers by behaviour, and turns the findings into recommendations with measurable KPIs.

> **Stakeholders:** start with the [report](report/SkyRun_Retention_Report.md), then tell us what we got wrong or missed (see [Feedback](#feedback)).

---

## Contents
- [Business problem](#business-problem)
- [Key results](#key-results)
- [What is in this repository](#what-is-in-this-repository)
- [Approach](#approach)
- [Tools and skills](#tools-and-skills)
- [How to run it](#how-to-run-it)
- [Data](#data)
- [Limitations](#limitations)
- [Feedback](#feedback)
- [Status and next steps](#status-and-next-steps)
- [Author](#author)

---

## Business problem
SkyRun wins many new customers, but too few come back. Retention has been declining, and customers who buy once and disappear rarely repay what it cost to acquire them.

This project answers five questions:
1. How well does SkyRun retain customers from each acquisition month?
2. Which customer groups behave differently?
3. When do customers drop off?
4. What is a customer worth over time?
5. What should SkyRun do about it, and how will it know it worked?

## Key results
Based on 4,339 identified customers and 18,536 orders (December 2024 - November 2025).

| Measure | Result |
|---|---|
| New customers who buy again in the following month | **20%** |
| Customers who eventually place a second order | **66%** |
| Customers currently churned (silent over 102 days) | **31%** |
| Revenue from the top 20% of customers | **66%** |
| Revenue from the "Champions" segment (18% of customers) | **58%** |

**Main findings**
- The biggest loss is between the **first and second order**; only 18% of new customers reorder within 30 days.
- Customers become stickier the more they buy (66% continue after order 1, 75% after order 3).
- **Cooling Regulars** (28% of customers, 28% of revenue) are the most valuable group to rescue.
- Retention dipped mid-2025 and recovered in autumn; it was not in steady decline.
- The first category a customer buys does not reliably change whether they return.

**Recommendations (summary):** nudge new customers between day 14 and day 45, win back regulars at about 75-100 days of silence, protect the Champions, spend little on one-time buyers, fix data gaps, and test every initiative against a control group. Details, KPIs and a 30/60/90-day plan are in the [report](report/SkyRun_Retention_Report.md#5-recommendations).

## What is in this repository
```
.
├── README.md
├── requirements.txt
├── SkyRun_Retention_Analysis.ipynb     # annotated, step-by-step analysis
└── report/
    ├── SkyRun_Retention_Report.md      # stakeholder report
    └── images/                         # charts used in the report
```

| File | Purpose |
|---|---|
| [`report/SkyRun_Retention_Report.md`](report/SkyRun_Retention_Report.md) | Findings, recommendations, limitations and feedback questions, written for non-technical readers |
| [`SkyRun_Retention_Analysis.ipynb`](SkyRun_Retention_Analysis.ipynb) | The full analysis, with explanations of each step and decision. Every number in the report traces back to it |

## Approach
The work follows CRISP-DM:

1. **Business understanding:** define KPIs (retention, repeat rate, churn, AOV, CLV, CAC).
2. **Data understanding:** inspect structure, dates, missing values and data quality.
3. **Data preparation:** remove cancellations and rows with no customer ID, create revenue, build order-level and customer-level tables.
4. **Cohort analysis:** assign customers to first-purchase month cohorts and calculate monthly retention.
5. **Exploration and visualisation:** retention heatmaps, retention curves, order "ladder", second-order timing, revenue concentration.
6. **Segmentation:** RFM (Recency, Frequency, Monetary) with K-Means clustering (k = 4).
7. **Customer value:** cumulative revenue per customer by cohort as inputs for CLV.
8. **Recommendations:** actions with KPIs, baselines and targets.

Key judgement calls (analysis window, churn definition, choice of k, and others) are recorded in the notebook's decision log and in the report's appendix.

## Tools and skills
- **Python:** pandas, NumPy
- **Visualisation:** matplotlib, seaborn
- **Machine learning (unsupervised):** scikit-learn (K-Means, StandardScaler, PCA, silhouette score)
- **Analysis methods:** cohort analysis, retention curves, RFM segmentation, churn definition, CLV inputs
- **Tooling:** Jupyter Notebook, Git and GitHub

## How to run it
1. Clone the repository and install the requirements:
   ```bash
   pip install -r requirements.txt
   ```
2. Place `Skyrun_dataset.csv` in the same folder as the notebook.
3. Open `SkyRun_Retention_Analysis.ipynb` and run all cells from top to bottom.

Results may differ very slightly on other machines because of library versions.

## Data
The transaction file contains 541,909 order lines (1 December 2024 - 9 December 2025) with order number, date, customer ID, product category, quantity, unit price and country.

**The dataset is not included in this repository.** Please obtain it from the project owner.

## Limitations
- About **12 months** of data, so the 18-month retention decline in the brief could not be confirmed.
- About **a quarter of order lines had no customer ID** and were excluded from retention analysis.
- The **country field is inconsistent** within orders, so no geographic analysis was done.
- The dataset appears **synthetic**, so patterns are smoother than real-world data.
- **No cost or margin data**, so CAC and profit-based CLV could not be calculated.
- Findings show **associations, not proof of cause**; changes should be tested.

Full details are in [Section 6 of the report](report/SkyRun_Retention_Report.md#6-limitations-and-risks).

## Feedback
We want your input, especially corrections to our assumptions.

1. Read the [report](report/SkyRun_Retention_Report.md), then go to [Section 7: Feedback requested](report/SkyRun_Retention_Report.md#7-feedback-requested).
2. Open a GitHub **Issue** (one topic per issue) and quote the question number.
3. You can also comment directly on the report file.

## Status and next steps
**Version 1.0 - draft for stakeholder feedback.**

- [x] Cohort retention analysis
- [x] Drop-off and churn analysis
- [x] RFM segmentation with K-Means
- [x] CLV inputs
- [x] Stakeholder report and recommendations
- [ ] Incorporate stakeholder feedback (v1.1)
- [ ] Re-run on production data once data gaps are fixed
- [ ] Design and run A/B tests for the first recommendations
- [ ] Add CAC and profit-based CLV when cost data is available
- [ ] Optional: supervised churn-prediction model built from first-order information only

## Author
**[Eugene]** - [https://www.linkedin.com/in/eugene-opoku-akosah-331307390]
