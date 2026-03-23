# AI Capex Diagnostic Modeling

## Objective
Rigorously diagnose and correct structural failures in an OLS regression model predicting AI Software Revenue from Nvidia's 2026 capital expenditure and deployment data, applying heteroskedasticity-consistent estimation to restore valid statistical inference.

## Methodology
- **Baseline model construction:** Fitted a naive OLS model regressing AI Software Revenue on Hardware Capex, Data Center Power (MW), and Cloud GPU Deployments to establish a diagnostic benchmark
- **Visual forensics:** Plotted residuals against fitted values to detect non-constant variance patterns across capital expenditure tiers
- **White Test & Breusch-Pagan Test:** Formally confirmed heteroskedasticity using two independent statistical tests, corroborating the visual evidence with LM statistics and p-values
- **Variance Inflation Factor (VIF) analysis:** Iterated across all regressors to quantify multicollinearity, identifying severe regressor redundancy (VIF ≈ 18) between Hardware Capex and Data Center Power
- **HC3 robust correction:** Re-estimated the model using heteroskedasticity-consistent (HC3) sandwich standard errors to produce asymptotically valid inference under non-constant variance

## Key Findings
The naive OLS model produced a deceptively high R² of 0.97 with near-zero p-values — a textbook baseline illusion. Diagnostic testing revealed two simultaneous violations: severe heteroskedasticity expanding at high capital expenditure tiers (White Test p < 0.001), which artificially compressed standard errors and overstated coefficient significance, and critical multicollinearity between Hardware Capex and Data Center Power (VIF ≈ 18), rendering the latter's coefficient statistically meaningless. Applying HC3 robust standard errors appropriately widened confidence intervals and restored honest significance thresholds, demonstrating that Cloud GPU Deployments and Hardware Capex are the structurally valid predictors of AI Software Revenue once false precision is removed.

## Tech Stack
- **Language:** Python
- **Libraries:** pandas, statsmodels, matplotlib, seaborn
- **Dataset:** 2026 Nvidia AI Capital Expenditure and Deployment Data (synthetic)
