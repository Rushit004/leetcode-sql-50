# 🟡 1321 · Restaurant Growth

**Difficulty:** Medium | **Topic:** Window Functions / CTE / Moving Average    
**LeetCode:** [Problem Link](https://leetcode.com/problems/restaurant-growth/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Compute the 7-day moving average of customer payments (current day + 6 days before).  
Return `visited_on`, total `amount` for the window, and `average_amount` rounded to 2 decimal places.  
Result should be ordered by `visited_on` in ascending order.

---

## 🗂️ Schema
```sql
CREATE TABLE Customer (
  customer_id INT,
  name VARCHAR(30),
  visited_on DATE,
  amount INT
);
```

### Sample Input

| customer_id | name    | visited_on | amount |
|-------------|---------|------------|--------|
| 1           | Jhon    | 2019-01-01 | 100    |
| 2           | Daniel  | 2019-01-02 | 110    |
| 3           | Jade    | 2019-01-03 | 120    |
| 4           | Khaled  | 2019-01-04 | 130    |
| 5           | Winston | 2019-01-05 | 110    |
| 6           | Elvis   | 2019-01-06 | 140    |
| 7           | Anna    | 2019-01-07 | 150    |
| 8           | Maria   | 2019-01-08 | 80     |
| 9           | Jaze    | 2019-01-09 | 110    |
| 1           | Jhon    | 2019-01-10 | 130    |
| 3           | Jade    | 2019-01-10 | 150    |

### Sample Output

| visited_on | amount | average_amount |
|------------|--------|----------------|
| 2019-01-07 | 860    | 122.86         |
| 2019-01-08 | 840    | 120.00         |
| 2019-01-09 | 840    | 120.00         |
| 2019-01-10 | 1000   | 142.86         |

---

## 💡 Solution
```sql
WITH daily AS (
    SELECT
        visited_on,
        SUM(amount) AS daily_amount
    FROM Customer
    GROUP BY visited_on
)

SELECT
    visited_on,
    SUM(daily_amount)  OVER (
        ORDER BY visited_on
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) AS amount,
    ROUND(AVG(daily_amount) OVER (
        ORDER BY visited_on
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ), 2) AS average_amount
FROM daily
LIMIT 100 OFFSET 6;
```

## 🧠 Approach

1. **CTE `daily`** — first collapse multiple transactions on the same day into one row using `SUM(amount) GROUP BY visited_on`.
2. Apply a **sliding window** of 7 rows (`ROWS BETWEEN 6 PRECEDING AND CURRENT ROW`) over the daily totals ordered by date.
3. `SUM()` over the window gives the 7-day total; `AVG()` with `ROUND(..., 2)` gives the moving average.
4. The first valid 7-day window only exists from the 7th row onward — `OFFSET 6` skips the first 6 incomplete windows.
5. `LIMIT 100` is a safe ceiling to avoid fetching unlimited rows after the offset.

---

## 📌 Concepts Used

`CTE (WITH)` · `Window Functions` · `SUM() OVER` · `AVG() OVER` · `ROWS BETWEEN` · `GROUP BY` · `ROUND()` · `LIMIT / OFFSET`

---

## 💭 My Takeaway

The CTE step of pre-aggregating by date is easy to miss — without it, multiple customers on the same day would create duplicate window rows and mess up the average. `OFFSET 6` is a clean trick to skip incomplete windows instead of filtering with a subquery.