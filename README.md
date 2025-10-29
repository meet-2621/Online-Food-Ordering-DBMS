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

🍽️ 2. Insert Sample Data
INSERT INTO customers VALUES
(1, 'Manmeet'), 
(2, 'Aarav'), 
(3, 'Neha');

INSERT INTO menu VALUES
(101, 'Burger', 120.00),
(102, 'Pizza', 250.00),
(103, 'Pasta', 180.00),
(104, 'Fries', 80.00);

INSERT INTO orders VALUES
(1001, 1, '2025-10-25'),
(1002, 2, '2025-10-26'),
(1003, 3, '2025-10-26');

INSERT INTO order_details VALUES
(1001, 101, 2),
(1001, 104, 1),
(1002, 102, 1),
(1002, 104, 2),
(1003, 103, 1),
(1003, 101, 1);

📊 3. Useful Queries
🧾 (a) Show total bill per order
SELECT 
    o.order_id,
    c.name AS customer,
    SUM(m.price * od.quantity) AS total_bill
FROM orders o
JOIN order_details od ON o.order_id = od.order_id
JOIN menu m ON od.item_id = m.item_id
JOIN customers c ON o.cust_id = c.cust_id
GROUP BY o.order_id, c.name;

✅ Example Output
order_id	customer	total_bill
1001	Manmeet	320.00
1002	Aarav	410.00
1003	Neha	300.00
🍕 (b) Find the most popular item
SELECT 
    m.item_name,
    SUM(od.quantity) AS total_ordered
FROM order_details od
JOIN menu m ON od.item_id = m.item_id
GROUP BY m.item_name
ORDER BY total_ordered DESC
LIMIT 1;

✅ Example Output
item_name	total_ordered
Burger	3
🧩 Project Summary

✔️ Demonstrates database design and relationships
✔️ Uses joins and aggregate functions (SUM, GROUP BY, ORDER BY)
✔️ Helps understand query optimization and data analysis

🛠️ Tools Used:-
MySQL / SQL Workbench
VS Code (optional for editing)

👩‍💻 Author

Manmeet Kaur
📅 Created: October 2025
🔗 #SQL #Database #DBMS #MiniProject #LearningByDoing


📦 How to use:
1. Copy this entire content into a file named **`README.md`**
2. Upload it to your GitHub repository (`Online-Food-Ordering-DBMS`)
3. GitHub will automatically display it as your project page
 
