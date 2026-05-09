# Customer-Retention-Churn-Analysis-
# 📉 Customer Retention & Churn Analysis — Telco Dataset

> A full-stack retention analysis on **7,032 telecom customers** using R, cohort modeling, and risk segmentation.  
> Built to answer: *Why are customers leaving — and what can we do about it?*

---

## 📌 Project Overview

This project performs an end-to-end customer churn analysis on the [Telco Customer Churn Dataset (Kaggle)](https://www.kaggle.com/datasets/blastchar/telco-customer-churn), simulating the kind of retention work done by data analysts in product, growth, and SaaS teams.

The goal is to help business stakeholders answer:

- 🔴 Why are customers leaving the platform?
- 📊 Which customer segments are most at risk of churning?
- ⏳ How long do customers typically stay active?
- ✅ What actions can measurably improve customer retention?

---

## 🔍 Key Findings at a Glance

| Metric | Value |
|--------|-------|
| Overall Churn Rate | **26.6%** |
| Churn — First 3 Months | **59.1%** |
| Churn — After 24 Months | **14.3%** |
| Month-to-Month Contract Churn | **42.7%** |
| Two-Year Contract Churn | **2.85%** |
| Senior Citizen Churn Rate | **41.7%** |
| Avg Monthly Charge — Churned | **$74.44** |
| Avg Monthly Charge — Retained | **$61.31** |

> **Bottom Line:** The first 90 days are make-or-break. Customers who survive past month 24 are highly stable. Month-to-month contracts are **15× riskier** than two-year contracts.

---

## 📈 Analysis Sections

### 1. 🧹 Data Cleaning & Exploration
- 7,043 raw records → 7,032 after removing 11 rows with missing `TotalCharges`
- No other missing values; `TotalCharges` coerced from character to numeric on load
- Summary statistics for all numeric variables

### 2. ⏱️ Customer Tenure & Lifetime Analysis
- Tenure distribution segmented by churn status
- Lifetime segments: Very Short (<3 mo), Short (3–12 mo), Medium (12–24 mo), Long (24+ mo)
- Early churn rate (≤6 months): **53.3%** vs. long-term (>24 months): **14.0%**

### 3. 📅 Cohort Analysis & Retention Curves ⭐
- Four signup cohorts tracked from 2020-01 through 2021-06
- Newest cohort (2021-06) shows only **46.7%** retention at 0–6 months
- Oldest cohort (2020-01) achieves **90.5%** retention at 49–72 months
- Cohort degradation trend signals onboarding problems in recent periods

### 4. 🔑 Churn Drivers & Root Cause Analysis
- Correlation analysis: tenure (r = −0.354) is the strongest predictor
- Contract type is the #1 controllable driver — month-to-month vs. two-year
- Monthly charges statistically significantly higher among churned customers (p < 0.0001)
- Senior citizens churn at nearly double the rate of non-seniors

### 5. 🎯 Customer Segmentation & Risk Scoring
- Risk score built from 3 factors: short tenure, high monthly charges, month-to-month contract
- High-Risk segment (score = 3): **74.0% actual churn rate** — 523 customers
- High-value customers (top 20% by charges) churn at **32.8%** vs. 25.0% for standard

---

## 💼 Recommendations

| Priority | Action | Target Segment | Expected Impact | Timeline |
|----------|--------|---------------|-----------------|----------|
| 🔴 HIGH | 30-day structured onboarding programme | All new customers | Reduce early churn 20–30% | 30 days |
| 🔴 HIGH | Incentivise annual contract upgrades (10–15% discount) | Month-to-month users | Lock in retention −25–35% | 60 days |
| 🟠 MEDIUM | Loyalty rewards at 12, 24, 36-month milestones | Long-term customers | Improve retention +10–15% | 90 days |
| 🟠 MEDIUM | Pricing review for high-charge customers | Top 20% by charges | Prevent price-driven churn | 45 days |
| 🟡 LOW | Quarterly success reviews | High-value segment | Strengthen relationships | Ongoing |
| 🟡 LOW | Exit surveys for all churning customers | Churned segment | Understand real reasons | Immediate |

---

## 💰 Financial Impact Projection

| Metric | Value |
|--------|-------|
| Current Annual Churn | ~1,865 customers |
| Target Annual Churn (post-interventions) | ~1,260 customers |
| Customers Saved | ~605 |
| Avg Revenue Per Customer / Month | $65 |
| Annual Revenue Impact | **+$39,325** |
| Estimated Programme Cost | ~$20,000 |
| **Net Benefit — Year 1** | **+$19,325** |
| **Projected ROI — Year 1** | **~97%** |

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| **R 4.5.2** | Core analysis & statistical testing |
| **tidyverse** | Data wrangling (dplyr, tidyr, ggplot2) |
| **ggplot2** | All visualizations |
| **patchwork** | Multi-panel plot composition |
| **corrplot** | Correlation matrix visualization |
| **knitr** | Clean table output |
| **scales** | Axis formatting |
| **R Markdown** | Reproducible report generation |

---

## 📁 Repository Structure

```
churn-analysis-telco/
│
├── data/
│   └── WA_Fn-UseC_-Telco-Customer-Churn.csv   # Original Kaggle dataset
│
├── analysis/
│   └── Customer-Retention-Churn-Analysis.Rmd  # Full R Markdown analysis
│
├── outputs/
│   ├── Customer_Retention_Churn_Report.docx   # Executive report (Word)
│   └── churn_analysis_report.html             # Rendered HTML report
│
└── README.md
```

---

## 🚀 How to Reproduce

1. **Clone the repository**
   ```bash
   git clone https://github.com/YOUR-USERNAME/churn-analysis-telco.git
   cd churn-analysis-telco
   ```

2. **Install required R packages**
   ```r
   install.packages(c("tidyverse", "scales", "knitr", "patchwork",
                      "lubridate", "corrplot"))
   ```

3. **Download the dataset**  
   Get `WA_Fn-UseC_-Telco-Customer-Churn.csv` from [Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn) and place it in `/data`.

4. **Run the analysis**  
   Open `analysis/Customer-Retention-Churn-Analysis.Rmd` in RStudio and click **Knit**.

---

## 📊 Dataset Details

- **Source:** [Telco Customer Churn — Kaggle (IBM Sample Data)](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
- **Records:** 7,043 raw → 7,032 cleaned
- **Variables:** 21 (demographics, services, billing, churn label)
- **Target Variable:** `Churn` (Yes / No)

Key variables include: `tenure`, `Contract`, `MonthlyCharges`, `TotalCharges`, `InternetService`, `PaymentMethod`, `SeniorCitizen`, `Partner`, `Dependents`

---

## 📚 Skills Demonstrated

✅ Exploratory Data Analysis (EDA)  
✅ Data Cleaning & Type Coercion  
✅ Cohort Analysis & Retention Curve Modeling  
✅ Statistical Testing (t-tests, Pearson correlation)  
✅ Customer Risk Segmentation  
✅ Business Insight Generation  
✅ Executive Report Writing  
✅ Reproducible Research with R Markdown  

---

## 👤 Author

**Bidusha Shrestha**  
📅 May 2026 | 📌 Status: Complete

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).  
Dataset is publicly available on Kaggle under its original terms of use.
