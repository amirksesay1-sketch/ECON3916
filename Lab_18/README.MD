# Fraud Detection Model Evaluation — Metrics that Matter

## Objective

Rigorously evaluate a logistic regression classifier on a severely imbalanced real-world dataset by moving beyond accuracy to operationally meaningful metrics — demonstrating that model selection and threshold choice are fundamentally economic decisions, not purely statistical ones.

---

## Data

**Kaggle Credit Card Fraud Detection Dataset**
- 284,807 European credit card transactions (September 2013)
- 492 confirmed frauds — a positive-class rate of **0.172%**
- Features V1–V28 are PCA-transformed (anonymized for privacy); `Amount` and `Time` are raw
- Binary target: `Class` = 1 (fraud), 0 (legitimate)

The extreme class imbalance is not a preprocessing artifact — it reflects the real-world signal-to-noise ratio that any production fraud system must confront.

---

## Methodology

**1. Establishing the Baseline Illusion**
- Constructed a naïve classifier that predicts "not fraud" for every transaction
- Demonstrated the **accuracy paradox**: 99.83% accuracy with zero fraud recall — a degenerate solution that a naive metric would reward

**2. Feature Engineering & Model Training**
- Dropped `Time`; applied `StandardScaler` to `Amount` (V1–V28 are already PCA-normalized)
- Performed a stratified 80/20 train/test split to preserve the fraud prevalence in both sets
- Trained a `LogisticRegression` classifier (L2 regularization, `max_iter=1000`)

**3. Confusion Matrix & Classification Report**
- Evaluated predictions at the default threshold τ = 0.5
- Extracted per-class Precision, Recall, and F1-Score; highlighted the fraud row as the operationally relevant signal
- Quantified True Positives, False Negatives (missed fraud), and False Positives (legitimate transactions wrongly blocked)

**4. ROC & Precision-Recall Curve Analysis**
- Plotted the full ROC curve and computed `roc_auc_score` — interpreted as the probability the model ranks a random fraud above a random legitimate transaction
- Plotted the Precision-Recall curve and computed PR-AUC — a stricter benchmark that ignores True Negatives and focuses entirely on fraud-class performance
- Compared both curves against their respective random-classifier baselines

**5. Threshold Sensitivity Analysis**
- Swept τ from 0.01 to 0.99 in steps of 0.01, computing Precision, Recall, and F1 at each point
- Identified the **F1-optimal threshold** — the operating point that maximizes the harmonic mean of Precision and Recall
- Visualized the precision-recall tradeoff to illustrate how the "best" threshold is cost-context dependent

**6. Capacity-Constrained Operating Point Selection**
- Applied a real-world business constraint: the fraud investigation team can review at most **500 flagged transactions per day**
- Programmatically identified the highest-recall threshold that respects this capacity ceiling
- Reported Precision, Recall, F1, and case counts at the capacity-constrained operating point

---

## Key Findings

| Metric | Naïve Baseline | Logistic Regression (τ = 0.5) |
|---|---|---|
| Accuracy | 99.83% | ~99.9% |
| Recall (fraud) | 0.00% | Meaningful |
| Precision (fraud) | — | Meaningful |
| ROC-AUC | 0.50 | Strong (> 0.95) |
| PR-AUC | ~0.0017 | Substantially above baseline |

**The accuracy paradox confirmed.** A classifier that never predicts fraud scores near-perfect accuracy on this dataset. Accuracy is not a valid evaluation metric when the positive class is rare — a finding with direct implications for model selection in any imbalanced production setting.

**The F1-optimal threshold is not 0.5.** The default decision boundary systematically under-flags fraud on imbalanced data. Threshold calibration is a first-order concern, not an afterthought.

**Business constraints dominate statistical optima.** The capacity-constrained operating point (τ selected to flag ≤ 500 transactions/day) yields a materially different — and more actionable — operating point than the F1-optimal threshold. The "correct" threshold is the one aligned with the organization's cost structure: the ratio of the cost of a missed fraud (FN) to the cost of a false investigation (FP).

**PR-AUC is the honest benchmark for imbalanced classification.** ROC-AUC is inflated by the large True Negative pool. PR-AUC removes TN from the evaluation entirely, measuring only how precisely the model ranks positive instances — the relevant question when positives are rare and costly.

---

## Tech Stack

`Python` · `scikit-learn` · `pandas` · `numpy` · `matplotlib` · `seaborn`

---

## Reproducibility

```
Dataset: https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud
Place creditcard.csv in the project root and run lab_18_model_evaluation.ipynb top-to-bottom.
Random seed: 42 (train_test_split and LogisticRegression)
```
