# Corporate-Finance-Income-Statement-Analysis-Python
Corporate Finance Income Statement Analysis: Tech Sector
Python analysis of quarterly income statements for 11 technology and semiconductor companies, built to identify which ones deliver sustainable, profitable growth and which are buying growth at the cost of margins.

[Image: Python] [Image: Pandas] [Image: Matplotlib] [Image: Seaborn]

Business Problem
Alpha Capital Partners (a hypothetical investment firm) wants to allocate capital in high-growth tech. The team sees margins sacrificed for sales growth, administrative bloat eroding profit, volatile quarterly earnings, and no comparative framework to separate scalable businesses from those buying growth.

Objective: use financial data to identify tech companies with sustainable, profitable growth versus those at risk of operational bloat.

Questions Answered
#	Question	Approach
1	Who grows profit faster than sales?	Growth Quality Score = net income growth − revenue growth
2	Is profitability improving over time?	Operating and net margin trends per company
3	How is spending allocated as companies scale?	R&D ratio vs SG&A ratio (% of revenue)
4	Who are reliable earners vs risky bets?	Standard deviation of net margin and revenue growth
5	Who are the top investment targets?	Growth vs profitability quadrant classification
Companies: NVDA, MSFT, AAPL, GOOG, AMZN, META, ORCL, AVGO, TSM, PLTR, NFLX

Data
Source: Alpha Vantage API quarterly income statements
Pipeline: API → JSON → Pandas DataFrames → ticker column added → consolidated CSV → analysis
Grain: one row per company per fiscal quarter
Methodology
Cleaning: filtered to target tickers, parsed dates, checked duplicates, dropped fully empty columns, filled structural nulls (interest and non-operating income) with 0, dropped rows missing core metrics (gross profit, operating income, net income, EBIT), filled missing currency with USD.
Outliers: IQR rule (Q1 − 1.5×IQR, Q3 + 1.5×IQR) on revenue growth.
Features:
Year-over-year growth via pct_change(4) inside groupby('symbol'), which removes seasonality and prevents cross-company comparisons.
Operating margin, net margin, R&D ratio, SG&A ratio (all divided by revenue so different-sized companies are comparable).
Risk: standard deviation of net margin and revenue growth as volatility measures.
Classification: thresholds of 10% average revenue growth and 15% average net margin.
Key Findings
Growth quality: AVGO (+1.32), AMZN (+0.98), NFLX (+0.83) and PLTR (+0.40) convert sales growth into faster profit growth. MSFT (−0.22) and ORCL (−0.095) show profit growth lagging revenue.

Stability: AMZN, TSM and AAPL have the most stable margins (std 0.03–0.05). PLTR is the riskiest by far (margin std 0.64).

Spending: R&D generally exceeds SG&A, R&D intensity is rising at NVDA, AMZN and PLTR, and SG&A ratios are flat or falling, so no sector-wide bloat.

Investment classification

Category	Companies
Top Picks (growth > 10%, net margin > 15%)	AAPL, AVGO, GOOG, META, MSFT, NVDA, TSM
Risky Growth (growth > 10%, net margin ≤ 15%)	AMZN, NFLX, PLTR
Stable (growth ≤ 10%, net margin > 15%)	ORCL
At Risk	none
Limitations
Percentage growth in net income is unstable on small or negative bases (notably PLTR, AVGO), so very large Growth Quality scores should be read cautiously.
The IQR filter was applied to pooled data and may remove genuine high-growth quarters; a per-company filter is a possible refinement.
The 10% / 15% cut-offs are judgment calls, and results are not yet tested for sensitivity.
Income statement only: no balance sheet, cash flow or valuation, so results describe operating quality, not price attractiveness.
Educational analysis, not investment advice.
Repository Structure
.
├── Corporate_Finance_Data_Analysis.ipynb   # full analysis notebook
├── corporate_income_statement.csv          # consolidated dataset
├── Corporate_Finance_Income_Statement_Analysis.md   # detailed project write-up
└── README.md
How to Run
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
pip install pandas matplotlib seaborn jupyter
jupyter notebook Corporate_Finance_Data_Analysis.ipynb
Update the CSV path in the first data-loading cell to match your local location. To refresh the data, pull income statements from the Alpha Vantage API with your own key (never commit the key to the repo).

Skills Demonstrated
Data cleaning and null-handling strategy · feature engineering with groupby and pct_change · outlier detection (IQR) · time-series visualization with multi-panel plots · volatility and risk analysis · translating financial metrics into business recommendations.

Author
Monalisa Mahanta · Data Analyst · 
