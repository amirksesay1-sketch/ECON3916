# Structural Forensics: Diagnosing Spurious Correlation in Macroeconomic Time-Series

## Project Overview

This project demonstrates a rigorous, end-to-end methodology for identifying and correcting spurious correlations in macroeconomic time-series data — one of the most common pitfalls in applied econometrics and financial data science.

## Objective

To expose the "Everything is Correlated" trap inherent in raw macroeconomic level data, diagnose the structural source of that redundancy, and recover interpretable, causally-grounded relationships through principled transformations and graphical modeling.

## Data

Five macroeconomic indicators were sourced from the **Federal Reserve Economic Data (FRED) API** via `pandas_datareader`, covering January 2010 to January 2024:

| Series | Variable | Type |
|--------|----------|------|
| CPIAUCSL | Consumer Price Index | Non-stationary level |
| M2SL | M2 Money Supply | Non-stationary level |
| INDPRO | Industrial Production Index | Non-stationary level |
| UNRATE | Unemployment Rate | Stationary |
| FEDFUNDS | Federal Funds Rate | Stationary |

## Methodology

### 1. Correlation Trap Visualization
Raw pairwise Pearson correlations were computed and visualized as a heatmap using `seaborn`. Variables such as CPI and M2 exhibited near-perfect correlations (~0.98) — not due to structural causation, but because both series share a common upward time trend, producing classically spurious results.

### 2. Multicollinearity Diagnosis via VIF
Variance Inflation Factors (VIF) were calculated for all predictors using `statsmodels`. CPI and Industrial Production returned VIF scores exceeding 50–100, confirming severe multicollinearity. At these levels, OLS coefficient estimates become numerically unstable, standard errors inflate, and signs can reverse — rendering regression output effectively uninterpretable.

### 3. Year-over-Year (YoY) Transformation
Non-stationary trending variables (CPI, M2, Industrial Production) were converted to 12-month percentage growth rates: `YoY % = 100 × (xₜ / xₜ₋₁₂ − 1)`. This transformation removes the deterministic trend component, rendering the series stationary. Post-transformation, VIF scores fell to 1–3 across all variables and previously inflated correlations collapsed substantially, isolating genuine structural co-movement from trend-driven noise.

### 4. Causal Structure Mapping via DAG
A Directed Acyclic Graph (DAG) was constructed using `networkx` to encode prior causal assumptions before modeling. The DAG identified "Expansionary Macro Policy" as an unobserved **fork** — a common upstream cause of both M2 growth and CPI inflation — explaining why their raw correlation overstates the direct M2→CPI causal effect. Additional structural paths were mapped: the Taylor Rule feedback loop (CPI→Fed Funds→CPI), Okun's Law (Industrial Production→Unemployment), and the Quantity Theory of Money (M2→CPI).

### 5. Interactive Visualization
An interactive dual-view heatmap dashboard was built using `plotly`, featuring a dropdown toggle between the raw-levels and YoY-transformed correlation matrices. Fixing the color scale at `[−1, 1]` across both views makes the reduction in spurious correlation immediately legible.

## Key Results

- CPI/M2 correlation: **0.98 → 0.67** after YoY transformation
- CPI/IndPro correlation: **0.97 → 0.27** after YoY transformation  
- All VIF scores reduced from **50–100+ → 1–3** after transformation
- OLS on raw levels: R² ≈ 0.99, Durbin-Watson ≈ 0 (spurious)
- OLS on YoY growth: lower R², Durbin-Watson ≈ 2 (valid inference)

## Tools & Libraries

`Python` · `pandas` · `numpy` · `seaborn` · `matplotlib` · `plotly` · `statsmodels` · `networkx` · `pandas_datareader`

## Skills Demonstrated

- Time-series stationarity analysis and transformation
- Multicollinearity diagnosis (VIF)
- Causal inference and DAG construction
- Interactive dashboard design with Plotly `updatemenus`
- FRED API data ingestion and preprocessing
