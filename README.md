# 🔴 Telecom Customer Churn Prediction
### *Turning churn signals into retention strategies — at scale.*

> **243,553 customers analysed. 79,957 at-risk identified. One model to act on all of it.**

---

## The Problem

Telecom companies lose billions every year to silent churn — customers who leave without warning. By the time the data shows it, it's too late. This project flips that equation: **predict who's leaving before they do**, and give the business a ranked, actionable list to fight back.

---

## What This Project Delivers

| | Deliverable | Impact |
|---|---|---|
| 🔍 | **Churn Drivers** | Know *why* customers leave, not just *that* they do |
| 📊 | **Risk Score (0–100)** | Every customer ranked by likelihood to churn |
| 🚨 | **CHURN_FLAG** | Plug-and-play targeting list for email campaigns |

---

## Results at a Glance

```
Total Customers Scored     →   243,553
──────────────────────────────────────
🟢  Low Risk    (<40)      →   119,196   (49.0%)
🟡  Medium Risk (40–69)    →   103,274   (42.4%)
🔴  High Risk   (≥70)      →    21,083    (8.7%)
──────────────────────────────────────
📧  Email Campaign Targets →    79,957   (32.8%)
```

---

## Pipeline Overview

```
MySQL Database
     │
     ▼
Data Ingestion & Cleaning
     │
     ▼
Exploratory Data Analysis ──► Churn distribution, feature correlations,
     │                         categorical breakdowns, boxplots
     ▼
Preprocessing
     │  ├── Label Encoding
     │  ├── SMOTE (class imbalance correction)
     │  └── StandardScaler
     ▼
Model Training & Evaluation
     │  ├── Logistic Regression
     │  ├── Decision Tree
     │  ├── Random Forest   ◄── Best Model
     │  ├── Gradient Boosting
     │  └── XGBoost
     ▼
5-Fold Cross-Validation (Robustness Check)
     │
     ▼
Output: Churn_Risk_Score · Risk_Tier · CHURN_FLAG
```

---

## Dataset

| Field | Detail |
|---|---|
| **Source** | MySQL — `project_telecom.telecom_churn_data` |
| **Records** | 243,553 customers |
| **Features** | Age, gender, state, telecom partner, salary, calls made, SMS sent, data used, dependents, registration date |
| **Target** | `churn` (0 = stayed, 1 = churned) |

---

## Models Benchmarked

All five models evaluated on **Accuracy · Precision · Recall · F1 Score · ROC-AUC**:

| Model | Notes |
|---|---|
| Logistic Regression | Baseline; scaled features |
| Decision Tree | Interpretable; depth-limited |
| **Random Forest** ✅ | **Selected — best overall ROC-AUC** |
| Gradient Boosting | Strong recall performance |
| XGBoost | Competitive; used for feature importance validation |

*5-Fold Stratified Cross-Validation confirmed stability across all three top models.*

---

## Output Columns (Predictions File)

| Column | Type | Description |
|---|---|---|
| `Churn_Risk_Score` | Float (0–100) | Model probability scaled to a readable score |
| `Risk_Tier` | String | `Low Risk` · `Medium Risk` · `High Risk` |
| `CHURN_FLAG` | Int (0/1) | 1 = predicted to churn |
| `CHURN_FLAG_LABEL` | String | `YES` / `NO` — ready for campaign tools |

---

## Tech Stack

```python
# Core
pandas · numpy · sqlalchemy · pymysql

# Visualisation
matplotlib · seaborn

# Machine Learning
scikit-learn · xgboost · imbalanced-learn (SMOTE)
```

---

## Business Recommendations

1. **High Risk customers (21K) need human outreach** — automated emails alone won't retain them.
2. **Automate email campaigns** for all 79,957 `CHURN_FLAG = YES` customers immediately.
3. **Re-run monthly** — customer behaviour shifts; static models decay fast.
4. **Dig into customer service data** — interaction patterns are likely early churn signals not yet in the model.
5. **Double down on top churn drivers** — the feature importance charts show exactly where to focus product and ops effort.

---

## How to Run

```bash
# 1. Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn xgboost imbalanced-learn sqlalchemy pymysql

# 2. Open the notebook
jupyter notebook Customer_Churn_Analysis.ipynb

# 3. Update DB credentials in Section 2 if needed, then run all cells
# Output → telecom_churn_predictions.csv (auto-saved)
```

---

## Repository Structure

```
📦 telecom-churn-prediction
 ┣ 📓 Customer_Churn_Analysis.ipynb   ← Full pipeline: EDA → Model → Output
 ┣ 📊 telecom_churn_predictions.xls   ← Scored predictions for all 243,553 customers
 ┗ 📄 README.md
```

---

*Built for No-Churn Telecom · Machine Learning · Churn Reduction*
