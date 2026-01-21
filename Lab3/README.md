Guatemala Economic Dashboard

Executive Visualization of Key Macroeconomic Indicators

Project Overview

This project builds a 2×3 executive-style economic dashboard to summarize key macroeconomic indicators for Guatemala using Python’s data visualization stack. The goal is to transform raw economic data into a concise, decision-ready visual snapshot that highlights growth, stability, and macroeconomic balances over time.

The dashboard is designed to mirror how economic data is presented in professional policy, finance, and analytics settings—emphasizing clarity, comparability, and interpretability rather than isolated charts.

Data Description

The analysis uses a cleaned pandas DataFrame (df_gtm) containing annual macroeconomic indicators for Guatemala. Key variables include:

Real GDP (Constant Prices) – measures long-run economic growth

Inflation (CPI) – captures price stability

Unemployment Rate – reflects labor market conditions

Tax Revenue (% of GDP) – government revenue capacity

Government Expenditure (% of GDP) – fiscal outlays

Exports & Imports (% of GDP) – external sector activity

Gross Domestic Savings (% of GDP) – internal capital availability

Gross Capital Formation (% of GDP) – investment levels

Time is represented using a Year column (or the DataFrame index if unavailable).

Dashboard Structure

The executive dashboard consists of six coordinated visualizations:

Top Row

Real GDP (Line Chart)
Displays long-term economic growth trends in constant prices.

Inflation Rate (Bar Chart)
Highlights annual inflation with a horizontal zero line to emphasize deflationary or inflationary periods.

Unemployment Rate (Line Chart)
Tracks labor market dynamics over time.

Bottom Row

Fiscal Position (Area Fill)
Visualizes the gap between Tax Revenue and Government Expenditure to illustrate fiscal balance or deficit pressures.

Trade Position (Area Fill)
Shows the relationship between Exports and Imports, providing insight into trade surpluses or deficits.

Savings vs Investment (Dual Line Chart)
Compares domestic savings with capital formation to assess macroeconomic sustainability.

Methodology

Matplotlib is used for precise subplot control and professional layout.

Seaborn styling complements Matplotlib while preserving flexibility.

A dark background theme is applied to improve contrast and readability in presentation settings.

fill_between() is used for fiscal and trade balance visualizations to emphasize gaps rather than standalone lines.

Gridlines and consistent labeling ensure interpretability across all panels.

tight_layout() prevents overlap between subplots and titles.

Key Takeaways

This dashboard enables users to:

Quickly assess Guatemala’s growth trajectory

Identify inflationary or labor market pressures

Evaluate fiscal discipline and trade imbalances

Compare domestic savings and investment trends in a single view

The layout is intentionally compact and presentation-ready, making it suitable for executive briefings, policy discussions, or portfolio-style economic analysis.

Tools & Libraries

Python

pandas

matplotlib

seaborn

Jupyter Notebook

Future Extensions

Potential enhancements include:

Annotating major economic shocks or policy changes

Adding rolling averages for volatility smoothing

Formatting axes with percentage and currency standards

Exporting the dashboard for reporting or presentation use
