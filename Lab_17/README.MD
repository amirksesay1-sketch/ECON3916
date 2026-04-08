
NY Fed Yield Curve Recession Model Replication
Objective
Replicated the Federal Reserve Bank of New York's yield curve recession probability model by fitting a logistic regression on FRED macroeconomic data to generate a monthly time series of recession probabilities 12 months ahead — the same methodology the NY Fed publishes for policymakers and market participants.
Methodology

Data acquisition: Pulled the 10-Year minus 3-Month Treasury yield spread (T10Y3M) and NBER recession indicator (USREC) directly from FRED via fredapi, resampled to monthly frequency and aligned with a 12-month predictive lag
LPM failure demonstration: Fitted an OLS Linear Probability Model as a baseline and documented out-of-bounds predicted probabilities (below 0 and above 1) on real data, motivating the logistic specification
Logistic regression: Fitted a logistic regression using sklearn and statsmodels, extracting the yield spread coefficient, odds ratio, and 95% confidence interval — the standard output format used in regulatory and policy contexts
Probability time series: Generated the full fitted recession probability series using .predict_proba()[:, 1] and visualized it against NBER recession shading in the style of the NY Fed's published chart
Model extension: Added a second predictor (12-month unemployment change) to assess whether labor market momentum improves out-of-sample discriminatory power, evaluated via TimeSeriesSplit cross-validation to prevent data leakage
Interactive dashboard: Deployed a Streamlit application with Plotly visualizations, an adjustable prediction horizon slider (6, 12, 18 months), a bootstrapped 90% confidence band, and a live sidebar displaying current model inputs and real-time recession probability

Key Findings
The logistic model successfully replicates the NY Fed's core result: an inverted yield curve is a statistically significant predictor of recession 12 months ahead, with a negative odds ratio confirming that a steeper curve reduces recession odds. The 2022–2024 inversion period produced elevated model-predicted recession probabilities — consistent with the historical signal — yet no NBER recession materialized, illustrating that probabilistic forecasts communicate risk, not certainty, and should be evaluated on calibration across many episodes rather than on any single outcome. Adding 12-month unemployment change as a second predictor improved AUC under TimeSeriesSplit, confirming that labor market momentum captures recession risk orthogonal to the yield spread alone.
Tech Stack
Python · pandas · numpy · scikit-learn · statsmodels · matplotlib · plotly · streamlit · fredapi
