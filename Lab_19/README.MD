## Objective
Demonstrate that ensemble tree methods substantially outperform both
linear regression and single decision trees on non-linear tabular data,
and establish a rigorous framework for hyperparameter selection and
feature importance interpretation grounded in predictive — not causal — logic.

## Data
California Housing dataset (sklearn) — 20,640 observations, 8 features.
Target: median house value (100k USD). Features include median income,
house age, average rooms/bedrooms/occupancy, population, latitude, longitude.

## Methodology
- Trained and benchmarked three models: unpruned Decision Tree, Ridge
  Regression (Ch 16), and Random Forest (100 trees)
- Tuned RF hyperparameters (n_estimators, max_depth, max_features) via
  5-fold GridSearchCV scored on negative MSE
- Extracted MDI and permutation feature importance; compared rankings
  and diagnosed high-cardinality bias in MDI
- Built an RF classifier (expensive vs. affordable homes) and benchmarked
  ROC-AUC against Logistic Regression
- Built an interactive Plotly + ipywidgets dashboard with live sliders
  for n_estimators and max_features

## Key Findings
- RF Test R² substantially exceeded Ridge, confirming non-linear
  feature relationships that OLS cannot capture
- Single Decision Tree showed near-perfect train R² with significant
  test degradation — a canonical overfitting demonstration
- MedInc ranked #1 in both MDI and permutation importance; geographic
  features were overstated by MDI due to high cardinality
- RF classifier AUC exceeded Logistic Regression, consistent with
  non-linear decision boundaries in the feature space
- Feature importance ≠ causal effect: MedInc ranking cannot be
  interpreted as evidence that income changes cause price changes

## How to Run
  pip install scikit-learn pandas numpy matplotlib plotly ipywidgets
  jupyter notebook notebooks/lab_19_random_forests.ipynb

## Tech Stack
Python · scikit-learn · pandas · numpy · matplotlib · plotly · ipywidgets
