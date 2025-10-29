# 🍽️ Online Food Ordering Database (Mini DBMS Project)

### 💡 Project Overview
This project simulates a simple **restaurant food ordering system** using SQL.  
It demonstrates how databases manage real-world relationships between **customers**, **menu items**, and **orders** — including how to calculate total bills and identify popular items.

---

## 🧱 1. Database and Tables

```sql
CREATE DATABASE food_ordering;
USE food_ordering;

CREATE TABLE customers (
    cust_id INT PRIMARY KEY,
    name VARCHAR(50)
);

CREATE TABLE menu (
    item_id INT PRIMARY KEY,
    item_name VARCHAR(50),
    price DECIMAL(6,2)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    cust_id INT,
    order_date DATE,
    FOREIGN KEY (cust_id) REFERENCES customers(cust_id)
);

CREATE TABLE order_details (
    order_id INT,
    item_id INT,
    quantity INT,
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (item_id) REFERENCES menu(item_id)
);
