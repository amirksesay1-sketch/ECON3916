# The Architecture of Dimensionality: Hedonic Pricing & the FWL Theorem

## Objective
Executed a multivariate hedonic pricing model on 2026 California real estate data to quantify the independent price effects of physical depreciation and location premium, while manually proving the Frisch-Waugh-Lovell (FWL) theorem to demonstrate how OLS achieves algebraic ceteris paribus.

---

## Data
- **Source:** Zillow synthetic dataset — 1,000 California residential transactions (2026)
- **Features:** `Property_Age` (years), `Distance_to_Tech_Hub` (miles), `Sale_Price` (USD)

---

## Tech Stack
- Python 3.10+
- `pandas` — data ingestion and residual storage
- `statsmodels.formula.api` — OLS model specification and estimation
- `matplotlib` / `plotly.graph_objects` — diagnostic plots and 3D hyperplane visualization

---

## Methodology

- **Baseline bivariate regression** — regressed `Sale_Price` on `Property_Age` alone to establish a naive benchmark and expose the sign anomaly introduced by omitted variable bias
- **Multivariate OLS expansion** — introduced `Distance_to_Tech_Hub` as a second regressor, allowing the hyperplane to partition variance across both dimensions simultaneously
- **FWL residual partialling (Step 1)** — regressed `Sale_Price` on the confounder and extracted residuals, isolating the price variation unexplained by location
- **FWL residual partialling (Step 2)** — regressed `Property_Age` on the confounder and extracted residuals, purging age of its correlation with proximity
- **FWL final regression (Step 3)** — regressed price residuals on age residuals with no intercept, recovering the isolated partial coefficient for `Property_Age`
- **Epistemological proof** — confirmed exact numerical equivalence between the FWL-derived coefficient and the multivariate OLS coefficient out to four decimal places

---

## Key Findings

**Omitted Variable Bias (OVB):** The naive bivariate model produced a `Property_Age` coefficient of **+$5,573.63**, falsely implying that older homes command higher prices. This sign reversal occurred because older properties in California tend to be located closer to established urban tech corridors — a strong positive price driver that the bivariate model could not separate from age.

**Multivariate Correction:** Introducing `Distance_to_Tech_Hub` as a control variable caused the `Property_Age` coefficient to flip to **−$2,063.13**, correctly reflecting physical depreciation. Each additional mile from a tech hub independently reduced sale price by **$7,964.24**. Model fit improved from R² = 0.757 to R² = 0.954.

**FWL Theorem Proof:** Manually partialling out the confounder from both the target and the feature of interest — then regressing the resulting residuals against each other — reproduced the multivariate coefficient of **−$2,063.1292** exactly. This confirms that OLS does not estimate coefficients jointly; it implicitly executes a residual-on-residual regression for each predictor, achieving algorithmic ceteris paribus by geometric projection onto an orthogonal subspace.
