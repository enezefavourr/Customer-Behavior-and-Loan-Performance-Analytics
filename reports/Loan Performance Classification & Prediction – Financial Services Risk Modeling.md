# Loan Performance Classification & Prediction – Fintech Risk Modeling

## Project Phase: 1 of 3  
**Objective:** Predict customer loan performance  
(Next phases: customer retention & transaction trends)

---

## Overview

This project simulates a real-world fintech problem — predicting whether customers will:
- **Repay loans on time** (Performing)
- **Struggle with payments** (Non-performing)
- **Fully default** (Defaulted)

This is **Phase 1** of a larger customer behavior analytics project for a fintech startup.

---

## Data Summary

- **Source:** [Lending Club (2007–2018)](https://www.kaggle.com/datasets/wordsforthewise/lending-club)
- 2.4M+ approved loans
- 150+ borrower, credit, and loan features
- Extremely imbalanced target variable

---

## Data Cleaning & Preprocessing

The original dataset contained over 150 columns and a raw `loan_status` field with values like:

* `Fully Paid`
* `Current`
* `Charged Off`
* `Late (31-120 days)`
* `In Grace Period`
* `Default`
* and others like `Does not meet the credit policy`

### Step 1: Loan Performance Classification

To simplify this for analysis and machine learning, I created a new column: `loan_performance`, which groups raw statuses into 3 clear categories:

| Raw Statuses                                                 | Classified As      |
| ------------------------------------------------------------ | ------------------ |
| `Fully Paid`, `Current`                                      | **Performing**     |
| `Late (16-30 days)`, `In Grace Period`, `Late (31-120 days)` | **Non-performing** |
| `Charged Off`, `Default`                                     | **Defaulted**      |

Statuses like `Does not meet the credit policy` were excluded from analysis.

This classification allowed us to:

* Run clean EDA and trend analysis
* Train a supervised model with a well-defined target variable
* Treat **loan performance as a 3-class prediction problem**

---

## Modeling Journey

### Initial Attempts – Random Forest

Started with **Random Forest Classifier**, but:
- Model predicted only the majority class (**Performing**)
- **Minority classes (Defaulted & Non-performing)** were ignored completely
- Accuracy was high, but **macro F1 score was very low (~0.33)** — poor for real-world use

### Tried Resampling (Downsampling Majority)

I attempted to fix the class imbalance using:
- **Downsampling** the majority class (Performing loans)
- This improved recall slightly, but:
  - The model began over-predicting Non-performing
  - Overall F1 performance was unstable
  - Precision dropped heavily
- **Macro F1 score remained under ~0.40**

### Switched to XGBoost

Tried **XGBoost** next (industry standard in credit risk modeling):
- Handled imbalance better than Random Forest
- Still underperformed at first:
  - Predicted almost all samples as **Performing**
  - Macro F1 score improved slightly (~0.45), but not usable

### Introduced Stratified Sampling

Updated the train/test split to use **stratification**, which:
- Ensured minority classes were present in both sets
- Helped the model learn better, **especially Non-performing**
- Macro F1 improved to ~0.50+

### Final Breakthrough – Feature Enrichment + Class Weights

Finally, I:
- **Selected better features** based on financial signal quality
- Introduced **payment-related features** like:
  - `total_rec_prncp`, `recoveries`, `out_prncp`, `fico_range_low`, etc.
- Computed **class weights dynamically** using `compute_class_weight` from `sklearn`
- Passed those weights as `sample_weight` to XGBoost

**Result**:
- **Macro F1 score jumped to `0.63+`**
- Model could now **correctly classify Non-performing loans**
- Defaulted class still underrepresented, but partially detectable

---

## Final Features Used

- **Credit scores:** `fico_range_low`, `fico_range_high`, `int_rate`
- **Borrower info:** `annual_inc`, `emp_length`, `dti`, `home_ownership`
- **Loan terms:** `loan_amnt`, `term`, `installment`, `purpose`, `grade`
- **Payment behavior:** `total_rec_prncp`, `recoveries`, `last_pymnt_amnt`, `out_prncp`

---

## 📈 Final Results

| Metric      | Value     |
|-------------|-----------|
| **Macro F1**| `0.63`     |
| Accuracy    | ~95%      |
| Model       | XGBoost + class weights |

### 🔍 Feature Importance (Top 5)
1. `int_rate`
2. `fico_range_low`
3. `total_rec_prncp`
4. `recoveries`
5. `dti`

---

## Business Value

- Helps detect **risk early** in the lending pipeline
- Prevents losses by flagging **customers likely to default or delay**
- No artificial data duplication — makes the model **trustworthy**
- Built with **production-ready tools**: Python, Scikit-learn, XGBoost

---

## Next Steps (Phase 2 & 3)

- **Customer Acquisition & Retention Analysis**
  - Who’s coming in, who’s dropping off, and why
- **Transaction Activity Trends**
  - Detect activity drop-offs or risk signals in user behavior

---

## Tools Used

- Python (Pandas, NumPy)
- Scikit-learn
- XGBoost
- Matplotlib

---

## Key Takeaway

This project reflects real data science work:
- Things didn't work at first
- I tried multiple strategies
- Solved it by combining:
  - **Feature engineering**
  - **Stratification**
  - **Smart class weighting**

💬 *This is the kind of modeling process you face in the real world.*

