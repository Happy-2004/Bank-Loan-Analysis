# Bank Loan Analysis

## Overview

The **Bank Loan Analysis** project is a comprehensive data analysis and visualization initiative aimed at uncovering key insights from loan data. The goal is to evaluate lending performance, borrower behavior, and repayment trends using **MS SQL Server** and **Power BI**. This project helps financial institutions make data-driven decisions, identify high-performing segments, and assess credit risk more effectively.



## Features

### Data Analysis with SQL (MS SQL Server)
- Created and populated a relational database using loan datasets.
- Executed SQL queries to extract meaningful insights:
  - Total Loan Applications and MoM/MTD tracking.
  - Total Funded Amount and Amount Received analysis.
  - Average Interest Rate and Debt-to-Income (DTI) Ratio.
  - Classification and performance of Good vs. Bad Loans.

### Power BI Dashboards

#### Dashboard 1: Summary
- KPIs:
  - Total Loan Applications
  - Total Funded Amount
  - Total Amount Received
  - Average Interest Rate
  - Average DTI
- Good Loan vs. Bad Loan metrics
- Loan Status Grid View

#### Dashboard 2: Overview
- Monthly Issue Trends (Line Chart)
- Regional Loan Distribution (Map)
- Loan Term Distribution (Donut Chart)
- Employment Length Analysis (Bar Chart)
- Loan Purpose Breakdown (Bar Chart)
- Home Ownership Impact (Tree Map)

#### Dashboard 3: Detailed View
- Full drilldown of borrower and loan details
- Holistic snapshot of the lending portfolio

### Dataset Processing
- Cleaned and transformed raw loan data using SQL and Power Query
- Aggregated key metrics to enable rich visualizations and insights



## Technologies Used
- **SQL Server (MS SQL 19.0)**: Data modeling, querying, aggregation
- **Power BI (June 2023)**: Dashboards, KPIs, and visualization
- **Excel/MS Office 2021**: Initial data review and formatting
- **SQL Server Management Studio (SSMS 19.0.20209.0)**: Database management and query execution



## Dataset Description
- **Loan Details**: Application date, funded amount, amount received, loan purpose, loan term
- **Borrower Info**: Employment length, home ownership, debt-to-income ratio
- **Performance Metrics**: Interest rates, repayment records, loan classification



## SQL Queries & Insights
- **Total Loan Metrics**: Overall and monthly loan volumes
- **Repayment Analysis**: Funded vs. received comparisons
- **Risk Assessment**: Good vs. Bad loan segmentation
- **Behavioral Trends**: Employment, loan purpose, and ownership correlations



## Business Insights
- **Monthly Trends**: High loan activity in specific months indicating seasonal patterns
- **Borrower Segmentation**: Employment length and ownership status impact funding
- **Revenue Tracking**: Alignment between funded and received amounts helps track efficiency
- **Loan Risk**: Bad loan segments identified through performance metrics



## Conclusion
This project demonstrates the application of end-to-end data analysis — from SQL querying to visual storytelling with Power BI — to extract insights that can drive smarter loan management strategies.
