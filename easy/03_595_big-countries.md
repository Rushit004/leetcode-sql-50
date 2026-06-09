## 🟢 595. Big Countries

**Difficulty:** Easy | **Topic:** Filtering / WHERE  
**LeetCode:** [Problem Link](https://leetcode.com/problems/big-countries/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

A country is **big** if it has:
- an area of at least 3,000,000 km², **or**
- a population of at least 25,000,000.

Find the `name`, `population`, and `area` of all big countries.

Return the result table in **any order**.

---

## 🗂️ Schema

```sql
CREATE TABLE World (
    name        VARCHAR(255) PRIMARY KEY,
    continent   VARCHAR(255),
    area        INT,
    population  INT,
    gdp         BIGINT
);
```

---

## 📥 Sample Input

**World**

| name        | continent | area    | population | gdp          |
|-------------|-----------|---------|------------|--------------|
| Afghanistan | Asia      | 652230  | 25500100   | 20343000000  |
| Albania     | Europe    | 28748   | 2831741    | 12960000000  |
| Algeria     | Africa    | 2381741 | 37100000   | 188681000000 |
| Andorra     | Europe    | 468     | 78115      | 3712000000   |
| Angola      | Africa    | 1246700 | 20609294   | 100990000000 |

---

## 📤 Sample Output

| name        | population | area    |
|-------------|------------|---------|
| Afghanistan | 25500100   | 652230  |
| Algeria     | 37100000   | 2381741 |

---

## 💡 Solution

```sql
SELECT name, population, area
FROM World
WHERE area >= 3000000 OR population >= 25000000;
```

---

## 🔍 Approach

1. Select `name`, `population`, and `area` columns from the `World` table.
2. Apply a `WHERE` filter with two conditions joined by `OR`.
3. First condition checks if `area >= 3000000` (at least 3 million km²).
4. Second condition checks if `population >= 25000000` (at least 25 million people).
5. A country satisfying **either** condition is included in the result.

---

## 🧠 Concepts Used

`WHERE clause` `OR condition` `Filtering` `Comparison Operators` `Multi-column SELECT`

---

## ✍️ My Takeaway

This problem is straightforward but reinforces an important SQL concept — using `OR` to combine multiple filter conditions. A row only needs to satisfy **one** of the conditions to be included, unlike `AND` where both must be true. Always think carefully about whether your business logic requires `AND` or `OR` before writing the filter.
