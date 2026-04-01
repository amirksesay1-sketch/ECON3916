High-Dimensional GDP Growth Forecasting with Lasso and Ridge Regularization
Objective: Forecast 5-year average GDP per capita growth rates across 120+ countries using 36 World Development Indicators, demonstrating the OLS overfitting failure mode in high-dimensional cross-country settings and applying regularized regression with cross-validated penalty selection to recover out-of-sample predictive performance.

Methodology

Data acquisition: Downloaded World Bank WDI data live via the wbgapi API covering 2013–2019 across trade, macroeconomics, education, infrastructure, health, finance, natural resources, agriculture, and governance dimensions; averaged to a single cross-sectional observation per country and imputed residual missingness with cross-country medians following standard practice in cross-country empirics.
OLS baseline: Fit ordinary least squares on standardized predictors to establish a high-dimensional benchmark; documented the variance explosion problem at elevated p/n ratios through the train–test R² gap.
Regularized estimation: Applied RidgeCV (L2 penalty) and LassoCV (L1 penalty) using 5-fold cross-validation to select the optimal penalty parameter λ from a log-spaced grid; all features standardized prior to fitting to ensure penalty comparability across indicators on different scales.
Lasso Path analysis: Computed the full regularization path via sklearn.linear_model.lasso_path to trace coefficient entry order as λ decreases, identifying which indicators Lasso considers most robustly predictive unconditional on other controls.
Interactive exploration: Built an in-notebook ipywidgets dashboard allowing real-time λ adjustment across Ridge and Lasso, with synchronized coefficient bar chart, Lasso Path plot with moveable λ marker, and train–test R² gap visualization.


Key Findings
OLS achieved a training R² near 1.0 while test R² collapsed substantially — a textbook illustration of variance explosion when the predictor-to-observation ratio approaches or exceeds 0.5. Both RidgeCV and LassoCV meaningfully closed the train–test gap, confirming that regularization recovers generalization in this setting.
Lasso selected a sparse model of roughly 5–10 predictors out of 30+, with the Lasso Path revealing that trade openness, institutional quality, and macroeconomic stability indicators enter first — those most robustly associated with growth regardless of what else is controlled for. Predictors zeroed out by Lasso should be interpreted as conditionally redundant given the selected set, not as economically irrelevant — a distinction with direct implications for policy diagnostics.

Stack
Python · wbgapi · scikit-learn · matplotlib · pandas · numpy · ipywidgets
