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
* [Dashboard Overview]
* [Visualization Created]
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

## Datasets
The analysis uses customer, transaction, sales, product, demographic, geographic, and RFM data.

Key metrics:
* 18,484 Customers
* 11 Customer Segments
* 6 Countries
* $29.36M Total Sales
Key fields include Customer Number, Age, Gender, Marital Status, City, Country, Product, Sales, Order Date, and Customer Segment.

## Data Cleaning
Data preparation was performed using Power Query, including:

* Removing duplicates and reviewing missing values.
* Correcting data types and standardizing fields.
* Preparing demographic and geographic attributes.
* Creating/validating age bands.
* Preparing transaction data for RFM analysis.
* Validating relationships and analytical fields.

## DAX Measures
Total Sales =
SUM(FactInternetSales[SalesAmount])


    
  Total Customers
  Nos of Customers = DISTINCTCOUNT('Customer_Data'[CustomerKey])
    
 ### 2. RFM Component Calculations
These measures calculate the foundational parameters for each individual customer.

 Recency (Days since last purchase):
  Finds the gap between the maximum overall transaction date in the dataset and each customer's last purchase date.
    Customer Recency
  Customer Frequency = 
    CALCULATE(DISTINCTCOUNT('Sales_Data'[OrderNumber]), ALLEXCEPT('Sales_Data', 'Customer_Data'[CustomerKey]))
    
  Monetary Value (Total spend per customer)
    Customer Monetary Value = 
    CALCULATE([Total Sales], ALLEXCEPT('Sales_Data', 'Customer_Data'[CustomerKey]))
  
  ### 3. RFM Scoring (Using Percentiles / NTILE equivalent)
  Customers are assigned a score from 1 to 5 for each metric using the RANKX function to divide them into quintiles.

    Recency Score:
    Recency Score = 
    VAR CustomerRank = RANKX(ALL('Customer_Data'), [Customer Recency], , ASC, Dense)
    VAR TotalCustomers = COUNTROWS(ALL('Customer_Data'))
    RETURN
    SWITCH(
        TRUE(),
        CustomerRank <= TotalCustomers * 0.2, 5,
        CustomerRank <= TotalCustomers * 0.4, 4,
        CustomerRank <= TotalCustomers * 0.6, 3,
        CustomerRank <= TotalCustomers * 0.8, 2,
        1
    )
    
## Strategic Marketing Recommendations

Based on the behavioral findings in the RFM matrix, the following actions are recommended for the business:

Execute Immediate Churn Win-Back Campaigns: Target the "Cannot Lose Them" and "At Risk" groups with aggressive re-engagement campaigns, exclusive loyalty perks, or personalized feedback surveys to safeguard the $11.2M in vulnerable revenue.
Optimize the Onboarding Funnel: Cultivate the high-volume "Promising" and "New Customer" pools with targeted product recommendations and milestone discounts to seamlessly guide them into becoming lifelong *"Champions"*.
Targeted Ad Spend Allocation: Double down on marketing spend targeted at the 55–74 age bracket, utilizing messaging and channels tailored to their distinct buying preferences.

---

##  Tech Stack & Tools Used
Data Visualization & Modeling: Power BI Desktop
DAX (Data Analysis Expressions): Used to construct calculated columns and measures for RFM scoring, customer counts, and ranking.
Data Source: Structured E-commerce Datasets (Excel/SQL Server)

![alt text](https://github.com/udeme054/Syntecxhub_Project_Name/blob/d81d8959ee3e26a350e3622faef32b5217dc009b/Customer%20Profile%20page%201.jpg)
![alt text](https://github.com/udeme054/Syntecxhub_Project_Name/blob/f87655ae13cea326eed866e2f7c4de2f8294f17b/Customer%20Segmentation%20page%202.jpg)
![alt text](https://github.com/udeme054/Syntecxhub_Project_Name/blob/325a80b1f86ca207dad227365be1a10a88caae5f/Customer%20details%20page%203.jpg)
![alt text](https://github.com/udeme054/Syntecxhub_Project_Name/blob/391ca3e2f32561ef3028d0ac9f0c3138dda6c5ac/RFM%20ANALYSIS%20AND%20MARKETING%20ACTIONS.jpg)
