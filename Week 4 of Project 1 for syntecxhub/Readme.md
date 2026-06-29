# Bank Loan Dashboard Report

# Project Overview

The Bank Loan Analysis Dashboard is an end-to-end Power BI Business Intelligence project designed to monitor, analyze, and evaluate the performance of a bank's loan portfolio. The dashboard transforms raw loan data into actionable insights that help management assess loan quality, customer behavior, lending performance, and repayment trends.

This project consists of three interactive dashboard pages:
1. Summary Dashboard – Overall loan performance and loan quality.
2. Overview Dashboard – Customer demographics and lending patterns.
3. Details Dashboard – Transaction-level loan records for detailed analysis.

📖 Table of Contents
1. Project Objective
2. Business Problem
3. Dataset Description
4. Tools & Technologies
5. Data Cleaning & Preparation
6. Data Modeling
7. DAX Measures (KPIs)
8. Dashboard Pages
9. Key Insights
10. Business Recommendations
11. How to Use the Dashboard
12. Repository Structure
13. Future Improvements
Author

# Project Objective

The objective of this project is to develop an interactive Power BI dashboard that enables stakeholders to:
1. Monitor loan application performance.
2. Track funded and recovered loan amounts.
3. Evaluate loan quality (Good vs Bad loans).
4. Identify customer borrowing patterns.
5. Monitor loan repayment status.
6. Support data-driven lending decisions.

# Business Problem

Banks process thousands of loan applications every year. Without proper reporting, it becomes difficult to answer important business questions such as:
1. How many loans have been issued?
2. What percentage of loans are performing well?
3. Which loan purposes generate the highest applications?
4. Which states issue the most loans?
5. What is the repayment performance?
6. What customer groups are most likely to apply for loans?

This dashboard addresses these challenges by providing a centralized reporting solution.

# Dataset Description

The dataset contains historical bank loan records including:
1. Loan ID
2. Loan Status
3. Loan Purpose
4. Home Ownership
5. Grade
6. Sub-grade
7. Employment Length
8. Loan Term
9. State
10. Funded Amount
11. Amount Received
12. Interest Rate
13. Debt-to-Income (DTI)
14. Installment
15. Issue Date

# Tools & Technologies
1. Microsoft Excel (Data Source)
2. Power Query (Data Cleaning & Transformation)
3. Power BI Desktop
4. DAX (Data Analysis Expressions)
5. Data Modeling
6. Interactive Visualizations

# Step 1 – Data Cleaning & Preparation

The dataset was prepared using Power Query before visualization.
1. Data cleaning steps
2  Removed duplicate records.
3. Corrected inconsistent data types.
4. Converted dates into proper Date format.
5. Handled missing values.
6. Renamed columns for readability.
7. Standardized categorical values.
8. Removed unnecessary fields.
9. Created Month and Year columns.
9. Verified numerical columns.
10 Loaded the cleaned data into Power BI.
   
# Step 2 – Data Modeling

After cleaning:
1. Created relationships between tables (where applicable).
2. Optimized the data model.
3. Built reusable DAX measures.
4. Applied appropriate formatting for currencies and percentages.
   
# Step 3 – KPIs Created

The dashboard includes the following Key Performance Indicators:

1. Total Loan Applications
2. Total Funded Amount
3. Total Amount Received
4. Average Interest Rate
5. Average Debt-to-Income Ratio (DTI)
6. Good Loan Percentage
7. Bad Loan Percentage
8. Good Loan Applications
9. Bad Loan Applications
10. Good Loan Funded Amount
11. Bad Loan Funded Amount
12. Loan Recovery Amount
13. Loan Status Analysis

# Dashboard Walkthrough
# Summary Dashboard

This page provides a high-level overview of the bank's lending performance.

# KPI Cards
1. Total Loan Applications
2. Total Funded Amount
3. Total Amount Received
4. Average Interest Rate
5. Average DTI

# Visualizations
1. Good Loan vs Bad Loan Donut Charts
2. Loan Status Performance Table
3. Loan Status KPIs
   
# Key Findings
1. 38.6K total loan applications.
2. $435.8M total funded amount.
3. $473M recovered from borrowers.
4. 86.2% of loans are Good Loans.
5. Only 13.8% are Bad Loans.
6. Fully Paid loans generate the highest repayments.
   
# Overview Dashboard

This page explores customer and loan characteristics.

# Visualizations
1. Loan Applications by State
2. Loan Applications by Loan Term
3. Loan Applications by Employment Length
4. Loan Applications by Loan Purpose
5. Loan Applications by Home Ownership
   
# Filters
1. Measure Selector
2. Good vs Bad Loan
3. Grade
4. State

# Key Findings
1. Most applications come from Rent and Mortgage homeowners.
2. Debt Consolidation is the leading loan purpose.
3. 36-month loans dominate the portfolio.
4. Customers with over 10 years of employment submit the most applications.
   
# Details Dashboard

This page provides transaction-level loan information.

# Features
1. Complete loan records.
2. Interactive filtering.
3. Drill-down capability.
4. Detailed loan information.

# Columns Included
1. Loan ID
2. Purpose
3. Home Ownership
4. Grade
5. Sub-grade
6. Funded Amount
7. Interest Rate
8. Issue Date
9. Installment
10. Amount Received

This page enables detailed record-level analysis for auditing and investigation.

# Key Business Insights
# Loan Portfolio Performance
1. The bank maintains a strong loan portfolio with 86.2% performing loans.
2. Total repayments exceed the funded amount, indicating positive loan recovery.

# Customer Behavior
1. Debt Consolidation represents the largest borrowing category.
2. Customers with longer employment histories are more likely to receive loans.
3. Renters and mortgage holders account for most applications.

# Lending Trends
36-month loans are significantly more popular than 60-month loans.
Loan demand varies across states, highlighting regional lending opportunities.

# Risk Analysis
Charged-off loans account for the majority of bad loans.
Monitoring high-risk borrower segments can further reduce defaults.

# Business Recommendations
1. Strengthen credit risk assessment for applicants with higher default risk.
2. Expand lending strategies in high-performing states.
3. Promote loan products for underrepresented customer segments.
4. Encourage shorter loan terms where appropriate to reduce risk.
5. Continue monitoring loan purposes with higher default rates.
6. Improve customer retention by offering repayment incentives for responsible borrowers.
   
# How to Use the Dashboard
1. Open the Power BI report.
2. Navigate between Summary, Overview, and Details pages.
3. Use the slicers to filter by:
    (i) Loan Grade
    (ii) Loan Status
    (iii) State
    (iv) Loan Purpose
4. Click on any visual to cross-filter the report.
5. Analyze KPIs and trends to support business decisions.
   
# Repository Structure
Bank-Loan-Dashboard/
│
├── Data/
│   ├── Bank Loan Dataset.xlsx
│
├── Dashboard/
│   ├── Bank Loan Dashboard.pbix
│
├── Images/
│   ├── Summary Dashboard.png
│   ├── Overview Dashboard.png
│   ├── Details Dashboard.png
│
├── README.md
└── LICENSE

# Future Improvements
1. Integrate real-time SQL database connectivity.
2. Add predictive analytics for loan default risk.
3. Build customer segmentation using machine learning.
4. Implement row-level security for different user roles.
5. Publish the dashboard to the Power BI Service with scheduled data refresh.

# Photo gallery
# Summary of Bank Load report
![Alt text](https://github.com/udeme054/Syntecxhub_Project_Name/blob/683ec23eedabe1cbf5c7a3001ba8ca915ec701b2/Week%204%20of%20Project%201%20for%20syntecxhub/Summary%20of%20Bank%20Loan%20report.jpg)

# Overview of Bank Load report
![Alt text](https://github.com/udeme054/Syntecxhub_Project_Name/blob/12c3cf6ed7a7a0dcaf3c4aa4cd07d3ed1cf92ff3/Week%204%20of%20Project%201%20for%20syntecxhub/Overview%20of%20Bank%20loan%20report.jpg)




# Author

# Udeme Jackson

# Role: Data Analyst | Business Intelligence Analyst

# Skills Demonstrated
1. Data Cleaning (Power Query)
2. Data Modeling
3. DAX Calculations
4. Data Visualization
5. Dashboard Design
6. Business Intelligence
7. Financial Analytics
8. Storytelling with Data
9. KPI Development
10. Interactive Reporting
