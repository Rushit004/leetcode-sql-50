## 🟢 1068. Product Sales Analysis I

**Difficulty:** Easy | **Topic:** JOIN / INNER JOIN  
**LeetCode:** [Problem Link](https://leetcode.com/problems/product-sales-analysis-i/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the `product_name`, `year`, and `price` for each sale in the `Sales` table.

Return the result table in **any order**.

---

## 🗂️ Schema

```sql
CREATE TABLE Sales (
    sale_id     INT,
    product_id  INT,
    year        INT,
    quantity    INT,
    price       INT,
    PRIMARY KEY (sale_id, year)
);

CREATE TABLE Product (
    product_id    INT PRIMARY KEY,
    product_name  VARCHAR(50)
);
```

---

## 📥 Sample Input

**Sales**

| sale_id | product_id | year | quantity | price |
|---------|------------|------|----------|-------|
| 1       | 100        | 2008 | 10       | 5000  |
| 2       | 100        | 2009 | 12       | 5000  |
| 7       | 200        | 2011 | 15       | 9000  |

**Product**

| product_id | product_name |
|------------|--------------|
| 100        | Nokia        |
| 200        | Apple        |
| 300        | Samsung      |

---

## 📤 Sample Output

| product_name | year | price |
|--------------|------|-------|
| Nokia        | 2008 | 5000  |
| Nokia        | 2009 | 5000  |
| Apple        | 2011 | 9000  |

---

## 💡 Solution

```sql
SELECT t2.product_name, t1.year, t1.price
FROM Sales t1
JOIN Product t2
ON t1.product_id = t2.product_id;
```

---

## 🔍 Approach

1. Start with the `Sales` table as the base table since all sale records are needed.
2. `INNER JOIN` with the `Product` table on the matching `product_id` column.
3. Fetch `product_name` from the `Product` table and `year`, `price` from the `Sales` table.
4. Since it's an `INNER JOIN`, only rows with a matching `product_id` in both tables are returned.

---

## 🧠 Concepts Used

`INNER JOIN` `JOIN` `Multi-table Query` `Table Alias` `Column Selection`

---

## ✍️ My Takeaway

This problem highlights the difference between `INNER JOIN` and `LEFT JOIN`. Here an `INNER JOIN` is appropriate because we only want sales that have a corresponding product — orphan sales with no product entry are irrelevant. Always choose your join type based on whether unmatched rows from either table need to be preserved or discarded.
