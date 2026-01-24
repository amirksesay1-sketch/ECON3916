📊 The Cost of Living Crisis: A Data-Driven Analysis
The Problem

Headline inflation statistics such as the Official Consumer Price Index (CPI) are reported as national averages. While useful for macroeconomic benchmarking, these averages often fail to reflect the lived experience of specific populations. For college students—particularly those living in high-cost metropolitan areas like Boston—spending is heavily concentrated in categories such as tuition, rent, and food away from home, which have historically outpaced overall inflation.

This project asks a simple but critical question:
Does the “average” CPI meaningfully capture the cost-of-living reality faced by students?

Methodology: Python, APIs, and Index Theory

This analysis was conducted in Python, using data retrieved programmatically from the Federal Reserve Economic Data (FRED) API via fredapi.

To ensure valid comparisons across cost categories, I applied core principles of index number theory, specifically the Laspeyres price index framework, which underlies CPI construction. Because CPI series are reported with different base years (e.g., 1982–84 vs. 2002), all series were re-indexed to a common base year (2016 = 100). This normalization step is critical to avoid misleading scale comparisons.

To reflect student-specific spending behavior, I constructed a custom Student Spending Price Index (Student SPI) using weighted CPI proxies:

Tuition & fees

Rent of primary residence

Food away from home (fast-casual dining proxy)

Streaming services (digital consumption proxy)

Weights were adjusted to reflect the fact that tuition and rent dominate student budgets, unlike in the official CPI basket.

Finally, I incorporated regional inflation data by fetching CPI for the Boston–Cambridge–Newton metropolitan area, allowing for a three-way comparison between:

National CPI

Boston CPI

Student SPI

Key Findings

Student-experienced inflation diverges meaningfully from the national CPI.

From 2016 onward, the Student SPI consistently grows faster than the Official CPI, revealing a persistent inflation gap driven by education and housing costs.

Boston-area inflation further amplifies this divergence, indicating that regional cost pressures compound the burden on students beyond what national averages suggest.

By the end of the sample period, my analysis reveals a clear percentage divergence between student costs and national inflation, demonstrating that students experience inflation more intensely than headline statistics imply.

Why This Matters

Policy discussions, wage adjustments, and financial aid calculations often rely on headline CPI figures. This project shows that aggregate inflation metrics can obscure localized and demographic-specific cost pressures, leading to systematic underestimation of financial strain for students.

By combining economic theory with reproducible data science workflows, this analysis highlights the importance of context-aware inflation measurement—and demonstrates how tailored indices can surface realities hidden by averages.

Tools & Skills Demonstrated

Python (pandas, matplotlib)

API data ingestion (FRED / fredapi)

Economic index construction & normalization

Data visualization and narrative communication

Applied macroeconomic reasoning
