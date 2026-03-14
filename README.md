#E-Commerce-Customer-Analytics
A full end-to-end analytics project built on the Online Retail dataset from Kaggle. The project covers data cleaning, customer segmentation, cohort retention analysis, churn prediction and an interactive Power BI dashboard.

# Project Overview
This project answers four business questions:
1. Who are our most valuable customers and how are they segmented?
2. How well do we retain customers over time?
3. Which customers are at risk of churning?
4. What does overall revenue and customer health look like?

# Tools Used
- MySQL for data extraction and cohort queries
- Python (pandas, matplotlib, seaborn, mlxtend) for analysis and modeling
- Power BI for interactive dashboard and visualization

# Analysis Steps
1. Data Cleaning (Python)
The raw dataset contained a significant amount of noise. Cancelled orders (identified by invoice numbers starting with "C"), rows with null CustomerIDs and entries with negative quantities were all removed. Date fields were parsed and standardized. After cleaning, the dataset was reduced to a reliable set of completed transactions ready for analysis.

2. SQL Queries (MySQL)
SQL was used to extract and aggregate data before moving into Python. Key queries included cohort assignment based on each customer's first purchase date, monthly retention rates per cohort using window functions, and RFM score calculation using NTILE ranking to divide customers into equal quartiles across Recency, Frequency and Monetary dimensions. Writing these queries first helped clarify the data structure before building the Python models.

3. RFM Segmentation (Python)
Each customer was scored from 1 to 5 on three dimensions: how recently they purchased (Recency), how often they purchased (Frequency) and how much they spent in total (Monetary). Combining these scores allowed customers to be grouped into meaningful business segments such as Champions, Loyal Customers, Promising, At Risk, Lost, Big Spenders and Others. The thresholds for each segment were based on standard RFM methodology, adapted to fit the distribution of this specific dataset.

4. Cohort Retention Analysis (Python + SQL)
Customers were grouped into monthly cohorts based on when they made their first purchase. For each cohort, the percentage of customers who returned to purchase in each subsequent month was tracked up to 12 months. This produced a retention matrix that makes it easy to see how different cohorts behave over time and whether retention is improving or worsening across acquisition periods.

5. Churn Analysis (Python)
A churn threshold of 181 days was defined, meaning any customer who had not purchased within the last 181 days was classified as churned. This threshold was chosen based on the dataset's purchase frequency distribution, where the natural drop-off in activity became clear around that point. Customers were then classified into four groups: Active, At Risk, Churned and Hibernating. Churn rates were also calculated per value tier (Low, Medium, High, VIP) to understand whether high-value customers were more or less likely to churn than low-value ones.

6. Market Basket Analysis (Python)
The Apriori algorithm was applied to find product combinations that customers frequently buy together. A minimum support threshold of 0.02 was used to keep computation manageable on this dataset. The resulting association rules highlight cross-sell opportunities that could be acted on through product recommendations or bundling strategies.

# Key Findings
- 357 Champions generate £4.47M, over half of total revenue. This group represents only 8% of the customer base but drives the majority of income. Losing even a small number of Champions would have a disproportionate impact on revenue, making retention of this segment the single highest priority.
- 1,299 Lost customers contribute only £818K despite being the largest segment by volume. This highlights a classic Pareto pattern where a small number of high-value customers outperform a much larger group of disengaged ones. Re-engagement campaigns targeting Lost customers with high historical spend could recover significant revenue.
- Retention drops from 100% to around 20-25% within the first month across all cohorts. This is the most critical point in the customer lifecycle. Improving early retention through onboarding, follow-up emails or first-purchase incentives would have a compounding effect on long-term revenue across every cohort.
- Low Value customers have the highest churn rate at around 40%, while VIP customers churn the least. This suggests that higher-spending customers have stronger reasons to return, whether through product satisfaction, loyalty or habit. It also means that acquisition strategies targeting low-value customers are costly relative to the revenue they generate.
- Customer 16029 represents £81K in revenue and is currently At Risk. A single at-risk customer at this value level represents a meaningful retention opportunity. The High Value Customers At Risk table in the dashboard allows the business to prioritize outreach to specific individuals before they churn.

# Data Source
Online Retail II dataset, UCI Machine Learning Repository via Kaggle
https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci
