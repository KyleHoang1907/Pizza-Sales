# Pizza-Sales
# Introduction
Analyze key metrics of pizza sales data to understand the business situation and customer needs. Use SQL Server to query data then use Excel as a data visualization tool.
### Skills: data cleaning, pivot table, window function, data analysis, data visualization, problem solving.

  ## 1.1	Problem statement
  #### The pizza store is a newly opened store but is also the best-selling food store in the market, the number of orders increases day by day. Every second, order data is constantly updated, so store owners cannot control the data with conventional paper methods. They have data analysts come up with KPI's requirement indicators and create charts that make the data more listener-friendly. The main aim is to focus on the types of products that sell well and point out the less popular pizzas in order to increase sales and reduce materials for less efficient products 
  #### Required indicators: Total revenue, Average order value, total pizzas sold, total orders and Average pizzas per order
  ## 1.2	Dataset
      The dataset is under the name Pizza Sales with a total of 4 tables with 48,620 records and 12 fields.
 - Order Details:
The table has the order_details_id which is the primary key of the table along with the order_id, pizza_id as the foreign key of the orders and pizzas table and last, we have the quantity column of each type of pizza.
 - Orders:
This table includes the order_id which is the primary key, and the date and time of each order.
 - Pizza Types:
We have the pizza_type_id as the primary key, along with each pizza's name, category and ingredients.
 - Pizzas:
The pizzas table has the pizza_id as the primary key, and the pizza_type_id as the foreign key from the pizza types table, it also includes the size and price of the pizzas. 
# Insights 
### A. KPI’s
#### 1. Total Revenue:
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;
#### 2. Average Order Value
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM
pizza_sales
#### 3. Total Pizzas Sold
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales
#### 4. Total Orders
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales
#### 5. Average Pizzas Per Order
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) /
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS Avg_Pizzas_per_order
FROM pizza_sales
### B. Daily Trend for Total Orders
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS
total_orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date)
### C. Hourly Trend for Orders
SELECT DATEPART(HOUR, order_time) as order_hours, COUNT(DISTINCT order_id) as
total_orders
from pizza_sales
group by DATEPART(HOUR, order_time)
order by DATEPART(HOUR, order_time)
### D. % of Sales by Pizza Category
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS
DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category
### E. % of Sales by Pizza Size
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS
DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size
### F. Total Pizzas Sold by Pizza Category
SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC
### G. Top 5 Best Sellers by Total Pizzas Sold
SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC
### H. Bottom 5 Best Sellers by Total Pizzas Sold
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC
# Recommendations
Having conducted a thorough analysis of the data, I've identified some valuable insights that have the potential to enhance the business. I would like to propose the following recommendations to the business owners.
 - Store credit or points can be applied as discounts when purchasing pizzas. Additionally, by occasionally multiplying these points on random days, sales may experience an uplift.
 - To enhance Sunday revenue, think about reducing working hours to support employee well-being while also driving pizza sales through limited-time B1G1 flash sales.
 - Let customers design custom pizzas with up to 5 toppings. The best ones chosen by the top chef can be added to the menu, and the customer who created it can name the pizza, allowing for regular menu updates based on customer choices.
 - October has the lowest revenue, likely due to its seasonal nature, with Halloween as a key factor. To leverage this, think about introducing Halloween-themed pizzas for the whole month or the week leading up to the event. If successful, this approach could extend to incorporating themed pizzas for other festivals too.
 - At the close of the year, gather feedback from customers to identify areas for improvement in the restaurant.
 - Due to the lower demand for XL and XXL-sized pizzas, consider introducing a half-and-half pizza option, allowing customers to enjoy two different pizza varieties on a single pie
   
