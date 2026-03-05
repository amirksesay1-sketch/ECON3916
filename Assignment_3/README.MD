# Assignment 3: The Causal Architecture
## SwiftCart Logistics — Senior Data Economist Audit
**Module 3: Bootstrapping, Permutation & Causal Inference**

---

## Overview

This assignment simulates a real-world data economics mandate at SwiftCart Logistics. Across four phases, parametric assumptions are deliberately discarded in favour of computation-heavy empirical methods to resolve three executive-level disputes around driver compensation equity, routing algorithm efficacy, and subscription ROI.

---

## Repository Structure

```
├── step_1_1.py          # Zero-inflated tip distribution (data generation)
├── step_1_2.py          # Manual bootstrap engine — 95% CI for median tip
├── step_2_1.py          # A/B test data generation — routing algorithm
├── step_2_2.py          # Manual permutation test — exact empirical p-value
├── step_3_1.py          # Naive SDO — SwiftPass spending comparison
├── step_3_2.py          # Propensity Score Matching — causal ATT
├── step_4_1.py          # Love Plot — covariate balance visualization
└── swiftcart_loyalty.csv
```

---

## Phases & Steps

### Phase 1 — Bootstrapping (Driver Tip Equity)
**Problem:** Tip data is zero-inflated (40% zeros) and heavily right-skewed. CLT is invalid.

| Step | Task |
|------|------|
| 1.1 | Simulate 250-driver audit sample: 100 zeros + 150 Exponential(scale=5.0) tips |
| 1.2 | Manual bootstrap engine — 10,000 resamples, compute 95% CI for the median via `np.percentile` |

**Key finding:** Bootstrap 95% CI = [$0.26, $1.36]. Asymmetric interval exposes the PR distortion — SwiftCart's mean-based claim of $2.77 vs. the true median of $0.76.

---

### Phase 2 — Permutation Test (Routing Algorithm A/B Test)
**Problem:** Treatment group contains crash-loop outliers, violating homoscedasticity. T-test is invalid.

| Step | Task |
|------|------|
| 2.1 | Generate A/B data — Control: Normal(35, 5), Treatment: LogNormal(3.4, 0.4), n=500 each |
| 2.2 | Manual permutation test — 5,000 shuffles via `np.random.permutation`, exact empirical p-value |

**Key finding:** p-value = 0.0004. The batch-routing algorithm significantly reduces delivery times with no distributional assumptions required.

---

### Phase 3 — Causal Inference (SwiftPass ROI)
**Problem:** High-volume power users self-select into SwiftPass, inflating naive spending comparisons.

| Step | Task |
|------|------|
| 3.1 | Naive SDO — raw mean difference between subscribers and non-subscribers |
| 3.2 | PSM — logistic regression propensity scores + nearest-neighbour matching → ATT |

**Key finding:** Naive SDO overstates the effect. PSM isolates the true causal ATT, stripping out pre-existing power-user behaviour. Marketing's budget case must be evaluated against the ATT, not the SDO.

---

### Phase 4 — Visualization (Love Plot)
**Problem:** Need to visually prove PSM successfully eliminated selection bias.

| Step | Task |
|------|------|
| 4.1 | Love Plot — Standardized Mean Differences before/after matching via `seaborn` + `matplotlib` |

**Validation criteria:** All post-match SMDs must fall below the 0.1 threshold, and every covariate's arrow must point left.

---

## Libraries Used

| Library | Purpose |
|---------|---------|
| `numpy` | All bootstrap and permutation engines (manual loops) |
| `sklearn.linear_model.LogisticRegression` | Propensity score estimation |
| `sklearn.neighbors.NearestNeighbors` | 1-to-1 nearest neighbour matching |
| `matplotlib` / `seaborn` | Phase 4 visualizations only |
| `pandas` | Data structuring for Love Plot |


```

---

## Academic Protocol

- Phases 1 & 2 use **only** native `numpy` and manual `for` loops
- No high-level statistical wrappers permitted for bootstrap or permutation engines
- LLM assistance authorized exclusively for Phase 4 visualization expansion
