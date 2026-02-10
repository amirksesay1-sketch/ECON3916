Lab 5: The Architecture of Bias
Overview

This project investigates how bias is introduced before modeling even begins—through the Data Generating Process (DGP), sampling decisions, and engineering failures. Rather than optimizing a predictive model, the lab focuses on diagnosing why models fail silently when data is not representative.

The core objective was to understand how sampling error, covariate shift, and sample ratio mismatch (SRM) distort inference and decision-making in both machine learning and real-world experimentation systems.

Objective

To analyze and diagnose sampling bias and ghost data in machine learning pipelines by:

Manually simulating flawed sampling processes

Applying industry-standard fixes

Using statistical forensics to detect broken experiments

Tech Stack

Python

pandas / numpy

scipy (Chi-Square tests)

scikit-learn (Stratified Sampling)

Methodology
1. Manual Simple Random Sampling (SRS)

Using the Titanic dataset, I manually shuffled indices and performed an 80/20 train-test split without automation.

Insight:
Even with random sampling, the training and test sets exhibited different survival rates. This variance is not a modeling issue—it is sampling error caused by randomness failing to produce a representative subset.

2. Stratified Sampling to Fix Covariate Shift

I then implemented stratified sampling using sklearn, forcing identical distributions of passenger class (pclass) across training and test sets.

Insight:
Stratification eliminates covariate shift by aligning the marginal distributions of key variables, ensuring that model performance differences are attributable to learning—not data leakage or imbalance.

3. Sample Ratio Mismatch (SRM) Forensic Audit

To simulate real-world experimentation failures, I implemented a Chi-Square SRM diagnostic to detect imbalance in A/B test group assignments.

Insight:
A significant deviation from an expected 50/50 split is not “bad luck.” It is a system failure—often caused by load balancers, feature flags, or user bucketing bugs—and invalidates causal inference.

Key Concept: “Ghost Data” and Survivorship Bias
The Problem

Analyzing only successful Unicorn startups (e.g., companies featured on TechCrunch) introduces Survivorship Bias. This dataset excludes the vast majority of startups that:

Failed

Pivoted

Never raised late-stage funding

Were never covered by media

As a result, conclusions about “what makes startups succeed” are systematically biased.

The Ghost Data (Heckman Correction)

To correct this bias using a Heckman Selection Model, we would need selection-stage ghost data, specifically:

Data on all startups, not just successful ones

Variables that influence visibility or selection (e.g., geography, founder network access, initial funding, media exposure likelihood)

A selection equation modeling the probability of being observed (covered by TechCrunch)

An outcome equation modeling success conditional on selection

Without this ghost data, observed success metrics are confounded by the selection process itself.

Key Insight:

The biggest bias is not in the data you see—it’s in the data you never collected.

Why This Matters

This lab demonstrates that:

Bias often originates before modeling

Randomness does not guarantee fairness or representativeness

Broken data pipelines can silently invalidate results

Statistical diagnostics are essential for trustworthy ML and experimentation systems

This project reflects how modern data scientists and economists think about causal validity, not just prediction.

Skills Demonstrated

Data Generating Process (DGP) analysis

Sampling bias diagnosis

Stratified experimental design

Statistical forensics (Chi-Square / SRM)

Applied causal reasoning (Survivorship Bias, Heckman Correction)
