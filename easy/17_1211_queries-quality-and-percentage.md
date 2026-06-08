# 🟢 1211 · Queries Quality and Percentage

**Difficulty:** Easy | **Topic:** Aggregation / Subquery  
**LeetCode:** [Problem Link](https://leetcode.com/problems/queries-quality-and-percentage/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find each `query_name` and compute two metrics:

- **quality** — the average of the ratio `rating / position`, rounded to 2 decimal places.
- **poor_query_percentage** — the percentage of queries where `rating < 3`, rounded to 2 decimal places.

Return the result table in any order.

---

### Schema

```sql
CREATE TABLE Queries (
  query_name VARCHAR(30),
  result     VARCHAR(50),
  position   INT,
  rating     INT
);
```

### Sample Input

| query_name | result           | position | rating |
|------------|------------------|----------|--------|
| Dog        | Golden Retriever | 1        | 5      |
| Dog        | German Shepherd  | 2        | 5      |
| Dog        | Mule             | 200      | 1      |
| Cat        | Shirazi          | 5        | 2      |
| Cat        | Siamese          | 3        | 3      |
| Cat        | Sphynx           | 7        | 4      |


### Sample Output

| query_name | quality | poor_query_percentage |
|------------|---------|-----------------------|
| Dog        | 2.50    | 33.33                 |
| Cat        | 0.66    | 33.33                 |

---

### Solution

```sql
SELECT query_name,
ROUND(AVG(rating/position), 2) AS 'quality',
ROUND(((SELECT COUNT(*)
        FROM Queries t2
        WHERE t2.rating < 3
        AND t2.query_name = t1.query_name) / COUNT(query_name)) * 100, 2) AS 'poor_query_percentage'
FROM Queries t1
GROUP BY query_name
```

## 🧠 Approach

1. `GROUP BY query_name` to process each query group separately.
2. Compute `quality` as `AVG(rating / position)` — MySQL evaluates the division per row before averaging, giving the correct per-row ratio mean.
3. For `poor_query_percentage`, use a **correlated subquery** that counts rows with `rating < 3` for the current `query_name`, then divide by `COUNT(query_name)` (total rows in the group) and multiply by `100` to get a percentage.
4. `ROUND(..., 2)` is applied to both metrics to meet the required precision.

---

## 📌 Concepts Used

`AVG()` · `COUNT()` · `ROUND()` · `GROUP BY` · `Correlated Subquery` · `Conditional Filtering` · `Arithmetic in SELECT`

---

## 💭 My Takeaway

The `quality` column is straightforward once you realise `AVG(rating/position)` computes the ratio row-by-row first and then averages — not the other way around. The trickier part is `poor_query_percentage`: using a correlated subquery here works cleanly, though a `SUM(CASE WHEN rating < 3 THEN 1 ELSE 0 END)` approach inside the same `GROUP BY` would be more efficient at scale by avoiding a subquery per group. Good problem for practising both styles.