
# 🗃️ SQL E-Commerce Sales Analytics Project

## 📌 Project Overview

This project simulates an e-commerce database system using **MySQL** and involves comprehensive data management for customers, products, categories, and orders. It is designed to demonstrate SQL skills in database creation, population, and advanced querying for business insights.

The database schema includes:
- **Customers**: 70+ unique customer entries across multiple U.S. cities.
- **Categories**: 70 distinct product categories.
- **Products**: A variety of electronics, furniture, appliances, fitness, and personal care items.
- **Orders**: 70 orders across different dates, linked to customers.

> 🔧 *Key Objective*: To perform data analysis using SQL queries to derive meaningful business insights on sales, product performance, and customer behavior.

---

## 📊 Key SQL Queries & Insights

### 1. **Total Sales by City**
```sql
SELECT customer_city, SUM(total_amount) AS total_sales
FROM Orders o
JOIN Customers c ON o.customer_id = c.customer_id
GROUP BY customer_city
ORDER BY total_sales DESC;
```
- **Insight**: Identifies high-performing cities. Useful for geo-targeted marketing and logistics planning.

### 2. **Top-Selling Products**
```sql
SELECT p.product_name, SUM(od.quantity) AS total_sold
FROM OrderDetails od
JOIN Products p ON od.product_id = p.product_id
GROUP BY p.product_name
ORDER BY total_sold DESC;
```
- **Insight**: Helps optimize inventory, identify popular products, and guide procurement decisions.

### 3. **Monthly Sales Trends**
```sql
SELECT DATE_FORMAT(order_date, '%Y-%m') AS month, SUM(total_amount) AS total_sales
FROM Orders
GROUP BY month
ORDER BY month;
```
- **Insight**: Reveals sales seasonality or monthly performance patterns.

### 4. **Category-wise Sales**
```sql
SELECT p.category, SUM(od.quantity * od.price) AS category_sales
FROM OrderDetails od
JOIN Products p ON od.product_id = p.product_id
GROUP BY p.category
ORDER BY category_sales DESC;
```
- **Insight**: Assists in evaluating category performance to determine focus areas.

---

## 📁 Database Structure

| Table Name   | Description                              |
|--------------|------------------------------------------|
| Customers    | Stores customer details                  |
| Categories   | List of product categories               |
| Products     | Product catalog with price and category  |
| Orders       | Records of purchases with date & amount  |
| OrderDetails | (Suggested) Linking orders to products   |

> 🔧 **Note**: The `OrderDetails` table is referred to in queries but not created. You should define it as follows:

```sql
CREATE TABLE OrderDetails (
    order_detail_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT,
    product_id INT,
    quantity INT,
    price DECIMAL(10, 2),
    FOREIGN KEY (order_id) REFERENCES Orders(order_id),
    FOREIGN KEY (product_id) REFERENCES Products(product_id)
);
```

---

## 🧠 Suggestions & Recommendations

### ✅ Suggestions
- **Normalize categories**: Use `category_id` as foreign key in `Products` instead of category name.
- **Create OrderDetails table**: Crucial for detailed sales reporting and product tracking per order.
- **Data constraints**: Add `NOT NULL`, `UNIQUE`, and appropriate `CHECK` constraints for data integrity.

### 📈 Recommendations
- **Indexing**: Use indexes on `customer_id`, `order_id`, `product_id` for performance.
- **Date range filtering**: Enable year-wise or quarter-wise analytics.
- **ETL-ready structure**: Ensure compatibility for integration with BI tools like Power BI or Tableau.

---

## 🛠️ Tools Used
- MySQL
- SQL Workbench / phpMyAdmin
- Data sourced manually

---

## 📚 Learning Outcomes

- ✅ Mastered SQL DDL and DML commands for schema creation and data insertion.
- ✅ Developed advanced analytical queries using `JOIN`, `GROUP BY`, `ORDER BY`, and aggregate functions.
- ✅ Practiced data normalization and relational data modeling.

---

## 🚀 Getting Started

1. Clone or download the repository.
2. Run the `SAMIALIMYSQLPROJECT.sql` script in MySQL.
3. (Optional) Create and populate `OrderDetails` for advanced analytics.
4. Use included queries or write your own to explore the data.

---

## 📎 License
This project is open-source and available under the [MIT License](LICENSE).
