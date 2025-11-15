# Tajudeen Omotosho - Data Analyst Portfolio  
## About

👋 Hi, I'm **Tajudeen Omotosho**
I am a data analyst specializing in transforming complex data into meaningful insights that support informed business decisions. With strong proficiency in SQL, Excel, and DAX, I focus on robust data preparation and analysis. I also develop clear, dynamic dashboards in Power BI and Tableau that communicate insights effectively to stakeholders. My work is driven by precision, clarity, and a commitment to delivering high-quality analytical solutions.   
  
## 🛠️ Skills

**Languages:** Python, SQL. DAX  
**Data Analysis:** pandas, NumPy, Excel, Power Query  
**Visualization:** Power BI, Tableau, Matplotlib, Seaborn  
**Databases:** SQL Server, MySQL, Oracle    
**Tools:** Jupyter Notebook, Mcrosoft SQL Server Manegement Studio 

# Pizza-Sales-Analysis
## Table of Contents
- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Explanatory Data Analysis](#explanatory-data-analysis)
- [Results/Findings](#resultsfindings)
- [References](#references)
## Project Overview 
We set out to analyse the key indicators for Pizza Sales data to gain insight into the business performance. We calculated the following:: Total Revenue, Average Order Value, Total Pizza Sold, Total Orders and Average Pizza Sold.

<img width="968" height="516" alt="Pizza_Sales_screanshot" src="https://github.com/user-attachments/assets/d8d7ae24-26a4-47f4-8696-ddc8cce58ba4" />


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
- MS Office Pro Plus/Excel 2013 - Data Cleaning (attach of Excel files)
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
### KPI's
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
### Revenue Overview
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
**5. Bottom 5 Pizzas by Revenue:**
```sql
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC;
```
### Top 5/Bottom 5 by Sales Quantity
**1. Top 5 Pizzas by Quantity**
```sql
SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC;
```
**2. Bottom 5 Pizzas by Quantity**
```sql
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC;
```
### Top 5/Bottom 5 by Total Orders
**1. Top 5 Pizzas by Total Orders**
```sql
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC;
```
**2. Bottom 5 Pizzas by Total Orders**
```sql
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC;
```
### Trends for Orders
**1. Daily Trend for Total Orders**
```sql
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date);
```
**2. Monthly Trend for Orders**
```sql
select DATENAME(MONTH, order_date) as Month_Name, COUNT(DISTINCT order_id) as Total_Orders
from pizza_sales
GROUP BY DATENAME(MONTH, order_date)Output;
```
### Results/Findings
The analysis results are summarised as follows:
1. The pizza sales results indicate that Thai Chicken Pizza contribute to maximum Revenue.
2. While the Classic Deluxe Pizza contributes to maximum Total Quantity.
3. The Classic Deluxe Pizza also contributes to Maximum Total Orders.
4. The Brie Carre Pizza contributes minimum Revenue.
5. The Brie Carre Pizza also contributes to minimum Total Quantities.
6. Finally, the Brie Carre Pizza contributes to minimum Total Orders.
### Recommendations
#### 1. Leverage High Performers
- Thai Chicken Pizza:
  - Increase visibility with premium placement on menus and promotions.
  - Consider upselling combos (e.g., Thai Chicken Pizza + drink/dessert) to maximize revenue further.
- Classic Deluxe Pizza:
  - Since it drives volume and orders, use it as a “gateway” product.
  - Bundle with higher-margin items to lift overall profitability.
#### 2. Address Low Performers
- Brie Carre Pizza:
  - Re-evaluate recipe, pricing, and positioning. Is it too niche or expensive?
  - Test limited-time promotions or reposition it as a specialty item.
  - If repeated efforts fail, consider phasing it out to reduce menu clutter and focus on stronger sellers.
#### 3. Marketing Strategy
  - Promote Thai Chicken Pizza in premium campaigns (since it’s revenue-rich).
  - Use Classic Deluxe Pizza in mass campaigns (since it’s popular and widely ordered).
  - Experiment with Brie Carre Pizza in niche campaigns targeting adventurous eaters or cheese lovers.
## References 
1. Youtube Tutorial
2. Google Search Engine to debug some code.
3. Stack Overflow
