# E-commerce Retail Sales Analysis - SQL Project

## Project Overview
This project focuses on analyzing a real-world e-commerce dataset to derive actionable business insights. Using PostgreSQL, I performed data cleaning, exploratory data analysis (EDA), and complex query-based analysis to solve 10 key business challenges, including sales trends, customer behavior, and product performance.

## Objectives
1. **Database Setup**: Importing raw CSV data into a PostgreSQL table.
2. **Data Cleaning**: Handling encoding issues and filtering out invalid/refunded transactions to ensure data accuracy.
3. **Exploratory Data Analysis (EDA)**: Understanding the dataset structure and data distributions.
4. **Business Intelligence**: Answering complex business questions through SQL queries.

## Project Workflow
- **Environment**: PostgreSQL / pgAdmin 4.
- **Data Import**: Addressed character encoding errors (`invalid byte sequence`) by converting the dataset to `LATIN1` encoding.
- **Analysis**: Developed 10+ SQL queries utilizing advanced concepts like:
    - `Window Functions` (`LAG()`) for growth analysis.
    - `Aggregate Functions` (`SUM`, `COUNT`) for performance metrics.
    - `CTE` (Common Table Expressions) for modular query logic.
    - `CASE` statements for data categorization.

## Key Insights & Findings
- **Sales Performance**: Identified key sales trends and high-revenue regions.
- **Customer Segmentation**: Differentiated between one-time and returning customers.
- **Operational Efficiency**: Analyzed peak business hours and average order values (AOV).
- **Product Strategy**: Categorized products into 'Budget', 'Mid-Range', and 'Premium' segments to optimize inventory management.

## SQL Queries Highlights

 1. **Revenue per Country**

      SELECT country,
	         SUM(quantity * unit_price) AS total_revenue
      FROM e_commerce
	  GROUP BY 1
	  ORDER BY 2 DESC;


-- 2. **Top 10 Spending Customers**

	  SELECT customer_id,
	         SUM(quantity*unit_price) AS total_spend
	  FROM e_commerce
	  WHERE customer_id IS NOT NULL
	  GROUP BY 1
	  ORDER BY 2 DESC
	  LIMIT 10;


-- 3. **Monthly Sales Growth**

	  WITH monthly_sales AS(
	  SELECT EXTRACT(MONTH FROM invoice_date) AS month,
	     	 SUM(quantity*unit_price) AS total_revenue
 	  FROM e_commerce
	  GROUP BY 1)
	  SELECT month,total_revenue,
	         LAG(total_revenue) OVER(ORDER BY month),
			 total_revenue - LAG(total_revenue) OVER(ORDER BY month) AS difference
	  FROM monthly_sales;


-- 4. **Product Frequency**

	  SELECT stock_code,COUNT(invoice_no) AS total_orders
	  FROM e_commerce
	  GROUP BY 1
	  ORDER BY 2 DESC;)


    
- **Monthly Sales Growth**: Used `LAG()` window function to calculate month-over-month revenue differences.
- **Revenue by Price Range**: Utilized `CASE` statements to segment products and calculate category-wise revenue.
- **Basket Analysis**: Calculated the average items per order to understand shopping habits.

## How to Run
1. Clone this repository.
2. Import the dataset into PostgreSQL using the provided encoding (`LATIN1`).
3. Run the analysis scripts in your SQL editor to reproduce the findings.

## Author - Suraj Dadwal
Data Analyst Portfolio | Passionate about SQL and Data-driven decision making.
