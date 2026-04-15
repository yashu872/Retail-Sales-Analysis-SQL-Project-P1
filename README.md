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
### 🔹 Clothing Sales (Nov 2022, Quantity ≥ 4)
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
### 🔹 Average Age (Beauty Category)
```sql
SELECT ROUND(AVG(age), 2) AS avg_age
FROM retail_sales
WHERE category = 'Beauty';
```
###🔹 High Value Transactions (>1000)
```sql
SELECT *
FROM retail_sales
WHERE total_sale > 1000;
```
### 🔹 Transactions by Gender & Category
```sql
SELECT 
    category,
    gender,
    COUNT(*) AS total_transactions
FROM retail_sales
GROUP BY category, gender
ORDER BY category;
```
### 🔹 Best Selling Month Each Year
```sql
SELECT year, month, avg_sale
FROM (
    SELECT 
        EXTRACT(YEAR FROM sale_date) AS year,
        EXTRACT(MONTH FROM sale_date) AS month,
        AVG(total_sale) AS avg_sale,
        RANK() OVER (
            PARTITION BY EXTRACT(YEAR FROM sale_date)
            ORDER BY AVG(total_sale) DESC
        ) AS rank
    FROM retail_sales
    GROUP BY 1,2
) t
WHERE rank = 1;
```
### 🔹 Top 5 Customers
```sql
SELECT 
    customer_id,
    SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;
```
### 🔹 Unique Customers per Category
```sql
SELECT 
    category,
    COUNT(DISTINCT customer_id) AS unique_customers
FROM retail_sales
GROUP BY category;
```
### 🔹 Sales by Shift
```sql
WITH hourly_sale AS (
    SELECT *,
        CASE
            WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
            WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
            ELSE 'Evening'
        END AS shift
    FROM retail_sales
)
SELECT 
    shift,
    COUNT(*) AS total_orders
FROM hourly_sale
GROUP BY shift;
```
## 📈 Key Insights

- Customers belong to multiple age groups across categories  
- High-value transactions (>1000) indicate premium purchases  
- Monthly trends reveal peak sales periods  
- Top customers contribute significantly to revenue  

---

## 📑 Reports Generated

- Sales Summary  
- Monthly Trend Analysis  
- Customer Insights  

---

## ✅ Conclusion

This project provides a strong foundation in:

- SQL querying  
- Data cleaning  
- Business analysis  

It helps in understanding customer behavior, sales trends, and product performance, which are essential for data analyst roles.

---

## 🚀 How to Use

1. Clone this repository  
2. Run database setup queries  
3. Execute analysis queries  
4. Modify queries for deeper insights  

---

## 👨‍💻 Author

**Yash Chaudhary**  
📊 Aspiring Data Analyst  

---

## 🔗 Connect With Me

- 💼 LinkedIn  
- 📺 YouTube  
- 📸 Instagram  

---

⭐ If you like this project, don’t forget to star the repo!
