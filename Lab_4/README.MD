Comparative Forensics Report: Core Market vs. The Tail
Overview

This assignment investigates structural differences between normal observations and outliers in a housing dataset using forensic statistical analysis. By separating the data into core (normal) and tail (outlier) segments, the analysis highlights how extreme values shape inequality, volatility, and distributional behavior.

The goal is to move beyond averages and examine how the “tail” of the distribution distorts traditional summary statistics.

Data Description

The dataset includes the following key variables:

MedInc — Median household income

MedHouseVal — Median housing value

outlier_iso — Boolean indicator (True = outlier, False = normal)

Outliers were pre-identified using an isolation-based anomaly detection method.

Methodology
1. Data Segmentation

The dataset is split into two groups:

df_normal: observations classified as normal

df_outlier: observations classified as outliers

This allows for direct comparison between the core market and the distributional tail.

2. Central Tendency

For both groups, the mean and median are calculated for:

Median Income (MedInc)

Median House Value (MedHouseVal)

Comparing mean vs. median helps detect skew and inequality.

3. Volatility & Dispersion

Two measures of spread are used:

Standard Deviation (SD) — sensitive to extreme values

Median Absolute Deviation (MAD) — robust to outliers

This contrast shows how volatility behaves differently in the tail versus the core.

4. Inequality Wedge

An Inequality Wedge is calculated for outliers only:

Inequality Wedge
=
Mean
−
Median
Inequality Wedge=Mean−Median

This metric quantifies how much extreme values pull the mean away from the typical observation.

Visualization

A comparative histogram is produced:

Left Panel: Distribution of MedInc for normal observations

Right Panel: Distribution of MedInc for outliers

Title: “The Pareto World: Core Market vs. The Tail”

This visualization makes the heavy-tailed nature of outliers visually explicit.

Key Insights

Outliers exhibit significantly larger mean–median gaps, signaling inequality.

Standard deviation inflates sharply in the tail, while MAD remains more stable.

The tail exerts disproportionate influence on aggregate statistics, masking the experience of typical observations.

Tools Used

Python

Pandas

NumPy

Matplotlib

Files

analysis.ipynb / analysis.py — main analysis code

README.md — project documentation

Takeaway

This analysis demonstrates why robust statistics and distribution-aware analysis are essential when studying economic data. In a Pareto-like world, averages alone fail to describe reality—especially for those living outside the “core” of the distribution.
