Select  * from pizza_sales;

select round(sum(total_price),2) as total_revenue from pizza_sales;

select round(SUM(total_price)/COUNT(distinct order_id),2)  as avg_order_value from pizza_sales;

select sum(quantity) as total_pizzas_sold from pizza_sales;

select count(distinct order_id) as total_orders from pizza_sales;

select cast(sum(quantity) as decimal(10,2))/cast(count(distinct order_id) as decimal(10,2)) as avg_order_per_pizza from pizza_sales;

-- Hourly trend for total pizzas sold 
select DATEPART(hour,order_time) as order_hours, sum(quantity) as total_pizzas_sold from pizza_sales
group by DATEPART(hour,order_time) order by DATEPART(hour,order_time);

-- weekly trend for total order
select DATEPART(ISO_WEEK,order_date) as week_number, year(order_date) as order_year, count(distinct order_id) as total_orders
from pizza_sales group by DATEPART(ISO_WEEK,order_date), year(order_date) order by DATEPART(ISO_WEEK,order_date), year(order_date);

-- Percentage of Sales by Pizza Category
select pizza_category, SUM(total_price) as total_sales,round(SUM(total_price) *100/(select SUM(total_price) from pizza_sales),2) as Prcnt_Pizza_Sales from pizza_sales
group by pizza_category

-- Percentage of Sales by Pizza Size
select pizza_size, SUM(total_price) as total_sales,round(SUM(total_price) *100/(select SUM(total_price) from pizza_sales),2) as Prcnt_Pizza_Sales from pizza_sales
group by pizza_size

-- Total Pizzas Sold by Pizza Category
select pizza_category, sum(quantity) as total_pizzas_sold from pizza_sales
group by pizza_category

-- Top 5 Best Sellers by Revenue
select top 5 pizza_name as pizza_name, sum(total_price) as total_revenue
from pizza_sales group by pizza_name order by sum(total_price) desc

-- Top 5 Best Sellers by Total Quantity
select top 5 pizza_name as pizza_name, sum(quantity) as total_qty
from pizza_sales group by pizza_name order by sum(total_price) desc

-- Top 5 Best Sellers by Total Orders
select top 5 pizza_name as pizza_name, count(distinct order_id) as total_orders
from pizza_sales group by pizza_name order by sum(total_price) desc

-- Bottom 5 Best Sellers by Revenue
select top 5 pizza_name as pizza_name, sum(total_price) as total_revenue
from pizza_sales group by pizza_name order by sum(total_price) 

-- Bottom 5 Best Sellers by Total Quantity
select top 5 pizza_name as pizza_name, sum(quantity) as total_qty
from pizza_sales group by pizza_name order by sum(total_price) 

-- Bottom 5 Best Sellers by Total Orders
select top 5 pizza_name as pizza_name, count(distinct order_id) as total_orders
from pizza_sales group by pizza_name order by sum(total_price) 