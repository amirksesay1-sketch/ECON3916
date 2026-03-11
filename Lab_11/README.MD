# Data Wrangling & Engineering Pipeline

## Objective
Engineer a production-ready econometric dataset by diagnosing and resolving structural data quality failures — including missingness mechanisms, multicollinearity traps, and high-cardinality categorical features — in preparation for downstream OLS modeling.

## Methodology
- **Data Ingestion & Audit:** Loaded `messy_hr_economics.csv` into a pandas DataFrame and conducted a full variable-level audit of dtypes and null distributions
- **Visual Missingness Forensics:** Applied `missingno` matrix visualization to diagnose the underlying missingness mechanism, identifying structural gap alignment consistent with Missing at Random (MAR)
- **Conditional Median Imputation:** Resolved MAR-driven nulls in `base_salary` via grouped median imputation, stratified by department — preserving inter-group variance structures rather than collapsing to a global central tendency
- **Dummy Variable Trap (Controlled Failure):** Intentionally generated a full-rank dummy matrix without dropping a reference class, demonstrating perfect linear dependence and OLS matrix singularity under `statsmodels`
- **Reference Class Encoding (k-1 Fix):** Re-specified the dummy matrix using `drop_first=True`, establishing a silent reference category and restoring OLS estimability
- **Target Encoding:** Applied `category_encoders.TargetEncoder` to compress high-cardinality geographic data into a continuous salary-mean vector, eliminating dimensionality explosion from one-hot encoding

## Key Findings
Missingness in the compensation variables followed a MAR structure, confirmed by co-aligned gap patterns in the missingness matrix — indicating that nulls were systematically related to observable department-level characteristics rather than occurring at random. The dummy variable experiment confirmed that including all $k$ categories alongside an intercept produces a rank-deficient design matrix, rendering OLS coefficients non-identifiable; dropping one reference class resolved the singularity cleanly. Target encoding of the geographic column produced a compact, information-dense continuous feature that retained salary signal while avoiding the curse of dimensionality inherent in high-cardinality one-hot representations.
