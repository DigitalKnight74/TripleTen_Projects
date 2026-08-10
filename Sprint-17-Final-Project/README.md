# Interconnect — Customer Churn Prediction

### Final Sprint | TripleTen Data Science Bootcamp

---

## Project Overview

Interconnect is a telecom operator that wants to identify customers who are likely to churn so its
marketing team can proactively offer promotional codes and special plan options before those customers
leave. This project builds a binary classification model to predict churn using contract, personal,
internet, and phone service data collected across four separate datasets.

**Win Condition:** AUC-ROC ≥ 0.88 on the test set (maximum scoring tier).

---

## Dataset

- **Source:** Four separate CSVs — `contract.csv`, `personal.csv`, `internet.csv`, `phone.csv`
- **Size:** 7,043 customers, merged on `customerID`
- **Target:** `Churned` — binary label derived from `EndDate` (1 = churned, 0 = active)
- **Split:** 60% train / 20% validation / 20% test, stratified on the target
- **Class Balance:** ~73.5% retained / ~26.5% churned — addressed via class weighting in each model,
  no resampling required

---

## Project Structure

```
Final-Sprint-Customer-Churn-Prediction/
│
├── datasets/
│   └── final_provider/
│       ├── contract.csv
│       ├── personal.csv
│       ├── internet.csv
│       └── phone.csv
│
├── Interconnect_Telecom_Client_Churn.ipynb
└── README.md
```

---

## Methodology

### Data Preparation

- Self-detecting path logic for local vs. platform environments
- Merged four datasets on `customerID`; missing internet/phone rows treated as a meaningful "no service"
  category rather than dropped or blindly imputed
- Cleaned `TotalCharges` (stored as an object dtype due to blank strings for new customers with zero
  elapsed billing periods) via numeric conversion and a justified zero-fill
- Derived `tenure` from `BeginDate` and `EndDate` (or the data's snapshot date, February 1, 2020, for
  still-active customers), preserving the original `EndDate` string column untouched for target derivation
- Collapsed six redundant "No Service" categories (internet add-ons) and `MultipleLines` into dedicated
  `HasInternet` / `HasPhone` flags to avoid duplicating the same fact across multiple encoded columns
- Checked for and removed duplicate rows after dropping identifying columns, before splitting into
  features and target
- Encoded categorical features by structure: ordinal encoding for `Type` (genuine order), one-hot/dummy
  encoding for low-cardinality unordered categories, manual binary mapping for two-category features

### EDA Findings

- `Type` (contract length), `InternetService`, `PaymentMethod`, and `SeniorCitizen` showed the strongest
  individual churn signals, with churn rates ranging from 2.83% to 42.71% by contract type alone
- `gender` and `MultipleLines` showed negligible predictive value on their own
- Cross-tabulation revealed meaningful overlap between `Type` and `PaymentMethod` — Month-to-month
  customers disproportionately paid via Electronic check — suggesting these features partially capture
  the same underlying "disengaged customer" pattern rather than acting independently

---

## Models

| Model | Preprocessing | Val AUC-ROC | Val Accuracy | Train Time | Predict Time |
| :---- | :---- | :---- | :---- | :---- | :---- |
| Model 0 | StandardScaler | Logistic Regression (baseline) | 0.8550 | 0.7409 | 0.0388s | 0.0004s |
| Model 1 | None | LightGBM | **0.8879** ✅ | 0.8171 | 0.3063s | 0.0069s |
| Model 2 | None | CatBoost | 0.8913 ✅ | 0.8171 | 1.7662s | 0.0032s |

**Final evaluation on the held-out test set (LightGBM):** AUC-ROC = **0.8903**, Accuracy = **81.99%**

---

## Results & Recommendations

### ✅ Recommended: Model 1 — LightGBM

LightGBM was selected as the final model, balancing quality and computational cost:

- **Quality:** Validation AUC-ROC of 0.8879, comparable to CatBoost's 0.8913 — confirmed on the test set
  at AUC-ROC 0.8903, clearing the project's 0.88 threshold for the maximum score tier
- **Training Speed:** Trained nearly 6x faster than CatBoost (0.31s vs. 1.77s)
- **Prediction Speed:** Fast enough for real-time scoring in a production churn-flagging pipeline

### Key Findings

**Logistic Regression** was the fastest model by a wide margin but produced the weakest class separation
(0.8550 AUC), limited by its inability to capture the feature interactions found during EDA
(e.g., contract type × payment method).

**CatBoost** matched LightGBM's quality almost exactly (0.8913 vs. 0.8879 AUC) but took nearly 6x longer
to train for no meaningful gain in predictive performance — a poor trade given Interconnect's stated
interest in training time as a business cost.

**Feature importance vs. EDA:** `tenure` dominated LightGBM's feature importance ranking, likely absorbing
much of the signal EDA attributed to `Type`, since contract length structurally constrains how early a
customer can churn. `gender` ranked higher in importance than its near-zero EDA churn-rate spread would
suggest — a reminder that tree-based feature importance reflects split usage, not standalone predictive
strength, and EDA-level churn-rate analysis remains the more reliable tool for business conclusions.

### Business Recommendation

The final model's confusion matrix showed 251 missed churners (false negatives) against 324 customers
incorrectly flagged as at-risk (false positives). Since a missed churner represents a fully lost customer
while a false positive only costs a modest promotional incentive, Interconnect's marketing team should
favor a model or decision threshold that prioritizes recall over precision for the churned class — the
cost of a missed at-risk customer outweighs the cost of an unnecessary retention offer.

---

## Technologies Used

- **Python** 3.12 (local) / 3.9 (TripleTen platform)
- **Libraries:** pandas, numpy, scikit-learn, LightGBM, CatBoost, matplotlib, seaborn

---

## Environment Notes

This notebook uses self-detecting path logic to handle the difference between local development and the
TripleTen platform:

```python
tripleten_path = '/datasets/final_provider/'
local_path = 'your/local/path/final_provider'

if os.path.exists(tripleten_path):
    dataset_path = tripleten_path
else:
    dataset_path = local_path
```

---

## Author

**George Knight** | DigitalKnight74
TripleTen Data Science Bootcamp — Final Sprint
[GitHub](https://github.com/DigitalKnight74)
