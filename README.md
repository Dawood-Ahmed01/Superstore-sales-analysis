# 📊 Superstore Sales Analysis

> Analyzed Superstore sales data using SQL to identify **profit drivers, loss-making areas, and the impact of discounts on profitability.**

---

## 🔎 Analysis Questions

This project answers the following business questions:

* 🏆 Which **Category** generates the highest profit?
* 🌎 Which **Region** performs best?
* 📉 Where are losses coming from within **Furniture**?
* 💸 What is the relationship between **Discount and Profit**?
* ⭐ Which products generate the most profit?
* ⚠️ Which products generate the lowest profit?

---

## 💻 SQL Analysis

### 🏆 Most Profitable Categories

```sql
SELECT category,
       ROUND(SUM(profit), 2) AS total_profit
FROM superstore
GROUP BY category
ORDER BY total_profit DESC;
```

### 🌎 Region-wise Profit

```sql
SELECT region,
       ROUND(SUM(profit), 2) AS total_profit
FROM superstore
GROUP BY region
ORDER BY total_profit DESC;
```

### 📉 Furniture — Sub-Category Profitability

```sql
SELECT subcategory,
       ROUND(SUM(profit), 2) AS total_profit,
       ROUND(AVG(discount), 2) AS discount
FROM superstore
WHERE category = 'Furniture'
GROUP BY 1
ORDER BY total_profit ASC;
```

### 💸 Discount & Profit Relationship

```sql
SELECT 
    CASE
        WHEN discount = 0 THEN 'No Discount'
        WHEN discount <= 0.2 THEN 'Low 0-20%'
        WHEN discount <= 0.4 THEN 'Medium 20-40%'
        ELSE 'High 40-100%'
    END AS discount_range,
    ROUND(SUM(profit), 2) AS total_profit,
    COUNT(*) AS Num_Orders
FROM superstore
GROUP BY discount_range
ORDER BY total_profit DESC;
```

### ⭐ Top 5 Products by Profit

```sql
SELECT subcategory,
       ROUND(SUM(profit), 2) AS total_profit
FROM superstore
GROUP BY 1
ORDER BY 2 DESC
LIMIT 5;
```

### ⚠️ Bottom 5 Products by Profit

```sql
SELECT subcategory,
       ROUND(SUM(profit), 2) AS Low_Profit
FROM superstore
GROUP BY 1
ORDER BY 2 ASC
LIMIT 5;
```

---

# 📈 Key Findings

### 🥇 Category Performance

**Technology** is the most profitable category with approximately **$145K** in profit, followed by **Office Supplies** with **$122K**.

**Furniture** is the least profitable category at approximately **$18K**, mainly due to discount-heavy sub-categories.

---

### 🌎 Regional Performance

**West** and **East** are the strongest-performing regions in terms of profit.

**Central** is the least profitable region, making it a potential area for improvement.

---

### 💸 Discount & Profit Relationship

The most important finding is the relationship between **discounting and profitability**.

| Discount Range |     Profit |
| -------------- | ---------: |
| No Discount    | **+$320K** |
| 40%+ Discount  |  **-$99K** |

This suggests that aggressive discounting can significantly reduce profitability.

---

### ⚠️ Problem Products

**Tables** and **Bookcases** are the biggest loss-making sub-categories.

Their relatively high average discounts:

* **Tables:** ~26%
* **Bookcases:** ~21%

appear to be contributing to their poor profitability.

---

### ⭐ Star Products

**Copiers, Phones, and Accessories** are among the strongest profit-generating sub-categories.

These products could be studied further to understand which pricing and discount strategies are driving their performance.

---

# 💡 Business Recommendation

> **Revisit the discount strategy, especially for Tables and Bookcases.**

Discounts above **20%** should be carefully evaluated because they can significantly reduce or even eliminate profit.

A more controlled discount policy could help improve overall profitability.

---

## 🛠️ Skills Demonstrated

* SQL
* Data Aggregation
* `GROUP BY`
* `ORDER BY`
* `CASE` Statements
* Profitability Analysis
* Discount Analysis
* Business Insights
* Data-Driven Recommendations

---

## 🎯 Project Goal

The goal of this project was to use SQL not just to retrieve data, but to **turn sales data into actionable business insights**.

**Raw Data → SQL Analysis → Business Findings → Recommendations**
