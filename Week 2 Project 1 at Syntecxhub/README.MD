# Customer Segmentation Using RFM Analysis (Project 1 - Week 2)
# Table of Contents
* [Project Overview]
* [Business Objectives]
* [Business Problems]
* [Business Questions]
* [Dataset Description]
* [Tools & Technologies]
* [Data Cleaning & Preparation]
* [Data Modeling]
* [DAX Measures Used]
* [Key Performance Indicators]
* [Visualization Created]
* [Dashboard Overview]
* [Key findings]
* [Business Insights]
* [Strategic Recommendation]
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
1.  CORE KPI MEASURES
* Total Sales = SUM(FactInternetSales[SalesAmount])

* Nos of Customers = DISTINCTCOUNT('Customer_Data'[CustomerKey])

2. RFM MEASURES
* Frequency value = DISTINCTCOUNT('FactInternetSales'[SalesOrderLineNumber])

* Monetary value = 
Calculate(
SUM(FactInternetSales[SalesAmount]),
ALLEXCEPT('FactInternetSales','FactInternetSales'[CustomerKey]
))

* Recency Value = DATEDIFF([Last_transaction date],TODAY(),DAY)

3. RFM Scores
* Recency Scores = 
Switch(
    True(),
    [Recency Value] <= PERCENTILE.INC('RFM Table'[Recency Value], 0.20), 5,
    [Recency Value] <= PERCENTILE.INC('RFM Table'[Recency Value], 0.40), 4,
    [Recency Value] <= PERCENTILE.INC('RFM Table'[Recency Value], 0.60), 3,
    [Recency Value] <= PERCENTILE.INC('RFM Table'[Recency Value], 0.80), 2,  1
)

* Frequency Scores = 
Switch(
    True(),
    [Frequency value] <= PERCENTILE.INC('RFM Table'[Frequency value], 0.20), 1,
    [Frequency value] <= PERCENTILE.INC('RFM Table'[Frequency value], 0.40), 2,
    [Frequency value] <= PERCENTILE.INC('RFM Table'[Frequency value], 0.60), 3,
    [Frequency value] <= PERCENTILE.INC('RFM Table'[Frequency value], 0.80), 4,  5)

* Monetary Scores = 
Switch(
    True(),
    [Monetary value] <= PERCENTILE.INC('RFM Table'[Monetary value], 0.20), 1,
    [Monetary value] <= PERCENTILE.INC('RFM Table'[Monetary value], 0.40), 2,
    [Monetary value] <= PERCENTILE.INC('RFM Table'[Monetary value], 0.60), 3,
    [Monetary value] <= PERCENTILE.INC('RFM Table'[Monetary value], 0.80), 4,  5)

* RFM Scores = 'RFM Table'[Recency Scores] & 'RFM Table'[Frequency Scores] & 'RFM Table'[Monetary Scores]
4. RFM Table
* RFM Table = SUMMARIZE('FactInternetSales','FactInternetSales'[CustomerKey],"Recency Value",[Recency Value],"Frequency value",[Frequency value],"Monetary value",[Monetary value])

* Last_transaction date = 
Maxx(FILTER(FactInternetSales, FactInternetSales[CustomerKey] = FactInternetSales[CustomerKey]),FactInternetSales[OrderDate])

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

Champions, Loyal, Cannot Lose Them, At Risk, About To Sleep, Hibernating Customers, Lost Customers, Need Attention, New Customers, Potential Loyalist, and Promising.

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

* Key Finding
The page connects segment-level analysis to individual customers.

* Business Insight:
Stakeholders can identify exactly which customers require retention, loyalty, re-engagement, or development actions.

## RFM Analysis & Marketing Actions

RFM analysis evaluates customers using:

* Recency (R): How recently they purchased.
* Frequency (F): How often they purchased.
* Monetary (M): How much they spent.

The dashboard links each segment to an appropriate marketing direction.

#Customer Group	                         Marketing Direction
Champions	                            Reward and retain
Loyal	                                Strengthen loyalty
Cannot Lose Them	                    Prioritize retention
At Risk	                                Re-engage and retain
Potential Loyalist	                    Encourage repeat purchases
New Customers	                        Nurture and onboard
Hibernating / Lost	                    Reactivate or win back

## Key Findings
## Business Question	               ## Finding & Insight
* Who are our customers?	  Customers differ across age, gender, marital status, location, sales contribution, and purchasing behavior.
* Which customers are most valuable?	RFM segmentation identifies high-value groups such as Champions and Cannot Lose Them.
* Which customers require attention?	At Risk, About To Sleep, Hibernating, and Lost Customers indicate declining engagement and retention opportunities.
* Who has growth potential?	New Customers, Promising, and Potential Loyalists provide opportunities for developing stronger long-term relationships.
* What should marketing do?	Different segments require different actions, ranging from loyalty rewards and retention to reactivation and win-back campaigns.
* Who should be targeted?	The Customer Details page identifies the individual customers behind each segment, enabling more precise targeting.

## Business Insights



---

##  Tech Stack & Tools Used
Data Visualization & Modeling: Power BI Desktop
DAX (Data Analysis Expressions): Used to construct calculated columns and measures for RFM scoring, customer counts, and ranking.
Data Source: Structured E-commerce Datasets (Excel/SQL Server)

![alt text](https://github.com/udeme054/Syntecxhub_Project_Name/blob/d81d8959ee3e26a350e3622faef32b5217dc009b/Customer%20Profile%20page%201.jpg)
![alt text](https://github.com/udeme054/Syntecxhub_Project_Name/blob/f87655ae13cea326eed866e2f7c4de2f8294f17b/Customer%20Segmentation%20page%202.jpg)
![alt text](https://github.com/udeme054/Syntecxhub_Project_Name/blob/325a80b1f86ca207dad227365be1a10a88caae5f/Customer%20details%20page%203.jpg)
![alt text](https://github.com/udeme054/Syntecxhub_Project_Name/blob/391ca3e2f32561ef3028d0ac9f0c3138dda6c5ac/RFM%20ANALYSIS%20AND%20MARKETING%20ACTIONS.jpg)
