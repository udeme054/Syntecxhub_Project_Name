# HR Analytics: Employee Attrition Dashboard (Power BI)

## Table of Contents
1. [Project Title](#hr-analytics-employee-attrition-dashboard-power-bi)
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
This project analyzes employee attrition (staff turnover) for a company of 1,480 employees. Using Power BI, I built an interactive HR dashboard that shows who is leaving and why, broken down by department, salary, age, job role, job satisfaction, gender and business travel. The goal is to help HR understand the drivers of attrition and reduce it.

## Business Objectives
- Measure overall attrition and describe the workforce profile.
- Identify the departments, roles and employee groups with the highest attrition.
- Understand how pay, age and job satisfaction relate to leaving.
- Provide data-driven recommendations to improve employee retention.

## Business Questions
1. What is the overall attrition rate, and what does the workforce look like?
2. Which department has the highest attrition?
3. How does salary level affect attrition?
4. Which age groups are most likely to leave?
5. Which job roles and satisfaction levels are linked to attrition?
6. Do gender and business travel influence attrition?

## Dataset Description
Source: `HR_Analytics.csv`, containing **1,480 employee records and 38 columns**.

| Group | Key Columns |
|---|---|
| Employee profile | EmpID, Age, AgeGroup, Gender, MaritalStatus, Education, EducationField |
| Job details | Department, JobRole, JobLevel, BusinessTravel, OverTime, DistanceFromHome |
| Pay | MonthlyIncome, SalarySlab, DailyRate, HourlyRate, MonthlyRate, PercentSalaryHike, StockOptionLevel |
| Satisfaction and performance | JobSatisfaction, EnvironmentSatisfaction, RelationshipSatisfaction, WorkLifeBalance, JobInvolvement, PerformanceRating |
| Tenure | YearsAtCompany, YearsInCurrentRole, YearsSinceLastPromotion, YearsWithCurrManager, TotalWorkingYears |
| Target | **Attrition** (Yes / No) |

## DAX Measures Used
The report uses a `_Measures` table. Most cards use simple aggregations of columns, and attrition rate is the main calculated measure. Formulas below are illustrative; adjust the names to match your model.

| Dashboard Metric | DAX |
|---|---|
| Total Employees | `COUNT(HR_Analytics[EmpID])` |
| Attrition Count | `CALCULATE(COUNT(HR_Analytics[EmpID]), HR_Analytics[Attrition] = "Yes")` |
| Active Employees | `CALCULATE(COUNT(HR_Analytics[EmpID]), HR_Analytics[Attrition] = "No")` |
| Attrition Rate | `SUM(HR_Analytics[Attrition count])/SUM(HR_Analytics[EmployeeCount])` |
| Average Age | `AVERAGE(HR_Analytics[Age])` |
| Average Tenure | `AVERAGE(HR_Analytics[YearsAtCompany])` |
| Average Monthly Salary | `AVERAGE(HR_Analytics[MonthlyIncome])` |

## Tools Used
- **Power BI Desktop**: data modeling, DAX and dashboard design
- **Power Query**: data preparation
- **Excel / CSV**: source data
- **GitHub**: documentation and version control

## Data Cleaning Process
The dataset was profiled column by column. Issues found and how they were handled:

| Issue | Rows Affected | Status and Impact |
|---|---|---|
| Duplicate rows | 7 (0.5%) | Flagged. Impact is negligible: attrition rate is 16.08% with them and 16.09% without |
| Missing values in `YearsWithCurrManager` | 57 | Flagged. Column is not used in the dashboard, so no KPIs are affected |
| Inconsistent label in `BusinessTravel` (`TravelRarely` vs `Travel_Rarely`) | 8 | Flagged. Should be merged into `Travel_Rarely` (currently shows as a separate near-empty bar) |
| Constant columns (`Over18`, `StandardHours`, `EmployeeCount`) | All | Contain no analytical value, so they are not used for analysis |
| Data types | All | Set correct types for numbers, text and categories |
| Segmentation | All | Used `AgeGroup` and `SalarySlab` bands to compare groups |

## KPIs

| Total Employees | Active Employees | Attrition Count | Attrition Rate | Avg Age | Avg Tenure | Avg Monthly Salary |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **1,480** | **1,242** | **238** | **16.08%** | **36.92** | **7.01 years** | **$6.50K** |

## Visualizations Created
- **KPI cards**: Active Employees, Average Tenure, Average Monthly Salary, Average Age, Attrition Rate, Attrition Count, Total Employees
- **Donut chart**: Attrition by Department
- **Bar chart**: Attrition by Salary Slab
- **Combo chart**: Attrition Count and Rate by Age Group
- **Matrix**: Attrition by Job Role and Job Satisfaction
- **Donut chart**: Performance by Department
- **Donut chart**: Employees by Education Field
- **Donut chart**: Attrition by Gender
- **Column chart**: Attrition Count by Business Travel
- **Slicers**: Department, Age Group, Education Field, Gender, Marital Status, Business Travel, Salary Slab

## Key Findings
Answers to the business questions:

1. **Overall attrition:** **238 of 1,480 employees (16.08%) have left**, leaving 1,242 active. The average employee is 36.9 years old, has 7 years of tenure and earns about $6.5K a month.
2. **Department:** **Research & Development has the most leavers (133, or 56%)** simply because it is the largest department. **Sales has the highest rate** at 20.7% (93 leavers), against 19.0% for HR and 13.8% for R&D.
3. **Salary:** Attrition falls sharply as pay rises. The **Up to 5K slab has 163 leavers and a 21.6% rate**, against 11.0% (5K to 10K), 14.0% (10K to 15K) and just 3.8% above 15K.
4. **Age:** The **18 to 25 group has the highest rate at 35.8%**. The 26 to 35 group has the most leavers (116, rate 19.0%). The lowest rate is 36 to 45 (9.1%).
5. **Job roles and satisfaction:** **Laboratory Technician (62) and Sales Executive (58)** have the most leavers, and Sales Representative has the highest rate (39.3%). About 28% of leavers (67) reported the lowest job satisfaction, and employees with a satisfaction score of 1 left at 22.9% against 11.3% for those scoring 4.
6. **Gender and travel:** Men make up 63% of leavers (151) against 37% for women (87), a rate of 17.0% against 14.7%. **Frequent travelers leave at 24.7%**, against 15.1% for rare travelers and 7.9% for non-travelers.

## Business Insights
- Attrition is concentrated among **young, lower-paid, early-career employees**. Leavers earn about $4.8K a month on average against $6.8K for those who stayed.
- Sales is the weakest department for retention, and Sales Representative is the most at-risk role.
- Pay matters: the lowest salary band loses employees at about 6 times the rate of the highest band.
- Low job satisfaction is a clear warning sign, with satisfaction-1 employees leaving at twice the rate of satisfaction-4 employees.
- Frequent business travel is linked to attrition, with leavers among frequent travelers at three times the rate of non-travelers.
- Performance ratings are nearly identical across departments (an average of about 3.1), so performance does not explain attrition.
- Gender differences are small, so attrition is not mainly a gender issue.
- **Additional insight (from the dataset):** Employees who work overtime leave at **30.6%** against 10.4% for those who do not, and single employees leave at 25.4%. These are the strongest drivers in the data.

## Recommendations
1. **Review pay for the lowest salary band** (Up to 5K) and for entry-level roles to reduce early exits.
2. **Launch early-career retention programs** (mentoring, career paths, onboarding) for employees aged 18 to 25.
3. **Investigate Sales** and the Sales Representative role through exit interviews, workload review and incentive changes.
4. **Reduce overtime and frequent travel** where possible, or offer compensation and time-off in return.
5. **Run regular job satisfaction surveys** and act quickly on employees who score 1 or 2.
6. **Track attrition monthly** with this dashboard and set a target to bring the rate below 16%.

## Skills Demonstrated
- Data cleaning and quality profiling
- Data modeling and DAX measures
- KPI design and interactive dashboards with slicers
- Data visualization and storytelling
- HR and workforce analytics
- Business insight generation and recommendations
- Documentation (GitHub README)

## Conclusion
The company has a **16.08% attrition rate (238 of 1,480 employees)**. Leavers are mostly young, lower-paid, less satisfied employees, particularly in Sales, and those who travel frequently or work overtime. Improving pay for entry-level staff, supporting early-career employees, and managing workload and travel offer the clearest path to better retention.

## Author
**Udeme Jackson**
Data Analyst
[LinkedIn](#) | [GitHub](#) | [Email](#)

## How to run/view run the project
1.Dashboard: Open the dashboard file in the week 3 project 2 at syntecxhub folder to interact with the visualization

● Linkedlin link:https://www.linkedin.com/posts/udeme-jackson-0a0887144_powerbi-hranalytics-dataanalytics-activity-7473634834574286848-RZja?utm_source=share&utm_medium=member_desktop&rcm=ACoAACMDV7gBXE-tE0ZG2fYv2alSEQVhZV173Wc

# Project gallery
![alt text](https://github.com/udeme054/Syntecxhub_Project_Name/blob/c9da8cde316bcc6c45f887a9293c64799969f433/Week%203%20Project%202%20at%20Syntecxhub/Picture%20of%20HR%20Analytics%20Dashboard%20for%20Week%203%20of%20Project%202.jpg)



