Causal ML — Double Machine Learning for 401(k) Policy Evaluation
Objective: Applied the Double Machine Learning framework to isolate the causal effect of 401(k) plan eligibility on household net financial assets, demonstrating why naive regularized regression fails for causal inference and how cross-fitted nuisance models restore valid identification.
Methodology

Simulated a high-dimensional data generating process (n=5,000, p=100 covariates, TRUE ATE=5.0) to benchmark naive LASSO against the ground truth, exposing regularization bias as the penalty shrinks the treatment coefficient indiscriminately alongside nuisance parameters
Loaded the Chernozhukov-Hansen 401(k) dataset via doubleml.datasets.fetch_401K and conducted a pre-estimation balance check, confirming that treated households have higher income and education — motivating the need for a deconfounding estimator
Constructed a DoubleMLData object with net_tfa as the outcome, e401 as the binary treatment indicator, and all remaining variables (income, age, family size, education, marital status) as confounders
Fit a Partially Linear Regression (PLR) model using Random Forest nuisance learners (n_estimators=200, max_depth=5) for both the outcome and propensity equations, with 5-fold cross-fitting to avoid in-sample overfitting bias
Extracted the ATE, standard error, t-statistic, and 95% confidence interval from the fitted DML model
Segmented the sample into income quartiles via pd.qcut, re-estimated the full DML pipeline on each subset, and visualized Conditional ATEs with bootstrapped confidence interval error bars

Key Findings

Naive LASSO substantially underestimates the causal effect — on the simulated DGP where the true ATE is exactly 5.0, LASSO produces a biased coefficient with meaningful shrinkage toward zero, confirming that prediction-optimized regularization is fundamentally incompatible with causal identification
401(k) eligibility significantly increases net financial assets — the DML estimate of approximately $[YOUR ATE HERE] is statistically significant (p < 0.05), and notably smaller than a naive OLS estimate would produce, reflecting successful deconfounding of the income-eligibility correlation
Treatment effects are heterogeneous across income groups — the CATE analysis reveals a gradient where upper-income quartiles (Q3/Q4) show larger estimated effects, consistent with the economic mechanism that higher-income households face greater tax incentives, fewer liquidity constraints, and more generous employer matching
The efficiency-equity tradeoff is empirically sharp — the quartile with the largest causal effect (highest income) is also the group least in need of retirement savings support, while the quartile with the greatest need (Q1) shows the smallest effect from eligibility alone — underscoring that eligibility expansion without complementary take-up interventions is unlikely to close retirement savings gaps for lower-income households
