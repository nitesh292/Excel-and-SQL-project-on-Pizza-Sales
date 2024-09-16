# Pizzza Shop Sales analysis
## Table of contents
- [Project Ovrview](#project-overview)
- [Data](#data-source)
- [Tools](#tools)
- [Data Cleaning and Prepration](#data-cleaning-and-prepration)
- [Expolatory Data Analysis](expolatory-data-analysis)
- [SQL code ](sql-code)
- [Result and Findings](result/findings)
  
### Project Overview
This data analysis project aims to provide insights into the sales performance of Pizza shop over time and products 
 ![pizza dashboard ](https://github.com/user-attachments/assets/6578f200-1c65-4fe5-a5ef-4ff71ba12eb3)
 
 ### Data Source
 [Download]([Uploading pizza_sales excel file.xlsx…])

### Tools
- Excel - data cleaning , visualization
- MySQL - data validation 

### Data cleaning and prepration
In the initial data preparation phase, we performed the following tasks:
- Data loading and inspection
- Create new column of intrest
- Data cleaning and formating

### Expolatory data analysis 
EDA involved exploring the sales data to answer key questions, such as:
-Total Revenue: The sum of the total price of all pizza orders.

-Average Order Value: The average amount spent per order, calculated by dividing the total revenue by the total number of orders.

-Total Pizzas Sold: The sum of the quantities of all pizzas sold.

-Total Orders: The total number of orders placed.

-Average Pizzas Per Order: The average number of pizzas sold per order, calculated by dividing the total number of pizzas sold by the total number of orders.
data analysis 

-Daily Trend for Total Orders:

Create a bar chart that displays the daily trend of total orders over a specific time period. This chart will help us identify any patterns or fluctuations in order volumes on a daily basis.

-Hourly Trend for Total Orders:

Create a line chart that illustrates the hourly trend of total orders throughout the day. This chart will allow

us to identify peak hours or periods of high order activity.

-Percentage of Sales by Pizza Category:

Create a pie chart that shows the distribution of sales across different pizza categories. This chart will provide insights into the popularity of various pizza categories and their contribution to overall sales.
results/findings

### SQL code

- Total Revenue:
```sql
select sum(total_price) as total_revenue from pizza_sales;
```

- Average order value:
```sql
select sum(total_price)/sum(quantity) as average_order_value from pizza_sales;
```
- Total pizza sold
```sql
select sum(quantity) as total_pizza_sold from pizza_sales;
```
- Average pizza per order
```sql
Select  CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS  Avg_Pizzas_per_order
FROM pizza_sales;
```
- Daily Trends for total orders
```sql
select datename(dw, order_date) as day,count(distinct order_id) as total_order from pizza_sales
group by datename(dw, order_date);
```
- Hourly Trends for total orders
``` sql
select datepart(hour,order_time) as hour,count(distinct order_id) as total_order from pizza_sales
group by  datepart(hour,order_time)
order by datepart(hour,order_time)
```
- Percentage of sales by pizza category
```sql
select pizza_category,sum(total_price) as revenue,
round(sum(total_price)/(select sum(total_price) from pizza_sales)*100,2) as percentage_sale_by_catogary
from pizza_sales
group by pizza_category
```
- Percentage of sales by pizza size
```sql
select pizza_size,round(sum(total_price),2) as revenue,
round(sum(total_price)/(select sum(total_price) from pizza_sales)*100,2) as percentage_sale_by_catogary
from pizza_sales
group by pizza_size
```

### Results/Findings

The analysis results are summarized as follows:
- Sales is highest on Friday & Saturday
- Maximum orders are between 12-2pm  &  4-7pm
- Classic Pizza Have the Maximum  Sale
- Large size pizza are mostly ordered
- The Classic Deluxe Pizza  is the best seller
- The Brie Carre Pizza  is the worst seller










