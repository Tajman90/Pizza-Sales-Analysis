# Pizza-Sales-Analysis
## Project Overview 
We set out to analyse the key indicators for Pizza Sales data to gain insight into the business performance. We calculated the following:: Total Revenue, Average Order Value, Total Pizza Sold, Total Orders and Average Pizza Sold.
## Problem Statement
### Charts Requirement
We would like to visualise various aspects of our pizza sales data to gain insights and understand key trends. We have identified the following requirements for creating charts:
1. **Daily Trend for Total Orders:** Create a bar chart that displays the daily trend of total orders over a specific time period. This chart will help us identify any patterns or fluctuations in order volumes on a daily basis.
2. **Monthly Trend for Total Orders:** Create a line chart that illustrate the hourly trend of total orders throughout the day. This chart will allow us to identify peak hours or periods of high hour activity.
3. **Percentage of Sales by Pizza Category:** Create a pie chart that shows the distribution of sales across different pizza categories. This chart will provide insights into the popularity of various pizza categories and their contribution to overall sales.
4. **Percentage of Sales by Pizza Sales:** Generate a pie chart that represents the percentage of sales attributed to pizza sizes. This chart will help us understand customer preference for pizza size and their impact on sales.
5. **Total Pizza Sold by Category:** Create a funnel chart that present the total number of pizza sold for each pizza category. This chart will allow us to compare the sales performance of different pizza categories.
6. **Top Five Best Sellers by Revenue, Total Quality and Total Orders:** Create a bar chart highlighting the top 5 best-selling pizzas based on Revenue, Total Quality and Total Orders.
The chart will help us identify the most popular pizza options.
7. **Bottom Five Best Sellers by Revenue, Total Quality and Total Orders:** Create a bar chart highlighting the top 5 best-selling pizzas based on Revenue, Total Quality and Total Orders.
This chart will help us to identify underperforming of less popular pizza option.
## Data Source
Sales Data: The primary dataset used for this analysis is the "pizza_sales.csv" file, containing detailed information about pizza sales and pizza categories in the company.
## Tools/Software used
- MS Office Pro Plus/Excel 2013 - Data Cleaning(attach of Excel files)
- SQL Server Management Studio 20 - Data Analysis 
- Power BI (June 2025) - Creating Report
## Data Cleaning/Preparation
In the initial Data preparation phase, we performed the following task:
1. Data loading and importation.
2. Handling missing values.
3. Data cleaning and formatting.
# Explanatory Data Analysis 
EDA involves uncovering patterns in customer behavior, sales trends, and product performance to inform business decisions, such as:
- Understand sales performance across time, categories, and locations
- Identify top-selling pizzas and least popular items
- Analyze customer ordering behavior (e.g., time of day, day of week)
- Evaluate pricing and revenue trends
- Spot seasonal or promotional impacts
### Data Analysis
Our analysis was executed using SQL server.
# KPI's
**1. Total Revenue:**
```sql
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;
```
**2. Average Order Value:**
```sql
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales;
```
**3. Total Pizzas Sold:**
```sql
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales;
```
**4. Total Orders:**
```sql
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales;
```
**5. Average Pizzas Per Order**
```sql
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS Avg_Pizzas_per_order
FROM pizza_sales;
```
# Revenue Overview
**1. % of Sales by Pizza Category:**
```sql
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category;
```
**2. % of Sales by Pizza Size**
```sql
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size;
```
**3. Total Pizzas Sold by Pizza Category:**
```sql
SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;
```
**4. Top 5 Pizzas by Revenue:**
```sql
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC;
```

