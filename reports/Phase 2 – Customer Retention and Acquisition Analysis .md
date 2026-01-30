# Customer Retention and Acquisition Analysis 

This phase focused on understanding **customer growth, retention, and churn behavior** using Lending Club loan data. The goal was to extract actionable insights about how customers join, stay, or leave over time — and communicate those insights through an interactive Power BI dashboard.

---

## 🎯 Objectives

- Analyze **customer acquisition trends** over time  
- Measure **customer retention** using active months  
- Identify **churned customers** and calculate churn rate  
- Visualize loan behavior by performance and term  
- Create a dashboard for **stakeholder-friendly reporting**

---

## 🧹 Data Preparation

- Filtered data from Lending Club's accepted loans dataset (2007–2018)
- Created a `loan_performance` label:
  - **Performing**: Current, Fully Paid
  - **Non-performing**: Late, In Grace Period
  - **Defaulted**: Charged Off, Default
- Calculated `active_months` as the number of months between loan issue date and last payment date
- Added a `churned` column:
  - `TRUE` for Defaulted or Non-performing loans
  - `FALSE` for Performing loans

---

## 📊 Dashboard Overview (Power BI)

![Customer Retention Dashboard](images/dashboard-phase2.png)

### 🔢 KPI Cards

| Metric                 | Value      |
|------------------------|------------|
| **Total Customers**    | 2M+        |
| **Churn Rate**         | 13.4%      |
| **Avg. Active Months** | 20 months  |
| **Monthly Growth Rate**| 1.8%       |

---

### 📈 Visual Insights

- **Customer Acquisition by Month**: Shows seasonal trends and growth rates over time.
- **Churn Over Time**: Line chart comparing retained vs churned customers monthly.
- **Loan Performance Distribution**: Donut chart showing the split between performing, non-performing, and defaulted loans.
- **Term Breakdown**: Distribution of loans by 36-month and 60-month terms.
- **Retention Curve**: Histogram of active customer duration in months.

---

## 🔎 Key Insights

- Most customers are retained for **20 months on average**, but a significant number churn before 12 months.
- **13.4% of customers** were classified as churned (defaulted or at risk).
- Majority of loans (~80%) were **Performing**, while ~13% were **Defaulted**, and ~7% were **Non-performing**.
- Acquisition rates grew steadily month-over-month, peaking in later quarters.
- 36-month loans make up the majority of the portfolio, but 60-month loans are more prone to late/default behavior.

---

## 🛠️ Tools Used

- **Power BI** for interactive visual analytics
- **DAX** for dynamic KPIs (churn rate, growth rate, averages)
- **Power Query** for data cleaning and feature creation
- **Python (Colab)** for initial preprocessing

---

## 📦 Outcome

This dashboard provides a **stakeholder-ready view** of customer health, lifecycle, and risk — enabling any fintech product or risk team to:
- Monitor growth and engagement
- Identify churn patterns
- Optimize product decisions by term and loan performance

> ✅ **Phase 2 is complete and connects seamlessly with Phase 1 (Loan Performance Prediction).**

---

## 📁 Next Phase

> Move into **Phase 3: Transaction Activity Analysis**, which will explore spending behaviors, transaction frequency, and patterns across customer segments.

