🍕 Pizza Sales Data Analysis (MySQL Project)
This project presents a structured SQL-based analysis of a pizza sales dataset. It covers key business insights such as revenue trends, top-selling pizza types, size distribution, category performance, and time-based ordering behavior.

📁 Dataset Overview

| File Name           | Description                                          |
| ------------------- | ---------------------------------------------------- |
| `orders.csv`        | Contains each order’s ID, date, and time             |
| `order_details.csv` | Breaks down orders into pizza items and quantities   |
| `pizzas.csv`        | Details about each pizza including size and price    |
| `pizza_types.csv`   | Metadata for each pizza: name, category, ingredients |


🔗 Foreign Key Relationships
> order_details.order_id → orders.order_id

> order_details.pizza_id → pizzas.pizza_id

> pizzas.pizza_type_id → pizza_types.pizza_type_id
