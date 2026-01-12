📉 The Illusion of Growth & the Composition Effect

Lab 2: Deflating History with FRED

🎯 Objective

The goal of this project was to build a reproducible Python pipeline that ingests live economic data from the Federal Reserve (FRED API) to analyze long-run wage trends in the United States. Specifically, this lab investigates whether apparent wage growth reflects genuine improvements in workers’ purchasing power—or whether it is driven by inflation and statistical bias.

🧪 Methodology

This analysis follows a concept-extension approach, moving from traditional economic measures to bias-corrected indicators:

API-Driven Data Collection

Retrieved nominal wage data (Average Hourly Earnings, AHETPI) and inflation data (CPI) directly from the Federal Reserve using fredapi.

Constructed real wages by deflating nominal wages with CPI to isolate purchasing power.

Anomaly Detection: The Pandemic Spike

Identified a sharp increase in real wages during 2020 that appeared inconsistent with labor-market fundamentals.

Treated this spike as a statistical anomaly requiring further investigation.

Bias Correction via the Employment Cost Index (ECI)

Introduced the Employment Cost Index (ECI) as a composition-adjusted wage measure.

Used ECI to control for the Composition Effect, where the exit of lower-wage workers during the pandemic artificially inflated average wage statistics.

Compared rebased wage indices to demonstrate divergence between biased averages and composition-fixed measures.

🔍 Key Findings — The Pandemic Paradox

The Money Illusion:
Over the long run, nominal wages have increased substantially, but real wages—after adjusting for inflation—have remained largely flat, highlighting persistent wage stagnation despite economic growth.

The Pandemic Paradox (2020):
The apparent “wage boom” during the COVID-19 period was not driven by increased labor demand or rising compensation. Instead, it was a statistical artifact caused by disproportionate job losses among lower-wage workers.

Standard average wages spiked.

The Employment Cost Index remained stable, revealing no true surge in labor compensation.

This lab demonstrates how naïve averages can mislead economic interpretation, and why correcting for composition bias is essential for credible empirical analysis.
