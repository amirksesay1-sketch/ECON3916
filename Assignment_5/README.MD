# Sovereign Risk Engine
### IMF Early Warning System — World Bank WDI Analysis

A machine learning pipeline that diagnoses OLS overfitting, applies Ridge and Lasso regularization for GDP growth forecasting, and builds a binary crisis classifier with full operational threshold analysis. Data is downloaded live from the World Bank API — no CSV files required.

---

## Setup

**1. Open Google Colab and run the install cell:**
```python
!pip install wbgapi scikit-learn statsmodels matplotlib seaborn numpy pandas
```

**2. Run the imports cell** (Cell 1 — all required libraries).

**3. Run the data pipeline cell** (Cell 2) before any other cell. It downloads live data and defines all shared variables used downstream.

---

## File Reference

| File | Contents |
|---|---|
| `cell1_setup.py` | Install + all imports |
| `pipeline_and_step1_1.py` | Data pipeline + OLS overfitting diagnostic |
| `step1_2_ridge_lasso.py` | RidgeCV, LassoCV, model comparison table |
| `step1_3_lasso_path.py` | Lasso coefficient path plot + stability analysis |
| `step2_1_lpm.py` | Linear Probability Model — out-of-range predictions |
| `step2_2_logistic.py` | Logistic regression, odds ratios, probability bounds |
| `step2_3_lpm_vs_logistic.py` | Side-by-side LPM vs. sigmoid visualization |
| `step3_1_accuracy_paradox.py` | Naïve baseline vs. logistic accuracy comparison |
| `step3_2_confusion_matrix.py` | Confusion matrix, classification report, cell breakdown |
| `step3_3_roc_pr.py` | ROC curve, Precision-Recall curve, AUC scores |
| `step3_4_threshold_analysis.py` | 5-mission capacity constraint + F1-optimal threshold |
| `step4_1_bootstrap_lasso.py` | Bootstrap Lasso stability (200 resamples) |
| `step4_2_cost_sensitive.py` | Cost-minimizing threshold ($50B FN vs. $2M FP) |

---

## Execution Order

Cells must be run **top to bottom**. Each cell depends on variables defined by the ones before it.

```
Cell 1  →  Cell 2 (pipeline)  →  Steps 1.1 → 1.2 → 1.3  →  Steps 2.1 → 2.2 → 2.3  →  Steps 3.1 → 3.2 → 3.3 → 3.4  →  Steps 4.1 → 4.2
```

---

## Shared Variables

The pipeline cell (Cell 2) defines these variables used by all downstream cells:

| Variable | Description |
|---|---|
| `X_train_s`, `X_test_s` | Standardized feature matrices (70/30 split) |
| `y_train`, `y_test` | Continuous GDP per capita growth (regression target) |
| `yc_train`, `yc_test` | Binary crisis labels (classification target) |
| `feature_cols` | List of predictor names |
| `scaler` | Fitted `StandardScaler` (training data only) |
| `base_rate` | Crisis prevalence in test set |

---

## Assignment Phases

### Phase 1 — Regularization
Diagnoses OLS overfitting via bias-variance analysis (learning curves, p/n ratio), then rebuilds the forecasting engine with Ridge and Lasso. The Lasso path identifies which WDI indicators are most robust predictors of cross-country growth.

### Phase 2 — Classification
Transitions from regression to binary crisis prediction. Exposes the Linear Probability Model's fundamental failure (probabilities outside [0, 1]), then fits logistic regression and interprets odds ratios for non-technical policy briefings.

### Phase 3 — Evaluation Under Operational Constraints
Applies the full classification metrics toolkit under IMF constraints: accuracy paradox, confusion matrix, ROC vs. Precision-Recall curves, and threshold optimization under a hard 5-mission-per-quarter capacity ceiling.

### Phase 4 — Advanced Extensions
Bootstrap stability analysis across 200 Lasso resamples identifies which WDI predictors are robust vs. collinearity-fragile. Cost-sensitive threshold optimization derives the IMF's operational decision point from its actual loss function ($50B missed crisis vs. $2M false alarm).

---

## Key Results (values update with each run)

- **OLS** achieves near-perfect training R² but collapses on test data — high p/n ratio leaves too few degrees of freedom
- **Lasso** outperforms Ridge on test R² and automatically zeros out redundant indicators
- **Accuracy paradox** — a naïve "never flag" baseline matches or beats logistic accuracy due to class imbalance
- **Cost-minimizing threshold** sits well below the F1-optimal threshold — the 25,000× cost asymmetry between FN and FP dominates any balanced metric
- **Bootstrap stability** reveals which predictors are genuine signals vs. proxies that swap with correlated neighbours across resamples

---

## Notes

- The `external_debt_gdp` indicator may return an API warning (`JSONDecodeError`) on some runs — this is a World Bank API issue with that series, not a code error. The pipeline skips it and continues with the remaining 30 indicators.
- Step 4.1 (bootstrap Lasso) takes approximately 3–8 minutes in Colab depending on the number of active features.
- All `random_state=42` seeds are fixed for reproducibility, but live API downloads may vary slightly between runs as the World Bank updates its data.
