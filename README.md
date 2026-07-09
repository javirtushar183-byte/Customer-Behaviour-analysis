# 🛍️ Customer Revenue & Segmentation Insights

### *Python | SQL | Power BI*

**By Tushar J**

An end-to-end data analytics project analyzing **3,900+ retail transactions** to uncover customer behavior, revenue trends, and product performance using Python, PostgreSQL, and Power BI.

---

## 📌 Project Objective

To analyze customer shopping behavior and generate actionable business insights through:

* Data cleaning & transformation (Python)
* SQL-based business analysis
* Interactive dashboard visualization

---

## 🛠️ Tech Stack

* **Python (Pandas, NumPy)** – Data Cleaning & Feature Engineering
* **PostgreSQL** – Advanced SQL Analysis (CTEs, Window Functions)
* **Power BI** – Dashboard & Data Visualization
* **SQLAlchemy** – Database Connectivity

---

## 🐍 Data Cleaning & Transformation (Python)

The dataset was prepared using Python to ensure high-quality analysis:

* Handled missing values using **median imputation**
* Standardized column names using **snake_case**
* Created **age-based customer segmentation**
* Converted categorical purchase frequency into numeric format
* Removed redundant/unnecessary columns
* Loaded cleaned data into PostgreSQL

This process ensured a **clean, structured, and analysis-ready dataset**.

---

## 🗄️ SQL Analysis & Business Queries

### 🔹 Total Revenue by Gender

```sql
SELECT gender,
       SUM(purchase_amount) AS total_revenue
FROM customer
GROUP BY gender;
```

### 🔹 Customers Using Discounts & Spending Above Average

```sql
WITH cte AS (
    SELECT AVG(purchase_amount) AS average_spend
    FROM customer
)
SELECT c.customer_id,
       c.purchase_amount
FROM customer c, cte
WHERE c.discount_applied = 'Yes'
  AND c.purchase_amount >= cte.average_spend;
```

### 🔹 Top 5 Highest Rated Products

```sql
SELECT item_purchased,
       ROUND(AVG(review_rating)::numeric, 2) AS average_product_rating
FROM customer
GROUP BY item_purchased
ORDER BY AVG(review_rating) DESC
LIMIT 5;
```

### 🔹 Shipping Type Spend Comparison

```sql
SELECT shipping_type,
       ROUND(AVG(purchase_amount), 2) AS average_spend
FROM customer
WHERE shipping_type IN ('Standard', 'Express')
GROUP BY shipping_type;
```

### 🔹 Subscriber vs Non-Subscriber Revenue

```sql
SELECT subscription_status,
       COUNT(customer_id) AS total_customers,
       ROUND(AVG(purchase_amount), 2) AS avg_spend,
       SUM(purchase_amount) AS total_revenue
FROM customer
GROUP BY subscription_status
ORDER BY total_revenue DESC;
```

### 🔹 Discount Usage by Product

```sql
SELECT item_purchased,
       ROUND(
           SUM(CASE WHEN discount_applied = 'Yes' THEN 1 ELSE 0 END) * 100.0
           / COUNT(*), 2
       ) AS discount_percentage
FROM customer
GROUP BY item_purchased
ORDER BY discount_percentage DESC
LIMIT 5;
```

### 🔹 Customer Segmentation

```sql
WITH customer_type AS (
    SELECT customer_id,
           CASE
             WHEN previous_purchases = 1 THEN 'New'
             WHEN previous_purchases BETWEEN 2 AND 10 THEN 'Returning'
             ELSE 'Loyal'
           END AS customer_segment
    FROM customer
)
SELECT customer_segment,
       COUNT(*) AS total_customers
FROM customer_type
GROUP BY customer_segment;
```

---

## 📈 Power BI Dashboard

An interactive dashboard was created to consolidate insights into a single view.

### 📊 Dashboard Highlights:

* Total Customers: **3.9K**
* Average Purchase Amount: **$59.76**
* Average Rating: **3.75**
* Category-wise Revenue Distribution
* Age Group Analysis
* Subscription Insights
* Demographic Revenue Trends

---

## 📷 Dashboard Preview

```markdown```
![Dashboard](customer_revenue_dashboard.jpeg)

---

## 🚀 Key Insights

* Identified top-performing products driving customer satisfaction
* Segmented customers into **New, Returning, and Loyal groups**
* Analyzed revenue distribution across **age & gender**
* Measured impact of **discounts and subscriptions** on revenue
* Built a centralized dashboard for **decision-making**

---

## 📌 Conclusion

This project demonstrates complete **end-to-end data analytics skills**:

* Data Cleaning (Python)
* Data Analysis (SQL)
* Data Visualization (Power BI)

It transforms raw retail data into **meaningful, business-driven insights**, enabling smarter and faster decision-making.
