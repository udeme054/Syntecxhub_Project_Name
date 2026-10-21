# E-Commerce Sales Performance Dashboard (Power BI)

![E-Commerce Sales Dashboard](dashboard.jpg)

## Table of Contents
1. [Project Title](#e-commerce-sales-performance-dashboard-power-bi)
2. [Project Overview](#project-overview)
3. [Business Objectives](#business-objectives)
4. [Business Questions](#business-questions)
5. [Dataset Description](#dataset-description)
6. [DAX Measures Used](#dax-measures-used)
7. [Tools Used](#tools-used)
8. [Data Cleaning Process](#data-cleaning-process)
9. [KPIs](#kpis)
10. [Visualizations Created](#visualizations-created)
11. [Key Findings](#key-findings)
12. [Business Insights](#business-insights)
13. [Recommendations](#recommendations)
14. [Skills Demonstrated](#skills-demonstrated)
15. [Conclusion](#conclusion)
16. [Author](#author)

---

## Project Overview
This project analyzes three years (2022 to 2024) of e-commerce sales data for a tech products retailer. I prepared the data in Power BI, created DAX measures, and built an interactive dashboard that shows sales, profit and quantity trends by category, product, region, month, quarter and year.

## Business Objectives
- Track overall sales, profit and units sold.
- Identify the best-performing category and products.
- Understand monthly and quarterly sales patterns, including peak and low periods.
- Compare performance across years and regions.
- Provide data-driven recommendations to grow sales and profit.

## Business Questions
1. Which product category generates the most sales and profit?
2. Which products are the top sellers?
3. Which months record the highest and lowest sales?
4. How did sales and profit change across quarters and years?
5. Which region performs best, and how profitable is the business overall?

## Dataset Description
Source: `ecommerce_sales_data.csv`, containing **3,500 orders and 7 columns**, from January 1, 2022 to December 31, 2024.

| Column | Description |
|---|---|
| Order Date | Date of the order |
| Product Name | One of 10 products (Camera, Monitor, Printer, Mouse, Smartphone, Smartwatch, Keyboard, Tablet, Headphones, Laptop) |
| Category | Electronics, Accessories or Office |
| Region | East, North, South or West |
| Quantity | Units sold per order (1 to 9) |
| Sales | Sales value of the order |
| Profit | Profit earned on the order |

## DAX Measures Used
Measures are stored in a dedicated `_Measures` table. They include:

```DAX
Total Sales    = SUM('E-commerce sales data'[Sales])
Total Profit   = SUM('E-commerce sales data'[Profit])
Total Revenue = Sum('E-commerce sales data'[Revenue])
Total Quantity = SUM('E-commerce sales data'[Quantity])
Gross Profit Margin = Divide([Total Profit], [Total Revenue], 0)
Previous year sales = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('E-commerce sales data'[Order Date].[Date]))
Yearly Growth rate % = Divide([Total Sales]-[Previous year sales],[Previous year sales], 0) * 100
```

Time analysis (year, quarter, month) uses the date hierarchy built from `Order Date`.

## Tools Used
- **Power BI Desktop**: data modeling, DAX and dashboard design
- **Power Query**: data preparation
- **Excel / CSV**: source data
- **GitHub**: documentation and version control

## Data Cleaning Process

| Check | Result | Action |
|---|---|---|
| Missing values | None in any column | None needed |
| Duplicate rows | None found | None needed |
| Order Date | All 3,500 dates valid (`YYYY-MM-DD`) | Set to Date type; built Year, Quarter and Month hierarchy |
| Numeric fields | Sales, Profit and Quantity all positive | Set correct number types |
| Text fields | Category, Region and Product values consistent | None needed |
| Model organization | Measures separated from data | Created a dedicated `_Measures` table |

## KPIs

| Total Sales | Total Profit | Total Quantity | Profit Margin |
|:---:|:---:|:---:|:---:|
| **$10.7M** | **$1.8M** | **17K units** | **17.3%** |

Year-over-year sales growth: **+16.3%** in 2023 and **-4.3%** in 2024.

## Visualizations Created
- **KPI cards**: Total Sales, Total Profit and Total Quantity
- **Column chart**: Total Sales by Quarter
- **Column chart**: Total Sales by Category
- **Column chart**: Total Sales by Month
- **Line chart**: Total Profit by Month
- **Bar chart**: Top 5 Products by Total Sales
- **Donut chart**: Total Profit by Year
- **Slicers**: Region, Year and Category
- **Key Insights panel**: Text summary of main takeaways

## Key Findings
Answers to the business questions:

1. **Top category:** **Electronics** leads with **$5.3M** in sales (about 50% of total) and $923K in profit, followed by Accessories ($4.2M) and Office ($1.1M).
2. **Top products:** **Camera ($1.18M)** and **Monitor ($1.16M)** lead, followed by Printer ($1.09M), Mouse ($1.07M) and Smartphone ($1.07M).
3. **Peak and low months:** **May is the best month** for sales at **$1.03M**, and **February is the lowest** at **$0.70M**. For profit, January ($177K), December ($174K) and May ($173K) are strongest, and February is lowest ($119K).
4. **Quarters and years:** Quarterly sales are steady at $2.6M to $2.7M, with Q4 highest. Yearly sales were $3.26M (2022), **$3.79M (2023, the best year)** and $3.63M (2024). Profit by year was $573K, $667K and $605K.
5. **Best region and profitability:** **West** is the top region at $2.84M (about 27% of sales) and $495K profit, while North is lowest at $2.49M. Overall profit margin is **17.3%**.

## Business Insights
- Electronics and Accessories together bring in about 90% of sales, so the business depends heavily on tech products.
- Product sales are evenly spread. The top five products are within $110K of each other, so no single product dominates.
- February is weak in both sales and orders (237 orders against about 290 on average), partly because it is a shorter month.
- Profit margin is stable at about 17% across categories and regions, so profit grows mainly through sales volume.
- 2024 sales fell about 4% from 2023, so the business has not sustained its 2023 growth.
- Regional performance is fairly balanced, with only about 7 percentage points between West and North.

## Recommendations
1. **Prioritize Electronics** in stock and marketing, and focus promotions on Camera and Monitor.
2. **Expand Office products.** The category has only one product (Printer), so adding more items could grow its share.
3. **Plan a February campaign** (discounts, bundles or loyalty offers) to lift the weakest month.
4. **Repeat what worked in May**, such as promotions or events, in other months.
5. **Investigate the 2024 decline** and set growth targets to regain 2023 levels.
6. **Improve margins** through pricing, supplier negotiation and product mix, since margin is flat at about 17%.
7. **Strengthen North region** performance with targeted marketing.

## Skills Demonstrated
- Data cleaning and validation
- Data modeling and date hierarchies
- DAX measures
- KPI design and interactive dashboards
- Data visualization and storytelling
- Business insight generation and recommendations
- Documentation (GitHub README)

## Conclusion
Over three years the business generated **$10.7M in sales and $1.8M in profit** across 17K units. Electronics is the leading category, Camera and Monitor are the top products, May is the strongest month and February the weakest. With stable margins and balanced regions, the main opportunity lies in reversing the 2024 dip, lifting February and expanding the product range.

## Author
**Udeme Jackson**
Data Analyst (Entry Level)
[LinkedIn](#) | [GitHub](#) | [Email](#)


![Image alt](https://github.com/udeme054/Syntecxhub_Project_Name/blob/e6b886c9abf8ce010d30db58fddf5f5da64deced/E-Commerce%20sales%20performance%20dashboard%20for%20week%201%20project%201%20at%20Syntecxhub.jpg)



