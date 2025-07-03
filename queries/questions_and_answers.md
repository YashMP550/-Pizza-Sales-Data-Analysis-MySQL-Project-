--Question Set


-- 1. 🧾 Retrieve the total number of orders placed.

-- select count(order_id) as total_number_of_order_placed from orders

-- 2. 💰 Calculate the total revenue generated from pizza sales.

-- select round(sum(p.price * o.quantity),2) as total_revenue from pizzas p

-- inner join order_details o

-- on p.pizza_id = o.pizza_id



-- 3. 🍕 Identify the highest-priced pizza with pizza name.

-- select p.price,pt.name from pizzas p 

-- inner join pizza_types pt

-- on p.pizza_type_id = pt.pizza_type_id

-- order by p.price desc

-- limit 1;


-- 4. 📏 Identify the most common pizza size ordered.

-- select p.size,count(o.order_details_id) as common from pizzas p

-- inner join order_details o

-- on p.pizza_id = o.pizza_id

-- group by p.size

-- order by common desc;


-- 5. 🥇 List the top 5 most ordered pizza types along with their quantities.

-- select pt.name, sum(od.quantity) as quantities from pizza_types pt

-- inner join pizzas p

-- on pt.pizza_type_id = p.pizza_type_id

-- inner join order_details od

-- on od.pizza_id = p.pizza_id

-- group by pt.name

-- order by quantities desc

-- limit 5;


-- 6. ⏰ Determine the distribution of orders by hour of the day.

-- select hour(time) as order_by_hour,count(order_id) as order_count

-- from orders

-- group by order_by_hour

-- order by order_by_hour;


-- 7. 📅 Group the orders by date and calculate the average of total number of pizzas ordered per day.

-- with avg_of_pizza_orderperday as (select date(o.date) as order_date,sum(od.quantity) as total_quantity

-- from orders o

-- inner join order_details od

-- on o.order_id = od.order_id

-- group by date(o.date)

-- )

-- select avg(total_quantity) as avg_pizza_per_day from avg_of_pizza_orderperday


-- 8. 🏆 Determine the to 3 most ordered pizza types based on revenue.

-- select pt.name,round(sum(p.price * o.quantity),2) as total_revenue

-- from pizza_types pt 

-- inner join pizzas p

-- on pt.pizza_type_id = p.pizza_type_id

-- inner join order_details o

-- on o.pizza_id = p.pizza_id

-- group by pt.name

-- order by total_revenue desc

-- limit 3;


-- 9. 📈 Analyze the cumulative revenue generated over monthly.

-- select month(o.date) as months,round(sum(p.price * od.quantity),2) as revenue,round(sum(sum(p.price * od.quantity))

-- over (order by month(o.date)),2) as cum_revenue

-- from orders o

-- inner join order_details od

-- on o.order_id = od.order_id

-- inner join pizzas p

-- on od.pizza_id = p.pizza_id

-- group by month(o.date)

-- order by months


-- 10. 📊 Calculate the percentage contribution of each pizza category type to total revenue.

-- select pt.category,concat(round(sum(p.price * od.quantity *100) / (select sum(p.price * od.quantity)

-- from pizzas p inner join order_details od

-- on p.pizza_id = od.pizza_id),2),"%") as percentage_contribution

-- from pizza_types pt inner join pizzas p

-- on pt.pizza_type_id = p.pizza_type_id

-- inner join order_details od

-- on p.pizza_id = od.pizza_id

-- group by pt.category;


-- 11. 📆 Group the orders by date and calculate the average of pizzas ordered per day.

-- select avg(p.price) as number_of_pizza,date_format(o.date,"%Y-%M-%D") as order_date from pizzas p

-- inner join order_details od

-- on p.pizza_id = od.pizza_id

-- inner join orders o

-- on od.order_id = o.order_id 

-- group by order_date

-- order by number_of_pizza;


-- 12. 🥇 Determine the top 3 most ordered pizza types based on revenue for each pizza category.

-- with top_three as (select pt.category, pt.name, round(sum(od.quantity * p.price),2) as total_revenue,dense_rank()

-- over (partition by pt.category order by round(sum(od.quantity * p.price),2)desc) as revenue_rank

-- from pizza_types pt inner join pizzas p on pt.pizza_type_id = p.pizza_type_id

-- inner join order_details od on od.pizza_id = p.pizza_id

-- group by pt.category, pt.name)

-- select category,name,total_revenue from top_three

-- where revenue_rank<=3

-- order by category,total_revenue desc

