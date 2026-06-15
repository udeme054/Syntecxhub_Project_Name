# Customer Segmentation Using RFM Analysis (Project 1 - Week 2)

##  Project Overview
This project focuses on data-driven customer segmentation utilizing the RFM (Recency, Frequency, Monetary) Analysis 
framework built in Power BI. By analyzing customer purchasing behavior, this interactive dashboard categorizes an e-commerce customer base 
of 18,484 unique customers into distinct behavioral segments. 

The primary objective is to empower marketing teams to replace generic campaigns with targeted, high-impact strategies, optimize resource 
allocation, and maximize Customer Lifetime Value (CLV).

## Key Performance Indicators (KPIs) & Dashboard Structure

The analytics solution is divided into interactive dashboard pages, referencing specific design files:
Total Sales Performance: $29.36M across the entire ecosystem.
Customer Profiles: Tracks primary demographic attributes including:
Gender Distribution: Balanced engagement with 50.46% Male and 49.54% Female shoppers.
Marital Status: 51.73% Single vs. 48.27% Married.
Age Cohorts: Highlights a massive revenue peak of $11.5M concentrated in the 55–64 age band, followed by $8.1M in the 65–74 group.
Geographic Sales Map: A visual map breakdown of sales distribution by country.
Customer Segmentation Matrix: Segments the customer volume against actual monetary contribution, profiling behavioral metrics across Recency, Frequency, and Monetary scores.
Granular Customer Details: An operational data sheet mapping individual customer IDs, names, email addresses, cities, and sales histories to their precise RFM segment for direct marketing exports.
Marketing Action Index: A strategic dictionary defining each customer segment and prescribing automated business interventions.

##  Core Business Insights

The "Promising" Revenue Driver: The "New Customers" and "Promising" cohorts hold the highest volume of unique buyers (~2.6K and ~2.5K respectively). Crucially, the "Promising" segment contributes the single highest revenue block at $6.5M, proving they are ripe for upselling.
Vulnerable Revenue At Risk: High-value customers categorized under "Cannot Lose Them" and "At Risk" represent a combined $11.2M in historical sales. These segments have high monetary scores but are experiencing severe recency drop-offs, signaling a critical risk of imminent churn.
Demographic Super-Group: Mature adults aged *55 to 74 generate nearly $20M* of the company’s total $29.36M sales revenue, identifying them as the business's most vital customer persona.

##  Core DAX Measures & Formulas Used

To build the dynamic segmentation and calculate the RFM scores, the following key DAX formulas and measures were implemented in the data model:

### 1. Base Performance Measures
These drive the high-level KPIs on the executive summary page.
  Total Sales:
  Total Sales = SUM('Sales_Data'[SalesAmount])
    
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
    
---
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
