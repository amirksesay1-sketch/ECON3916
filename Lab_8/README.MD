Hypothesis Testing & Causal Evidence Architecture
Objective

This project operationalizes the scientific method as a falsification engine rather than a mere estimation exercise. Using the Lalonde (1986) dataset, I pivoted from simply estimating treatment effects to rigorously adjudicating between competing causal narratives. The objective was not just to measure an Average Treatment Effect (ATE), but to formally attempt to reject the null hypothesis through structured statistical contradiction.

Technical Approach

Implemented Welch’s T-Test (Scipy) to compute the signal-to-noise ratio and estimate the Average Treatment Effect (ATE) of the job training intervention under unequal variance assumptions.

Conducted a Non-Parametric Permutation Test (10,000 resamples) to validate inference robustness against non-normal earnings distributions and distributional asymmetries.

Explicitly controlled for Type I error, ensuring statistical significance thresholds were not artifacts of distributional assumptions.

Structured the analysis as a falsification workflow: hypothesis → statistical stress test → contradiction or survival.

Key Findings

The analysis identified a statistically significant lift in real earnings (~$1,795), allowing rejection of the Null Hypothesis. Results were consistent across both parametric and non-parametric frameworks, strengthening causal confidence through methodological triangulation.

Business Insight

Rigorous hypothesis testing functions as the safety valve of the algorithmic economy. In high-velocity data environments, unchecked estimation invites data grubbing, p-hacking, and spurious correlation mining. Structured falsification frameworks prevent overfitting narratives to noise and enforce disciplined evidence architecture. In production systems, this safeguards capital allocation, experimentation pipelines, and model deployment decisions from false positives that erode trust and ROI.

Portfolio Note: Return-Aware Experimentation

In industry contexts such as Netflix, experimentation is return-aware—decision thresholds are calibrated to expected business impact, not fixed scientific conventions. Unlike the academic standard of p < 0.05, decision criteria are adjusted based on risk tolerance, opportunity cost, and projected revenue lift. Statistical significance is therefore a tool, not a rule. I understand that “decision thresholds” are economic parameters optimized for expected return, rather than universal scientific constants.
