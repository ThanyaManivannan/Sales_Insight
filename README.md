# Sales Insights Data Analysis

### Dashboard Link: [https://app.powerbi.com/reportEmbed?reportId=2828e4d2-5c4e-415f-8e9c-0e8b18411f6d&autoAuth=true&ctid=c99cd995-dded-4bba-99cf-3727b59f7612]

## Problem Statement

Atliq Hardware, a computer hardware business, is facing challenges in a dynamically changing market. To tackle this, the Sales Director has decided to invest in a data analysis project. The goal is to create a Power BI dashboard that provides real-time sales insights, helping in decision-making and improving business strategies.

## Steps Followed

- **Step 1:** Data was extracted from MySQL database which includes sales transactions, customers, products, and market information.
- **Step 2:** Connected the MySQL database to Power BI for further analysis.
- **Step 3:** Performed ETL (Extract, Transform, Load) operations, also known as data wrangling, which included:
  - Currency normalization
  - Handling invalid/missing values
  - Removing duplicates and ensuring data consistency
- **Step 4:** Designed an interactive dashboard in Power BI with key sales metrics and insights.
- **Step 5:** Implemented various visualizations and KPIs, such as total revenue, profit margin, and market trends.
- **Step 6:** Published the dashboard to Power BI Service for real-time access.

## Features of the Dashboard

- **Sales Performance Analysis:** Provides an overview of revenue, profit, and sales trends.
![Image](https://github.com/user-attachments/assets/700a4020-5678-46cc-9e26-1e982c308884)
- **Market Insights:** Analyzes sales by region
![Image](https://github.com/user-attachments/assets/cd4d0a31-6373-4282-bb6a-954e011d9ea7)
- **Market Insights:** Analysis sales by Top 5 customers
![Image](https://github.com/user-attachments/assets/41419d25-0aef-4cf8-8994-5c06b3168806)
- **Market Insights:** Analysis sales by Top 5 products
![Image](https://github.com/user-attachments/assets/0851cd81-daf1-4711-abdf-e6ddcca385b8)
- **Profitability Analysis:** Revenue growth trends by Year and Date
![Image](https://github.com/user-attachments/assets/a5250269-5349-4141-bdcc-6336daa41809)

## Technologies Used

- **Database:** MySQL
- **Data Visualization Tool:** Power BI
- **Data Transformation:** Power Query (ETL)
- **Scripting:** SQL for data extraction and transformation

## Data Analysis Using SQL

### Show all customer records
```sql
SELECT * FROM customers;
```
### Show total number of customers
```sql
SELECT count(*) FROM customers;
```
### Show transactions for Chennai market (market code for Chennai is Mark001)
```sql
SELECT * FROM transactions where market_code='Mark001';
```
### Show distinct product codes that were sold in Chennai
```sql
SELECT distinct product_code FROM transactions where market_code='Mark001';
```
### Show transactions where currency is US dollars
```sql
SELECT * from transactions where currency="USD";
```
### Show transactions in 2020 join by date table
```sql
SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;
```
### Show total revenue in year 2020
```sql
SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and (transactions.currency="INR" or transactions.currency="USD");
```
### Show total revenue in year 2020, January Month
```sql
SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and date.month_name="January" and (transactions.currency="INR" or transactions.currency="USD");
```
### Show total revenue in year 2020 in Chennai
```sql
SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.market_code="Mark001";
```

## Data Analysis Using Power BI

### Formula to create norm_amount column
```powerquery
= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)
```

## Repository Structure

```
sales-insights-powerbi/
│-- data/                # Contains raw and cleaned data files
│-- reports/             # Power BI report (.pbix) file
│-- scripts/             # SQL queries used for data extraction and transformation
│-- README.md            # Project documentation
│-- LICENSE              # Open-source license (optional)
```

## Insights from the Dashboard

- **Revenue Trends:** Monthly sales performance with year-over-year comparison.
- **Customer Insights:** Distribution of customers based on purchase behavior.
- **Profit Analysis:** Identification of high-margin and low-margin products.
- **Market Performance:** Best and worst-performing markets based on sales.

## Author
Thanya Manivannan



