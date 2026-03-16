# E-commerce Database-Exploratory Data Analysis (EDA)

### Project Overview
The goal of this project is to perform a comprehensive profiling of an e-commerce database. By applying fundamental SQL aggregations and filtering techniques, I identified the geographical distribution of customers, product hierarchies, sales boundaries, and top-performing business segments.

### Data Source

sales data 

### Tools Used 

- Database: PostgreSQL
- Core Concepts: Data Profiling,
- Aggregations, 
- Table Joins, 
- Metadata Queries

### Methodology

- Database Exploration: Understanding the schema, tables, and columns.
- Dimension Exploration: Identifying unique values in categorical data.
- Date Exploration: Defining the time span of the business.
- Measure Exploration: Calculating high-level key metrics (Total Sales, Order Volume).
- Magnitude & Ranking: Comparing metrics across categories to identify top performers.
- Advanced Analytics: Implementing "Change Over Time," "Cumulative," and "Part-to-Whole" analyses.
- Business Intelligence Reporting: Consolidating queries into reusable SQL Views for automated reporting. 


## 1. Database & Dimension Profiling

I started by querying the system's metadata to understand the environment and then identified the unique categories within the dimensions.

## 2. Date Boundaries (Time Span)

Establishing the timeframe is essential for context. I calculated the total range of the data in years and months.

MIN(), MAX(), AGE(), EXTRACT.

## 3. Key Business Metrics (Measures)

I generated a "Metric Summary Report" by consolidating several high-level aggregations into a single query to provide an instant snapshot of business health.

SUM(), COUNT(DISTINCT), AVG(), UNION ALL.

## 4. Magnitude Analysis

This phase involves breaking down a single measure by a dimension to see the distribution of values (e.g., Sales by Category).

GROUP BY, JOIN.

## 5. Ranking & Performance

Finally, I identified the "Top Performers" to help stakeholders focus on the most profitable segments of the business.

LIMIT, ORDER BY.

## 6. Growth & Trend Analysis 

Change Over Time 

To understand seasonality, I analyzed total sales and customer acquisition trends at the yearly level. 

EXTRACT(YEAR FROM ...), SUM(), GROUP BY. 

## 7. Performance & Contribution 

Year-Over-Year (YoY) Performance 

I compared current year sales against the previous year's performance to identify growth rates. 

LAG(), PARTITION BY, EXTRACT.

Part-to-Whole Analysis 

Determined which product categories contribute most to the overall revenue. 

Window Functions, Type Casting (::NUMERIC). 

## 8. 3. Customer Segmentation (RFM Lite) 

I segmented the customer base based on their spending behavior and loyalty lifespan. 

Segments: 

VIP: Active ≥ 12 months AND > $5,000 spend. 

Regular: Active ≥ 12 months AND ≤ $5,000 spend. 

New: Active < 12 months. 

CASE WHEN, AGE() or EXTRACT(MONTH FROM ...) for interval calculation. 

## 9. Final Business Reports (SQL Views) 

Consolidated the logic into a final PostgreSQL View. 

Report: Customer Intelligence 360 

This view provides a consolidated profile for every customer. 

CREATE VIEW, CURRENT DATE



  
