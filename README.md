# 🛒 Retail Sales Analysis SQL Project

## 📌 Project Overview

- **Project Title**: Retail Sales Analysis  
- **Level**: Beginner  
- **Database**: `p1_retail_db`  

This project demonstrates SQL skills used by data analysts to **explore, clean, and analyze retail sales data**. It includes database setup, data cleaning, exploratory data analysis (EDA), and solving real-world business problems using SQL.

---

## 🎯 Objectives

- Create and set up a retail sales database  
- Perform data cleaning (handle null/missing values)  
- Conduct exploratory data analysis (EDA)  
- Solve business problems using SQL queries  

---

## 🗂️ Project Structure

### 1️⃣ Database Setup

```sql
CREATE DATABASE p1_retail_db;

CREATE TABLE retail_sales
(
    transactions_id INT PRIMARY KEY,
    sale_date DATE,	
    sale_time TIME,
    customer_id INT,	
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,	
    cogs FLOAT,
    total_sale FLOAT
);
```

## 2️⃣ Data Exploration & Cleaning
```sql
-- Total Records
SELECT COUNT(*) FROM retail_sales;

-- Unique Customers
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;

-- Unique Categories
SELECT DISTINCT category FROM retail_sales;

-- Null Check
SELECT * FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;

-- Delete Null Records
DELETE FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;
```
## 📊 Data Analysis Queries
### 🔹 Sales on Specific Date
```sql
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';
```
###🔹 Clothing Sales (Nov 2022, Quantity ≥ 4)
```sql
SELECT *
FROM retail_sales
WHERE category = 'Clothing'
AND TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
AND quantity >= 4;
```
### 🔹 Total Sales by Category
```sql
SELECT 
    category,
    SUM(total_sale) AS net_sale,
    COUNT(*) AS total_orders
FROM retail_sales
GROUP BY category;
```
