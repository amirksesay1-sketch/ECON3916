Recovering Experimental Truths via Propensity Score Matching
Objective
Applied Propensity Score Matching (PSM) to correct for selection bias in observational labor market data, successfully recovering a credible causal estimate of job training program effectiveness from a heavily confounded naive comparison.
Methodology

Diagnosed observational failure by computing a naive difference-in-means between the NSW trainees and PSID comparison group, revealing a severely biased estimate driven by systematic differences in age, prior earnings, and employment status
Modeled the selection process using logistic regression to estimate each individual's propensity score — the probability of receiving treatment given observed covariates including age, education, race, marital status, and pre-treatment earnings
Applied 1:1 Nearest Neighbor Matching with replacement to pair each treated unit with its closest control counterpart in propensity score space, constructing a balanced pseudo-experimental sample
Validated covariate balance post-matching using Standardized Mean Differences (SMD), confirming all covariates fell below the 0.1 threshold

Key Findings
EstimateValueNaïve Observational Estimate-$15,204PSM-Recovered Causal Estimate+$1,800NSW Experimental Benchmark~$1,700
The naive comparison dramatically understated program effectiveness due to the PSID control group's structural advantages. After matching on propensity scores, the recovered treatment effect aligned closely with the randomized experimental benchmark — demonstrating that PSM, when correctly implemented, can credibly approximate causal inference from observational data.
Tools & Technologies
Python, Pandas, Scikit-Learn, SciPy
