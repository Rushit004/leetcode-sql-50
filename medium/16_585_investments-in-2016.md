# 🟡 585 · Investments in 2016

**Difficulty:** Medium | **Topic:** Aggregation / Subquery / IN Filter  
**LeetCode:** [Problem Link](https://leetcode.com/problems/investments-in-2016/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Report the sum of all total investment values in 2016 (`tiv_2016`), for all policyholders who:
- Have the same `tiv_2015` value as one or more other policyholders, **and**
- Are not located in the same city as any other policyholder (i.e., the `(lat, lon)` pair must be unique).

Round the result to 2 decimal places.

---

### Schema

```sql
CREATE TABLE Insurance (
  pid      INT,
  tiv_2015 FLOAT,
  tiv_2016 FLOAT,
  lat      FLOAT,
  lon      FLOAT
);
```

### Sample Input

| pid | tiv_2015 | tiv_2016 | lat | lon |
|-----|----------|----------|-----|-----|
| 1   | 10       | 5        | 10  | 10  |
| 2   | 20       | 20       | 20  | 20  |
| 3   | 10       | 30       | 20  | 20  |
| 4   | 10       | 40       | 40  | 40  |

### Sample Output

| tiv_2016 |
|----------|
| 45.00    |

---

### Solution

```sql
SELECT ROUND(SUM(tiv_2016), 2) AS tiv_2016
FROM Insurance
WHERE tiv_2015 IN (
    SELECT tiv_2015
    FROM Insurance
    GROUP BY tiv_2015
    HAVING COUNT(*) > 1
)
AND (lat, lon) IN (
    SELECT lat, lon
    FROM Insurance
    GROUP BY lat, lon
    HAVING COUNT(*) = 1
);
```

## 🧠 Approach

1. Use a subquery on `tiv_2015` grouped by value — keep only values that appear more than once (`HAVING COUNT(*) > 1`). This filters policyholders sharing a 2015 investment value.
2. Use a second subquery on the `(lat, lon)` pair grouped together — keep only coordinate pairs that appear exactly once (`HAVING COUNT(*) = 1`). This ensures the city location is unique.
3. Apply both subquery results as `IN` filters in the main `WHERE` clause to get rows satisfying **both** conditions simultaneously.
4. Sum the `tiv_2016` values of the qualifying rows and round to 2 decimal places using `ROUND(..., 2)`.

---

## 📌 Concepts Used

`IN` · `Subquery` · `GROUP BY` · `HAVING` · `COUNT(*)` · `SUM()` · `ROUND()` · `Composite column filter`

---

## 💭 My Takeaway

The key insight is treating `(lat, lon)` as a **composite key** inside an `IN` clause — MySQL supports tuple comparison natively, which keeps the query clean. The two subqueries act as independent allow-lists and the main query simply intersects them. A great exercise in multi-condition subquery filtering.