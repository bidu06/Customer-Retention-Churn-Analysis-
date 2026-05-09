# Customer Retention and Churn Analysis — Telco Dataset

A comprehensive, end-to-end customer churn analysis on 7,032 telecom customers using R, cohort modeling, statistical testing, and risk segmentation. This project replicates the kind of retention analytics work carried out by data analysts embedded in product, growth, and customer success teams at SaaS companies and subscription businesses.

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Business Questions Addressed](#business-questions-addressed)
3. [Dataset](#dataset)
4. [Project Structure](#project-structure)
5. [Methodology](#methodology)
6. [Key Findings](#key-findings)
7. [Cohort Analysis](#cohort-analysis)
8. [Churn Drivers](#churn-drivers)
9. [Customer Risk Segmentation](#customer-risk-segmentation)
10. [Recommendations](#recommendations)
11. [Financial Impact Projection](#financial-impact-projection)
12. [Tools and Technologies](#tools-and-technologies)
13. [How to Reproduce](#how-to-reproduce)
14. [Skills Demonstrated](#skills-demonstrated)
15. [Author](#author)

---

## Project Overview

Customer churn — the rate at which customers stop doing business with a company — is one of the most critical metrics for any subscription or service business. Reducing churn by even a few percentage points can have an outsized impact on revenue, customer lifetime value, and growth efficiency.

This project uses the Telco Customer Churn dataset (sourced from Kaggle / IBM Sample Data) to conduct a structured retention analysis. The dataset contains 7,043 customer records covering demographics, subscribed services, billing details, contract type, and churn status. After cleaning, 7,032 records were used for analysis.

The analysis is structured to mirror real-world work: it moves from raw data cleaning through exploratory analysis, cohort-level retention curves, statistical significance testing, multi-factor risk scoring, and finally business recommendations with projected financial impact. The final deliverable is an executive-grade report suitable for presentation to a product manager, startup founder, or business stakeholder.

---

## Business Questions Addressed

- Why are customers leaving the platform?
- Which customer segments are most likely to churn?
- How long do customers typically stay active before churning?
- Are there statistically significant differences in monthly charges between churned and retained customers?
- Which cohorts show the worst retention, and what does that imply operationally?
- What targeted actions can reduce churn, and what is the projected return on those interventions?

---

## Dataset

| Attribute | Detail |
|-----------|--------|
| Source | [Kaggle — Telco Customer Churn (IBM Sample)](https://www.kaggle.com/datasets/blastchar/telco-customer-churn) |
| Raw Records | 7,043 |
| Cleaned Records | 7,032 (11 removed due to missing TotalCharges) |
| Variables | 21 |
| Target Variable | `Churn` (Yes / No) |
| Key Predictors | `tenure`, `Contract`, `MonthlyCharges`, `TotalCharges`, `InternetService`, `PaymentMethod`, `SeniorCitizen`, `Partner`, `Dependents`, `TechSupport`, `OnlineSecurity` |

The dataset covers a range of customer profiles across different contract lengths (month-to-month, one-year, two-year), internet service types (DSL, Fiber Optic, None), and payment methods. Senior citizen status, partner status, and number of dependents are also included as demographic variables.

---

## Project Structure

```
churn-analysis-telco/
│
├── data/
│   └── WA_Fn-UseC_-Telco-Customer-Churn.csv       # Original Kaggle dataset
│
├── analysis/
│   └── Customer-Retention-Churn-Analysis.Rmd       # Full reproducible R Markdown analysis
│
├── outputs/
│   ├── Customer_Retention_Churn_Report.docx         # Executive report (Word format)
│   └── churn_analysis_report.html                   # Rendered HTML report
│
└── README.md
```

---

## Methodology

The analysis follows a structured five-stage pipeline.

**Stage 1 — Data Cleaning and Preparation**

- Loaded raw CSV and inspected structure, column types, and missing values
- Coerced `TotalCharges` from character to numeric, which introduced NAs for blank string entries
- Removed 11 rows with missing `TotalCharges`; no other variables contained missing values
- Converted `SeniorCitizen` from integer (0/1) to a labelled factor for interpretability
- Final dataset: 7,032 rows, 21 columns

**Stage 2 — Exploratory Data Analysis**

- Computed summary statistics across all numeric variables, segmented by churn status
- Visualised churn distribution, tenure histograms, and monthly charges distributions
- Calculated overall churn rate, mean and median tenure, and average charges for churned vs. retained segments

**Stage 3 — Cohort Analysis**

- Assigned customers to synthetic signup cohorts (2020-01, 2020-06, 2021-01, 2021-06) using tenure as a proxy for signup period
- Constructed cohort-level retention curves binned by tenure intervals (0–6, 7–12, 13–24, 25–36, 37–48, 49–72 months)
- Calculated average retention rate per cohort to identify degradation trends over time

**Stage 4 — Churn Drivers and Statistical Testing**

- Pearson correlation between churn and all numeric predictors
- Independent samples t-test comparing monthly charges of churned vs. retained customers
- Categorical breakdowns of churn rate by contract type, senior citizen status, internet service type, and payment method

**Stage 5 — Risk Segmentation and Recommendations**

- Built a three-factor composite risk score using short tenure, high monthly charges, and month-to-month contract as binary flags
- Segmented customers into four risk tiers: High, Medium, Low-Medium, and Low
- Identified the high-value customer segment (top 20% by monthly charges) and analysed their churn behaviour separately
- Translated all findings into prioritised business recommendations with estimated financial impact

---

## Key Findings

**Overall Churn and Tenure Statistics**

| Metric | Value |
|--------|-------|
| Overall churn rate | 26.6% |
| Total customers analysed | 7,032 |
| Churned customers | 1,869 |
| Retained customers | 5,163 |
| Mean tenure (all customers) | 32.42 months |
| Median tenure | 29 months |
| Minimum tenure | 1 month |
| Maximum tenure | 72 months |

**Churn Rate by Tenure Segment**

| Tenure Segment | Churn Rate |
|----------------|------------|
| Very Short — under 3 months | 59.1% |
| Short — 3 to 12 months | 41.1% |
| Medium — 12 to 24 months | 29.5% |
| Long — 24 months or more | 14.3% |

The steepest decline in churn occurs between the Very Short and Long segments — a 74% relative reduction in churn probability. This confirms that the first 90 days of a customer relationship represent the single highest-leverage window for retention intervention. Once a customer crosses the 24-month threshold, churn stabilises at a level that is manageable for most subscription businesses.

**Monthly Charges Comparison**

| Segment | Average Monthly Charge |
|---------|----------------------|
| Churned customers | $74.44 |
| Retained customers | $61.31 |
| Difference | +$13.13 (21.4% higher for churned) |
| t-test p-value | less than 0.0001 — statistically significant |

Customers who churn are paying meaningfully more per month than those who stay. This points to a price-value gap: customers at higher price points are not perceiving sufficient value in the service to justify continued subscription.

---

## Cohort Analysis

Customers were grouped into four approximate signup cohorts based on their tenure at the time of data collection. This provides a proxy view of how retention has evolved across different customer generations.

**Cohort Churn Summary**

| Cohort | Customers | Churned | Churn Rate |
|--------|-----------|---------|------------|
| 2020-01 (oldest cohort) | 3,001 | 358 | 11.9% |
| 2020-06 | 832 | 180 | 21.6% |
| 2021-01 | 1,024 | 294 | 28.7% |
| 2021-06 (newest cohort) | 2,175 | 1,037 | 47.7% |

**Retention Rate by Cohort and Tenure Bin**

| Cohort | Tenure Bin | Retention Rate |
|--------|------------|---------------|
| 2020-01 | 49–72 months | 90.5% |
| 2020-01 | 37–48 months | 81.0% |
| 2020-06 | 25–36 months | 78.4% |
| 2021-01 | 13–24 months | 71.3% |
| 2021-06 | 7–12 months | 64.1% |
| 2021-06 | 0–6 months | 46.7% |

The 2021-06 cohort is the most urgent concern in the dataset. Less than half of customers from this signup period are being retained in the first six months, compared to the 2020-01 cohort which achieves over 90% retention at tenure periods beyond 49 months. The widening gap between the oldest and newest cohorts suggests either a deterioration in onboarding quality, increased competitive pressure on newer acquisitions, or a shift in the profile of customers being acquired in more recent periods. Any of these scenarios warrants urgent investigation.

---

## Churn Drivers

**Correlation Analysis — Numeric Variables**

| Variable | Correlation with Churn | Interpretation |
|----------|----------------------|----------------|
| Tenure | -0.354 | Longer tenure strongly predicts retention |
| Total Charges | -0.199 | Higher lifetime spend predicts retention |
| Monthly Charges | +0.193 | Higher monthly bill predicts churn |
| Senior Citizen | +0.151 | Senior status modestly predicts churn |

**Churn Rate by Contract Type**

| Contract Type | Churn Rate |
|---------------|------------|
| Month-to-Month | 42.7% |
| One Year | 11.3% |
| Two Year | 2.85% |

Contract type is the single most powerful controllable predictor of churn in this dataset. Month-to-month customers churn at approximately 15 times the rate of two-year contract holders. The absence of switching costs or long-term commitment removes all friction against leaving. Every month-to-month customer who can be converted to an annual or two-year plan represents a dramatic reduction in that individual customer's churn probability.

**Churn Rate by Demographic Group**

| Segment | Churn Rate | Share of Customer Base |
|---------|------------|----------------------|
| Senior Citizen | 41.7% | 16.2% |
| Non-Senior | 23.6% | 83.8% |

Senior citizens churn at nearly double the rate of non-seniors. This likely reflects a combination of price sensitivity, lower feature utilisation, and insufficient dedicated support options for this demographic.

**High-Value vs. Standard Customers**

| Segment | Customers | Churn Rate | Avg Monthly Charge | Avg Tenure |
|---------|-----------|------------|-------------------|------------|
| High-Value (top 20%, above $95.80 per month) | 1,408 | 32.8% | $103.00 | 46.7 months |
| Standard | 5,624 | 25.0% | $55.20 | 28.8 months |

High-value customers pay 87% more per month and have 62% longer average tenure, yet they churn at a higher absolute rate than standard customers. The loss of a single high-value customer carries a disproportionate revenue impact and should be treated as a priority retention case.

---

## Customer Risk Segmentation

A composite risk score was constructed from three binary flags, each contributing one point to the total score.

**Risk Factor Definitions**

| Risk Factor | Criteria | Points |
|-------------|----------|--------|
| Short Tenure | Customer tenure of 6 months or fewer | 1 |
| High Monthly Charges | Monthly charges above the dataset median of $70.35 | 1 |
| Month-to-Month Contract | Customer is on a month-to-month plan | 1 |

**Segmentation Results**

| Risk Level | Risk Score | Customers | Share of Base | Actual Churn Rate |
|------------|------------|-----------|---------------|------------------|
| High Risk | 3 | 523 | 7.4% | 74.0% |
| Medium Risk | 2 | 2,414 | 34.3% | 45.0% |
| Low-Medium Risk | 1 | 2,461 | 35.0% | 13.9% |
| Low Risk | 0 | 1,634 | 23.2% | 3.24% |

The High Risk segment, while representing only 7.4% of the total customer base, churns at 74%. This means three out of every four customers in this group will leave without intervention. Targeting this segment first maximises the retention impact per dollar spent on intervention programmes.

---

## Recommendations

**High Priority — Implement within 60 days**

**Recommendation 1: Redesign the new customer onboarding programme**

Target segment: all new customers

The data shows that 59.1% of customers with under 3 months of tenure churn. This is the most acute problem in the dataset and should be treated as the primary intervention. A structured 30-day onboarding sequence with proactive check-ins at Day 7, Day 14, and Day 30 can meaningfully close this gap. Assign a named customer success contact or automated outreach sequence for all new sign-ups. The goal is to get customers to their first clear value moment as quickly as possible and remove any friction that would cause disengagement before a retention habit forms.

Expected impact: 20–30% reduction in early-stage churn.
Timeline: 30 days to design and deploy.

**Recommendation 2: Launch a contract upgrade incentive campaign**

Target segment: all month-to-month customers

Month-to-month customers churn at 42.7% versus 2.85% for two-year customers. Offering a 10–15% discount on the first annual billing cycle — targeted at customers in months 2 through 4 — converts them from the highest-risk contract tier to the lowest overnight. This can be delivered via in-app prompt, email campaign, or direct customer success outreach. The long-term revenue gain from reduced churn more than offsets the short-term discount cost.

Expected impact: 25–35% reduction in churn for successfully converted customers.
Timeline: 60 days to build and launch campaign.

**Medium Priority — Implement within 90 days**

**Recommendation 3: Introduce a loyalty rewards programme for long-term customers**

Target segment: customers with 12 or more months of tenure

Customers who reach the 12-month mark are on the path to long-term retention, but the data shows meaningful churn still occurs between months 12 and 24 (29.5% rate). Milestone rewards at 12, 24, and 36 months — in the form of billing credits, free service upgrades, or access to exclusive features — give customers a concrete reason to stay and a perceived cost to leaving. This also reinforces the sense of relationship with the product.

Expected impact: 10–15% improvement in retention among 12+ month customers.
Timeline: 90 days to design reward structure and automate delivery.

**Recommendation 4: Conduct a pricing review for high-charge customers**

Target segment: top 20% of customers by monthly charges (above $95.80 per month)

Churned customers pay $13.13 more per month on average than retained customers, and this gap is even wider in the high-value segment. A pricing audit of top-tier service bundles — combined with proactive outreach to communicate the specific value delivered at those price points — can address the price-value perception gap before it becomes a cancellation decision. Consider introducing a transparent value summary in monthly billing communications for high-charge customers.

Expected impact: reduce price-driven churn in the top 20% segment.
Timeline: 45 days for audit; 90 days for full implementation.

**Ongoing Initiatives**

**Recommendation 5: Monthly cohort retention tracking**

The degradation of the 2021-06 cohort was only visible through structured retrospective cohort analysis. Without ongoing monthly tracking, similar declines can go undetected for multiple quarters. A recurring cohort dashboard — reviewed monthly by the analytics and product teams — provides an early warning system for any future retention degradation before it compounds into a larger problem.

**Recommendation 6: Mandatory exit surveys for all churning customers**

The quantitative analysis identifies statistical patterns but cannot capture the qualitative reasons customers choose to leave. A brief exit survey of 3 to 5 questions, delivered at the point of cancellation, reveals service failures, competitor influences, pricing objections, and unmet feature expectations that do not appear in structured data. This feeds directly into product roadmap prioritisation and pricing decisions.

**Recommendation 7: Dedicated support track for senior citizens**

Senior citizens churn at 41.7% — nearly double the overall rate — despite representing only 16.2% of the customer base. A dedicated support tier with simplified interface guides, priority phone support, and lower-friction billing options addresses the most likely root causes of their elevated exit rate. This segment responds poorly to purely digital self-service experiences.

---

## Financial Impact Projection

The following projections assume successful implementation of the high- and medium-priority recommendations, using conservative estimates of impact across the targeted segments.

| Metric | Value |
|--------|-------|
| Current annual churn (estimated customers) | approximately 1,865 |
| Target annual churn after interventions | approximately 1,260 |
| Customers retained per year | approximately 605 |
| Average monthly revenue per customer | $65.00 |
| Annual revenue recovered | +$39,325 |
| Estimated programme cost (onboarding redesign, campaign spend, tooling) | approximately $20,000 |
| Net benefit — Year 1 | +$19,325 |
| Projected ROI — Year 1 | approximately 97% |

These figures are conservative. They do not account for the compounding effect of retained customers increasing their tenure and total lifetime value over subsequent years. They also do not include the secondary benefit of reduced customer acquisition cost spend required to replace churned customers.

---

## Tools and Technologies

| Tool | Purpose |
|------|---------|
| R 4.5.2 | Core analysis environment |
| tidyverse 2.0.0 | Data wrangling and transformation (dplyr, tidyr, readr) |
| ggplot2 3.5.1 | All data visualisations |
| patchwork 1.3.0 | Multi-panel plot composition |
| scales 1.3.0 | Axis and label formatting |
| corrplot 0.94 | Correlation matrix visualisation |
| knitr 1.49 | Clean table rendering in R Markdown |
| R Markdown 2.29 | Reproducible report generation |

---

## How to Reproduce

**Step 1 — Clone the repository**

```bash
git clone https://github.com/YOUR-USERNAME/churn-analysis-telco.git
cd churn-analysis-telco
```

**Step 2 — Install required R packages**

Open R or RStudio and run the following:

```r
install.packages(c(
  "tidyverse",
  "scales",
  "knitr",
  "patchwork",
  "lubridate",
  "corrplot"
))
```

**Step 3 — Download the dataset**

Download `WA_Fn-UseC_-Telco-Customer-Churn.csv` from the [Kaggle dataset page](https://www.kaggle.com/datasets/blastchar/telco-customer-churn) and place it in the `/data` directory of the cloned repository.

**Step 4 — Run the analysis**

Open `analysis/Customer-Retention-Churn-Analysis.Rmd` in RStudio. Set the working directory to the project root, then click Knit to generate the full HTML report. To render the Word document version, change the output format in the YAML header to `word_document` before knitting.

**Step 5 — View outputs**

- HTML report: `outputs/churn_analysis_report.html`
- Word report: `outputs/Customer_Retention_Churn_Report.docx`

---

## Skills Demonstrated

- Exploratory data analysis and data cleaning in R
- Cohort analysis and retention curve modelling
- Statistical hypothesis testing (independent samples t-test, Pearson correlation)
- Customer risk scoring and multi-factor segmentation
- Business insight generation from structured data
- Executive report writing for non-technical stakeholders
- Reproducible research with R Markdown
- Data visualisation with ggplot2

---

## Author

**Bidusha Shrestha**

Completed: May 2026
Status: Complete
Dataset: Telco Customer Churn — Kaggle (IBM Sample Data)

---

## License

This project is open-source and available under the [MIT License](LICENSE).
The dataset is publicly available on Kaggle under its original terms of use.
