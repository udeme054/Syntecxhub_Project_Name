# Customer Segmentation Using RFM Analysis (Project 1 - Week 2)
# Table of Contents
* [Project Overview]
* [Business Objectives]
* [Business Problems]
* [Business Questions]
* [Dataset Description]
* [Tools used]
* [Data Cleaning & Preparation]
* [Data Modeling]
* [DAX Measures Used]
* [Key Performance Indicators]
* [Visualization Created]
* [Dashboard Overview]
* [Key findings]
* [Business Insights]
* [Recommendation]
* [Skills Demonstrated]
* [Conclusion]
* [Author]

##  Project Overview
An interactive Power BI Customer Analytics Dashboard designed to analyze customer demographics, purchasing behavior, customer value, RFM segmentation, and marketing opportunities.

The project combines four analytical views:
Customer Demographics → Customer Segmentation → RFM Marketing Actions → Customer Details
The analysis covers 18,484 customers across 6 countries and 11 customer segments, providing a complete view from understanding customers to identifying appropriate business actions..

## Business Objectives
* Understand customer demographic and geographic characteristics.
* Measure customer sales and purchasing behavior.
* Identify valuable, loyal, at-risk, and inactive customers.
* Segment customers using Recency, Frequency, and Monetary (RFM) analysis.
* Define appropriate marketing actions for different customer segments.
* Enable customer-level investigation for targeted decision-making.

## Business Problems
The business needs to understand who its customers are, how they behave, how valuable they are, and which customers require attention.

Without customer segmentation, marketing efforts may be too broad and fail to address the different needs of high-value, loyal, emerging, at-risk, and inactive customers.

## Business Questions
* Who are our customers and where are they located?
* Which customer groups generate the most value?
* Which customers are loyal, at risk, or becoming inactive?
* Which customers represent future growth opportunities?
* What marketing action is appropriate for each segment?
* Who are the individual customers within each segment?

## Dataset Description
The analysis uses customer, transaction, sales, product, demographic, geographic, and RFM data.

Key metrics:
* 18,484 Customers
* 11 Customer Segments
* 6 Countries
* $29.36M Total Sales

* Key fields include Customer Number, Age, Gender, Marital Status, City, Country, Product, Sales, Order Date, and Customer Segment.

## Tools Used
* Power BI desktop 
* Power Query
* DAX (Data Analysis Expressions): Used to construct calculated columns and measures for RFM scoring, customer counts, and ranking.
* Data visualization and Modeling
* GitHub | Linkedln (Project Documentation)
* Data Source: Structured E-commerce Datasets (Excel/SQL Server)

## Data Cleaning and preparation
Data preparation was performed using Power Query, including:

* Removing duplicates and reviewing missing values.
* Correcting data types and standardizing fields.
* Preparing demographic and geographic attributes.
* Creating/validating age bands.
* Preparing transaction data for RFM analysis.
* Validating relationships and analytical fields.

## Data Modelling
A structured Power BI data model was created to connect customer, order, product, and transaction information.
The model enables analysis across:
* Customers
* Orders
* Products
* Sales
* Demographics
* RFM metrics
* Customer segments
Relationships were configured to allow customer-level filtering and drill-down across the dashboard.

## DAX Measures
### 1. Core KPI Measures
```dax
Total Sales = 
SUM(FactInternetSales[SalesAmount])

Nos of Customers = 
DISTINCTCOUNT('Customer_Data'[CustomerKey])
```
### 2. RFM Measures
```dax
Frequency value = 
DISTINCTCOUNT('FactInternetSales'[SalesOrderLineNumber])

Monetary value = 
CALCULATE(
    SUM(FactInternetSales[SalesAmount]),
    ALLEXCEPT('FactInternetSales', 'FactInternetSales'[CustomerKey])
)

Recency Value = 
DATEDIFF([Last_transaction date], TODAY(), DAY)
```
### 3. RFM Scores
```dax
Recency Scores = 
SWITCH(
    TRUE(),
    [Recency Value] <= PERCENTILE.INC('RFM Table'[Recency Value], 0.20), 5,
    [Recency Value] <= PERCENTILE.INC('RFM Table'[Recency Value], 0.40), 4,
    [Recency Value] <= PERCENTILE.INC('RFM Table'[Recency Value], 0.60), 3,
    [Recency Value] <= PERCENTILE.INC('RFM Table'[Recency Value], 0.80), 2,
    1
)

Frequency Scores = 
SWITCH(
    TRUE(),
    [Frequency value] <= PERCENTILE.INC('RFM Table'[Frequency value], 0.20), 1,
    [Frequency value] <= PERCENTILE.INC('RFM Table'[Frequency value], 0.40), 2,
    [Frequency value] <= PERCENTILE.INC('RFM Table'[Frequency value], 0.60), 3,
    [Frequency value] <= PERCENTILE.INC('RFM Table'[Frequency value], 0.80), 4,
    5
)

Monetary Scores = 
SWITCH(
    TRUE(),
    [Monetary value] <= PERCENTILE.INC('RFM Table'[Monetary value], 0.20), 1,
    [Monetary value] <= PERCENTILE.INC('RFM Table'[Monetary value], 0.40), 2,
    [Monetary value] <= PERCENTILE.INC('RFM Table'[Monetary value], 0.60), 3,
    [Monetary value] <= PERCENTILE.INC('RFM Table'[Monetary value], 0.80), 4,
    5
)

RFM Scores = 
'RFM Table'[Recency Scores] & 'RFM Table'[Frequency Scores] & 'RFM Table'[Monetary Scores]
```

### 4. RFM Table & Calculated Columns
```dax
RFM Table = 
SUMMARIZE(
    'FactInternetSales',
    'FactInternetSales'[CustomerKey],
    "Recency Value", [Recency Value],
    "Frequency value", [Frequency value],
    "Monetary value", [Monetary value]
)

Last_transaction date = 
MAXX(
    FILTER(FactInternetSales, FactInternetSales[CustomerKey] = FactInternetSales[CustomerKey]),
    FactInternetSales[OrderDate]
)
```

## Key Performance Indicators (KPIs)
* Total Customers:	18,484
* Total Sales:	    $29.36M

## Visualization Created

The dashboard includes:
* KPI Cards
* Bar & Column Charts
* Donut Charts
* Geographic Map
* RFM Segment Analysis
* Customer Detail Table
* Slicers & Filters
* Interactive Drill-downs

## Dashboard Overview

👥 Customer Demographics: Analyzes customers by age, age band, gender, marital status, country, city, and sales.

* Key Finding
The dashboard provides a clear profile of the customer base and shows how sales vary across demographic and geographic groups.

* Business Insight:
Customer characteristics and location provide useful context for targeted marketing and customer engagement rather than applying a single strategy to the entire customer base.


🎯 Customer Segmentation

Customers are classified into 11 RFM-based segments, including: 
* Champions, Loyal
* Cannot Lose Them
* At Risk
* About To Sleep
* Hibernating Customers
* Lost Customers
* Need Attention
* New Customers
* Potential Loyalist
* Promising.

* Key Finding

Customers demonstrate different levels of engagement, purchasing frequency, and monetary value.

* Business Insight:
The customer base should be managed using segment-specific strategies rather than a one-size-fits-all approach.

👤 Customer Details

The Customer Details page provides customer-level information including:

* Customer Number
* Name & Email
* Age
* Gender
* Marital Status
* City & Country
* Total Sales
* Customer Segment

* Key Finding: The page connects segment-level analysis to individual customers.

* Business Insight:Stakeholders can identify exactly which customers require retention, loyalty, re-engagement, or development actions.

## RFM Analysis & Marketing Actions

RFM analysis evaluates customers using:

* Recency (R): How recently they purchased.
* Frequency (F): How often they purchased.
* Monetary (M): How much they spent.

The dashboard links each segment to an appropriate marketing direction.

### Customer Groups & Marketing Direction

| Customer Group         | Marketing Direction        |
| ---------------------- | -------------------------- |
| **Champions**          | Reward and retain          |
| **Loyal**              | Strengthen loyalty         |
| **Cannot Lose Them**   | Prioritize retention       |
| **At Risk**            | Re-engage and retain       |
| **Potential Loyalist** | Encourage repeat purchases |
| **New Customers**      | Nurture and onboard        |
| **Hibernating / Lost** | Reactivate or win back     |


## Key Findings
* Customers differ across age, gender, marital status, location, sales contribution, and purchasing behavior.
* RFM segmentation identifies high-value groups such as Champions and Cannot Lose Them has the most valuable customers
* At Risk, About To Sleep, Hibernating, and Lost Customers indicate declining engagement and retention opportunities.
* New Customers, Promising, and Potential Loyalists provide opportunities for developing stronger long-term relationships.
* Different segments require different actions, ranging from loyalty rewards and retention to reactivation and win-back campaigns.
* The Customer Details page identifies the individual customers behind each segment, enabling more precise targeting.

## Business Insights 

1. **High-value customers drive significant revenue:** Champions generate approximately $8.3M in revenue, highlighting their importance to business performance.

2. **At-Risk customers represent substantial revenue exposure:** The At-Risk segment has approximately $7.3M in historical spend, making customer retention an important opportunity.

3. **Customers are at different stages of loyalty:** The 11 RFM segments reveal distinct customer behaviors, ranging from New Customers and Promising customers to Champions, At Risk, Hibernating, and Lost Customers.

4. **Emerging customers provide growth opportunities:** New Customers, Promising, and Potential Loyalists have potential to develop into higher-value and more loyal customer segments.

5. **Inactive customers require differentiated attention:** About To Sleep, Hibernating, and Lost Customers show different levels of disengagement and therefore require different reactivation approaches.

6. **Demographics provide additional customer context:** Age, gender, marital status, country, city, and individual customer information can be combined with RFM segmentation to better understand customer behavior.

## Business Recommendations

1. **Retain high-value customers:** Implement loyalty rewards, exclusive benefits, personalized offers, and proactive engagement for Champions and other high-value customers.

2. **Prioritize At-Risk customers:** Deploy targeted retention and re-engagement campaigns using personalized offers, reminders, product recommendations, and loyalty incentives.

3. **Nurture emerging customers:** Use welcome campaigns, repeat-purchase incentives, personalized recommendations, and loyalty programs to move New Customers and Potential Loyalists toward higher-value segments.

4. **Develop differentiated win-back campaigns:** Tailor reactivation strategies to About To Sleep, Hibernating, and Lost Customers based on their previous value and level of inactivity.

5. **Personalize customer engagement:** Use the Customer Details dashboard to identify individual customers for targeted retention, upselling, cross-selling, and reactivation activities.

6. **Combine demographics with RFM analysis:** Use customer demographics together with Recency, Frequency, and Monetary scores to improve campaign targeting and marketing resource allocation.

# Skills Demonstrated
* Power BI: Dashboard Development, Data Visualization, KPI Design, Slicers, Drill-downs
* Power Query: Data Cleaning, Transformation, Data Preparation
* DAX: Measures, Aggregations, RFM Calculations, KPI Development
* Analytics: Customer Analytics, RFM Analysis, Customer Segmentation, Demographic Analysis, Sales Analysis
* Business Intelligence: Data Storytelling, Business Problem Solving, Insight Generation, Customer Retention Strategy

👨‍💻 Author

Udeme Jackson
Chemical Engineer | Entry-Level Data Analyst

Technical Skills: Excel | SQL | Power BI | Power Query | DAX

Passionate about transforming raw data into meaningful insights, interactive dashboards, and actionable business recommendations.


![alt text](https://github.com/udeme054/Syntecxhub_Project_Name/blob/d81d8959ee3e26a350e3622faef32b5217dc009b/Customer%20Profile%20page%201.jpg)
![alt text](https://github.com/udeme054/Syntecxhub_Project_Name/blob/f87655ae13cea326eed866e2f7c4de2f8294f17b/Customer%20Segmentation%20page%202.jpg)
![alt text](https://github.com/udeme054/Syntecxhub_Project_Name/blob/325a80b1f86ca207dad227365be1a10a88caae5f/Customer%20details%20page%203.jpg)
![alt text](https://github.com/udeme054/Syntecxhub_Project_Name/blob/391ca3e2f32561ef3028d0ac9f0c3138dda6c5ac/RFM%20ANALYSIS%20AND%20MARKETING%20ACTIONS.jpg)



