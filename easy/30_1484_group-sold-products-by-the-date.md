# 🟢 1484 · Group Sold Products By The Date

**Difficulty:** Easy | **Topic:** Aggregation / GROUP_CONCAT / GROUP BY    
**LeetCode:** [Problem Link](https://leetcode.com/problems/group-sold-products-by-the-date/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

For each date, find the number of **different products** sold and their names.
The product names for each date must be sorted **lexicographically** and separated by a comma.
Return the result table ordered by `sell_date`.

---

### Schema

```sql
CREATE TABLE Activities (
  sell_date DATE,
  product   VARCHAR(255)
);
```

### Sample Input

| sell_date  | product    |
|------------|------------|
| 2020-05-30 | Headphone  |
| 2020-06-01 | Pencil     |
| 2020-06-02 | Mask       |
| 2020-05-30 | Basketball |
| 2020-06-01 | Bible      |
| 2020-06-02 | Mask       |
| 2020-05-30 | T-Shirt    |

### Sample Output

| sell_date  | num_sold | products                     |
|------------|----------|------------------------------|
| 2020-05-30 | 3        | Basketball,Headphone,T-shirt |
| 2020-06-01 | 2        | Bible,Pencil                 |
| 2020-06-02 | 1        | Mask                         |

---

### Solution

```sql
SELECT sell_date,
       COUNT(DISTINCT product) AS 'num_sold',
       GROUP_CONCAT(DISTINCT product ORDER BY product SEPARATOR ',') AS 'products'
FROM Activities
GROUP BY sell_date;
```

## 🧠 Approach

1. `GROUP BY sell_date` partitions all rows into per-date buckets.
2. `COUNT(DISTINCT product)` counts how many unique products were sold on each date — `DISTINCT` handles duplicate entries in the table.
3. `GROUP_CONCAT(DISTINCT product ORDER BY product SEPARATOR ',')` collects all unique product names within each group, sorts them lexicographically via `ORDER BY product`, and joins them into a single comma-separated string.
4. The result is naturally ordered by `sell_date` since `GROUP BY` on a date column sorts ascending by default, but an explicit `ORDER BY sell_date` can also be added for clarity.

---

## 📌 Concepts Used

`GROUP BY` · `COUNT(DISTINCT)` · `GROUP_CONCAT()` · `DISTINCT` · `ORDER BY inside aggregate` · `SEPARATOR`

---

## 💭 My Takeaway

`GROUP_CONCAT` is a MySQL-specific gem that most beginners overlook. The power here is combining `DISTINCT`, `ORDER BY`, and `SEPARATOR` all inside a single aggregate call — it handles deduplication, sorting, and formatting in one shot. A must-know function for any string aggregation problem in MySQL.