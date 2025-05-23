# Pizza Sales Analysis Project

This project provides a detailed analysis of pizza sales data using *SQL* for data extraction and *Microsoft Excel* for data visualization. It uncovers key business insights to help improve decision-making in a pizza restaurant's operations and strategy.

## 📊 Project Summary

- *Objective*: Analyze sales data to identify performance trends, customer behavior, and product insights.
- *Tools Used*:
  - SQL (MySQL/PostgreSQL)
  - Microsoft Excel (PivotTables, Charts, Slicers, Dashboards)

## ⚙️ Features

- Total revenue, total orders, and average order value
- Best and worst selling pizzas
- Sales breakdown by pizza size and category
- Busiest days and hours for sales
- Monthly and hourly trends
- Interactive Excel dashboard for visualization

## 🧠 Insights

- Friday and Saturday evenings are peak sales periods
- Larger pizzas generate more revenue
- "The classic Chicken Pizza" are top-performing items
- Some pizzas have consistently poor sales and may need review
- Visual analysis highlights seasonal and hourly patterns

## 🛠️ How It Works

1. *SQL Queries*:
   - Used to clean, join, and analyze raw order and menu data.
   - Extracted key metrics like order totals, item frequencies, and revenue.

2. *Excel Dashboard*:
   - Built using PivotTables and charts.
   - Includes slicers for filtering by date, category, size, and more.

## 📂 Project Structure

1. Pizza Sales Analysis

2. SQl Query

3. --CREATE TABLE 

CREATE TABLE pizza_sales
            (
            pizza_id INT PRIMARY KEY,	
			order_id INT,
			pizza_name_id VARCHAR(50),
			quantity INT,
			order_date	DATE,
			order_time	TIME,
			unit_price FLOAT,
			total_price FLOAT,
			pizza_size	VARCHAR(50),
			pizza_category	VARCHAR(50),
			pizza_ingredients	VARCHAR(200),
			pizza_name VARCHAR(50)
			)

			
select * 
from pizza_sales

SELECT 
sum(total_price) as Total_revenue
FROM pizza_sales


SELECT 
sum(total_price)/count(distinct order_id) as Avg_order_values
FROM pizza_sales

SELECT 
sum(quantity) as Total_pizza_sold
FROM pizza_sales


SELECT 
count(distinct order_id) as Total_number_order
FROM pizza_sales

SELECT 
cast (cast (sum(quantity) as Decimal(10,2))/
cast (count(distinct order_id) as Decimal(10,2)) as Decimal(10,2)) as Average_Pizza_per_orders
FROM pizza_sales

--Daily Trend for orders

SELECT 
    TO_CHAR("order_date", 'Day') AS order_day,
    COUNT(DISTINCT "order_id") AS total_orders
FROM 
    pizza_sales
GROUP BY 
    1
	
--Hourly state train for Total orders:

SELECT 
EXTRACT(HOUR FROM order_time) as order_hours,
 COUNT(DISTINCT "order_id") AS total_orders
FROM 
    pizza_sales
GROUP BY 1
 
-- percentage of sales by Pizza category: 

SELECT pizza_category,
      sum(total_price)*100/(select(sum(total_price)) FROM 
    pizza_sales) as Percentage_sale
FROM 
    pizza_sales
GROUP BY 1

--  percentage of sales by Pizza size:
SELECT pizza_size,
      sum(total_price)*100/(select(sum(total_price)) FROM 
    pizza_sales) as Percentage_sale
FROM 
    pizza_sales
GROUP BY 1

--total Pizza sold by Pizza category
 SELECT pizza_category,
sum(quantity) total_pizza_sold
 FROM  pizza_sales
 GROUP BY 1

 --Top 5 best seller by total Pizza sold
 SELECT pizza_name,
 sum(quantity) total_pizza_sold
 FROM  pizza_sales
 GROUP BY 1
 order by 2 desc
 limit 5

 -- bottom five worst sailors by total Pizza sold :
 SELECT pizza_name,
 sum(quantity) total_pizza_sold
 FROM  pizza_sales
 GROUP BY 1
 order by 2 asc
 limit 5

 
