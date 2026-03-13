# E-commerce Database-Exploratory Data Analysis (EDA)

### Project Overview
The goal of this project is to perform a comprehensive profiling of an e-commerce database. By applying fundamental SQL aggregations and filtering techniques, I identified the geographical distribution of customers, product hierarchies, sales boundaries, and top-performing business segments.

### Data Source

sales data 

### Tools Used 

Database: PostgreSQL
Core Concepts: Data Profiling, Aggregations, Table Joins, Metadata Queries.

### Methodology

- Database Exploration: Understanding the schema, tables, and columns.
- Dimension Exploration: Identifying unique values in categorical data.
- Date Exploration: Defining the time span of the business.
- Measure Exploration: Calculating high-level key metrics (Total Sales, Order Volume).
- Magnitude & Ranking: Comparing metrics across categories to identify top performers.


## 1. Database & Dimension Profiling

I started by querying the system's metadata to understand the environment and then identified the unique categories within the dimensions.

-- Explore all unique product categories and their sub-hierarchies
SELECT DISTINCT 
    category, 
    subcategory, 
    product_name 
FROM dim_products
ORDER BY category, subcategory;

## 2. Date Boundaries (Time Span)

Establishing the timeframe is essential for context. I calculated the total range of the data in years and months.
SQL Technique: MIN(), MAX(), AGE(), EXTRACT.

SQL


-- Find the business timeframe and the age range of customers
SELECT 
    MIN(order_date) AS first_order, 
    MAX(order_date) AS last_order,
    EXTRACT(YEAR FROM AGE(MAX(order_date), MIN(order_date))) AS years_of_data
FROM fact_sales;


## 3. Key Business Metrics (Measures)

I generated a "Metric Summary Report" by consolidating several high-level aggregations into a single query to provide an instant snapshot of business health.
SQL Technique: SUM(), COUNT(DISTINCT), AVG(), UNION ALL.

SQL


-- High-level snapshot of business metrics
SELECT 'Total Sales' AS measure_name, SUM(sales_amount) AS measure_value FROM fact_sales
UNION ALL
SELECT 'Total Orders', COUNT(DISTINCT order_number) FROM fact_sales
UNION ALL
SELECT 'Total Customers', COUNT(DISTINCT customer_key) FROM dim_customers;


## 4. Magnitude Analysis

This phase involves breaking down a single measure by a dimension to see the distribution of values (e.g., Sales by Category).

SQL Technique: GROUP BY, JOIN.

SQL


-- Analyze Total Revenue by Product Category
SELECT 
    p.category, 
    SUM(f.sales_amount) AS total_revenue
FROM fact_sales f
LEFT JOIN dim_products p ON f.product_key = p.product_key
GROUP BY p.category
ORDER BY total_revenue DESC;


## 5. Ranking & Performance

Finally, I identified the "Top Performers" to help stakeholders focus on the most profitable segments of the business.
SQL Technique: LIMIT, ORDER BY.

SQL


-- Find the Top 5 products by revenue generated
SELECT 
    p.product_name, 
    SUM(f.sales_amount) AS total_revenue
FROM fact_sales f
JOIN dim_products p ON f.product_key = p.product_key
GROUP BY p.product_name
ORDER BY total_revenue DESC
LIMIT 5;


  
