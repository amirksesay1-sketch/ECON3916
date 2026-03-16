# Architecting the Prediction Engine

## Objective
Architect a multivariate Ordinary Least Squares (OLS) prediction engine to forecast real estate valuations across U.S. micro-markets and quantify out-of-sample predictive performance through loss minimization, enabling direct assessment of algorithmic business risk in dollar terms.

---

## The Data
**Zillow ZHVI 2026 Micro Dataset** — Cross-sectional modern real estate market data capturing hedonic property attributes across U.S. micro-markets, including structural, locational, and qualitative features.

---

## Methodology

- **Environment Initialization & Data Ingestion:** Configured the analytical environment with core scientific Python libraries (`pandas`, `numpy`, `statsmodels`) and performed rapid Exploratory Data Analysis (EDA) to understand the scale and variance of the target variable, `Home_Value`.

- **OLS Architecture via Patsy Formula API:** Leveraged the `statsmodels.formula.api` (smf) R-style formula interface to specify a multivariate regression model, regressing `Home_Value` on `Square_Footage`, `Property_Age`, and `Distance_to_Transit`. The Patsy API automatically handles intercept inclusion, eliminating manual matrix construction.

- **Model Fitting & Diagnostic Extraction:** Fitted the OLS model and extracted the full summary statistics table, examining R-squared values, coefficient signs for alignment with economic intuition (e.g., depreciation effect of property age), and t-statistics for predictor significance.

- **Prediction Vector Generation:** Transitioned from classical statistical explanation to predictive engineering by generating a continuous vector of fitted home value predictions using the trained model, establishing the foundation for loss quantification.

- **RMSE Calculation & Financial Interpretation:** Computed the Root Mean Squared Error (RMSE) between ground-truth valuations and model predictions using `statsmodels.tools.eval_measures`, denominated directly in US Dollars to translate abstract model error into actionable business risk.

- **Residual Forensics Dashboard:** Engineered an interactive visual diagnostic using Plotly, plotting fitted values against residual errors with a zero-reference line and crimson-highlighted outliers exceeding two standard deviations — enabling detection of heteroscedasticity, structural breaks, and systematic model blind spots.

---

## Key Findings

The OLS prediction engine successfully transitioned from classical regression explanation to applied predictive modeling on live real estate market data. By calculating the RMSE in raw US Dollar terms, the model's precise financial error margin was quantified — providing a direct, interpretable measure of algorithmic business risk that abstract statistical metrics obscure.

Residual forensics analysis revealed the model's structural blind spots: crimson outlier clusters identified homes where predictive error exceeded two standard deviations, signaling the influence of unmodeled categorical variables (e.g., `School_District_Rating`) creating latent sub-populations within the data. These diagnostics confirm that while the continuous feature set captures meaningful price signal, a full hedonic specification — inclusive of qualitative market factors — is required to minimize loss and close the prediction gap.

---

## Tech Stack
`Python` · `pandas` · `numpy` · `statsmodels` · `Patsy Formula API` · `Plotly`

---

*Zillow ZHVI 2026 Micro Dataset — Cross-sectional real estate market data.*
