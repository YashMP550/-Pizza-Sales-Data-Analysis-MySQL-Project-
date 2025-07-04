🍕 Pizza Sales Data Analysis (MySQL Project)
This project presents a structured SQL-based analysis of a pizza sales dataset. It covers key business insights such as revenue trends, top-selling pizza types, size distribution, category performance, and time-based ordering behavior.

📦 Pizza Sales Database Schema
┌────────────┐          ┌────────────────────┐          ┌─────────────┐
│  orders    │          │   order_details    │          │   pizzas    │
├────────────┤          ├────────────────────┤          ├─────────────┤
│ order_id   │◀────────▶│ order_id           │          │ pizza_id    │◀──────┐
│ date       │          │ order_details_id   │          │ pizza_type_id│       │
│ time       │          │ pizza_id           │◀────────▶│ size        │       │
└────────────┘          │ quantity           │          │ price       │       │
                        └────────────────────┘          └─────────────┘       │
                                                                              │
                                                                              ▼
                                                                     ┌────────────────┐
                                                                     │  pizza_types    │
                                                                     ├────────────────┤
                                                                     │ pizza_type_id   │
                                                                     │ name            │
                                                                     │ category        │
                                                                     │ ingredients     │
                                                                     └────────────────┘


🔗 Foreign Key Relationships
> order_details.order_id → orders.order_id

> order_details.pizza_id → pizzas.pizza_id

> pizzas.pizza_type_id → pizza_types.pizza_type_id
