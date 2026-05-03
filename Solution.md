# 📊 Superstore Sales Analysis — Solution

This section contains business-focused analysis using SQL along with insights.

---

## 1. Monthly Sales Trend

**Question:**  
How are sales changing over time?

```sql
SELECT 
    substr("Order Date", -4) || '-' || 
    printf('%02d', CAST(substr("Order Date", 1, instr("Order Date", '/') - 1) AS INTEGER)) AS month,
    SUM(Sales) AS revenue
FROM Superstore
GROUP BY month
ORDER BY month;
```

## 2. Impact of Discount on Profit

**Question:**
How does discount affect profitability?

```sql
SELECT 
    Discount,
    round(SUM(Sales), 2) AS total_sales,
    round(SUM(Profit),2) AS total_profit
FROM Superstore
GROUP BY Discount
ORDER BY Discount;
```

## 3. Loss-Making Products

**Question:**  
Which products are generating losses?

```sql
SELECT 
    product_name, 
    ROUND(SUM(Sales), 2) AS total_sales,
    ABS(ROUND(SUM(Profit), 2)) AS total_loss
FROM Superstore
GROUP BY product_name
HAVING SUM(Profit) < 0
ORDER BY total_loss DESC
LIMIT 10;
```

## 4. Category vs Profitability
**Question:**  
Which categories are most profitable, not just highest in sales?

```sql
SELECT 
    category, 
    round(SUM(Sales), 2) AS total_sales,
    round(SUM(Profit),2) AS total_profit
FROM Superstore
GROUP BY category
ORDER BY total_profit desc;
```

## 5. Regional Profitability

**Question:**  
Which regions are most profitable?

```sql
SELECT 
    region, 
    round(SUM(Sales), 2) AS total_sales,
    round(SUM(Profit),2) AS total_profit
FROM Superstore
GROUP BY region
ORDER BY total_profit desc;
```

## 6. Top Customers & Ranking

**Question:**  
Who are the highest-value customers and how do they rank based on spending?

**SQL Query:**
```sql
SELECT 
    "Customer Name",
    SUM(Sales) AS total_spent,
    RANK() OVER (ORDER BY SUM(Sales) DESC) AS rank
FROM orders
GROUP BY "Customer Name"
LIMIT 10;
Limit 10;
```

## 7. Customer Segment Profitability

**Question:**  
Which customer segments generate the highest sales and profit?

**SQL Query:**
```sql
SELECT 
    Segment,
    SUM(Sales) AS total_sales,
    SUM(Profit) AS total_profit
FROM Superstore
GROUP BY Segment
ORDER BY total_profit DESC;
```

