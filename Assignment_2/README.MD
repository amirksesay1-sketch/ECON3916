# Task 4.1 — The Memecoin Graveyard  
### Visualizing Survivorship Bias in Crypto Markets

## Overview
This project demonstrates **Survivorship Bias** in financial data using a simulated cryptocurrency market. In highly speculative ecosystems like memecoins, the overwhelming majority of assets fail quietly and disappear from datasets. Analyzing only “successful” or “listed” coins creates a distorted view of risk and return.

Using a simulated **power-law (Pareto) distribution**, this project shows how deleting failed tokens inflates perceived average performance and manufactures misleading narratives about profitability.

---

## Problem Statement
Platforms such as Pump.fun exhibit extreme failure rates (≈98–99%). However, most analyses focus only on surviving or listed tokens.

**Key question:**  
> *How different do market statistics look when failures are included versus when they are erased?*

---

## Methodology

### Data Generating Process (DGP)
- **10,000 simulated token launches**
- **Peak Market Capitalization** drawn from a **Pareto distribution**
  - Models real crypto markets where:
    - Most tokens reach near-zero value
    - A tiny minority achieve extreme success
- Scaling applied to reflect realistic magnitudes

### Dataset Construction
Two datasets are created:
- **`df_all` — “The Graveyard”**
  - Contains *all* token launches
  - Represents the full market reality
- **`df_survivors` — “Listed Coins”**
  - Top 1% of tokens by peak market cap
  - Mimics survivorship-biased datasets used in many reports

---

## Visualization
Dual histograms are plotted using `matplotlib`:
- **All Tokens:** Heavy mass near zero, long tail
- **Survivors Only:** Skewed toward large values, hiding failure

Log-scaled frequency axes are used to correctly visualize extreme skew.

---

## Evaluation Metric
The **Mean Peak Market Capitalization** is calculated for both datasets:
- Mean of all tokens
- Mean of survivors only

This directly quantifies the inflation caused by survivorship bias.

---

## Key Results
- The mean market cap of surviving tokens is **orders of magnitude larger** than the mean across all tokens.
- The same market appears either:
  - Extremely risky and failure-dominated, or
  - Highly profitable and attractive  
  depending solely on **which data is deleted**.

---

## Insight
> In power-law markets, deleting failures does not reduce noise — it **manufactures alpha**.

This failure mode is not unique to crypto. It appears in:
- Startup “unicorn” analyses
- Hedge fund performance databases
- Influencer PnL screenshots
- Backtested trading strategies

---

## Tech Stack
- **Python**
- **NumPy** — stochastic simulation
- **Pandas** — data structuring
- **Matplotlib** — visualization

---

## Files
- `memecoin_graveyard.py` or `.ipynb` — simulation and visualization
- `README.md` — project documentation

---

## Why This Matters
This project highlights why **robust analysis requires ghost data** — the missing failures that never make it into polished datasets. Without them, conclusions about performance, risk, and opportunity are statistically invalid.

---

## Author
*Financial Data Science — Robustness & Bias Audits*
