<div align="center">

<img src="https://capsule-render.vercel.app/api?type=rect&color=0:0f0c29,50:302b63,100:24243e&height=200&section=header&text=LeetCode%20SQL%2050&fontSize=52&fontColor=ffffff&animation=fadeIn&fontAlignY=45&desc=50%20Problems%20%7C%20Solved%20%7C%20Documented%20%7C%20MySQL&descAlignY=68&descColor=a78bfa&descSize=16" />

</div>

<div align="center">

[![Solved](https://img.shields.io/badge/Solved-50%2F50-6d28d9?style=for-the-badge&logo=leetcode&logoColor=white)](https://leetcode.com/studyplan/top-sql-50/)
[![Easy](https://img.shields.io/badge/🟢%20Easy-32-22c55e?style=for-the-badge)](#-easy--32-problems)
[![Medium](https://img.shields.io/badge/🟡%20Medium-17-f59e0b?style=for-the-badge)](#-medium--17-problems)
[![Hard](https://img.shields.io/badge/🔴%20Hard-1-ef4444?style=for-the-badge)](#-hard--1-problem)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://www.mysql.com/)
[![Stars](https://img.shields.io/github/stars/Rushit004/leetcode-sql-50?style=for-the-badge&color=fbbf24)](https://github.com/Rushit004/leetcode-sql-50/stargazers)

</div>

---

<div align="center">

### Not just solutions — a full study companion.
*Every problem has the schema, sample data, a working query, a step-by-step breakdown, and a personal takeaway so you know **why** it works — not just that it does.*

</div>

---

## 📌 Why This Repo?

Most SQL solution repos dump queries in a `.sql` file and call it done.

This one is different. Every single problem is its own documented file — with the table schema, sample input/output, the SQL solution, a numbered approach walking through the logic, the concepts it exercises, and a personal takeaway distilled from actually solving it. Think of it as the notes you wish someone had written before you started.

**Who is this for?**
- 🎓 Students preparing for placements / internships
- 💼 Anyone brushing up SQL for data analyst / data engineering roles
- 🏗️ People who want to understand *why* a query works, not just copy it

---

## 🗂️ Repo Structure

```
leetcode-sql-50/
│
├── 📂 easy/           # 32 problems — WHERE, JOINs, Aggregation, String Functions
├── 📂 medium/         # 17 problems — Subqueries, Window Functions, CTEs, UNION
├── 📂 hard/           # 1  problem  — DENSE_RANK, Advanced Window Functions
└── 📄 README.md
```

**Each file follows this exact structure:**

```
# 🟡 [Problem Number] · [Title]
Difficulty + Topic badge | LeetCode link
---
📋 Problem Statement
🗂️ Schema  (CREATE TABLE block)
📥 Sample Input  (markdown table)
📤 Sample Output (markdown table)
💡 Solution  (SQL code block)
🔍 Approach  (numbered steps)
📌 Concepts Used  (`backtick` tags)
💭 My Takeaway  (1–2 sentences in plain language)
```

---

## 🟢 Easy — 32 Problems

| # | LC # | Problem | Topic |
|:---:|:---:|---------|-------|
| 01 | [1757](https://leetcode.com/problems/recyclable-and-low-fat-products/) | [Recyclable and Low Fat Products](easy/01_1757_recyclable-and-low-fat-products.md) | Filtering / WHERE |
| 02 | [584](https://leetcode.com/problems/find-customer-referee/) | [Find Customer Referee](easy/02_584_find-customer-referee.md) | NULL Handling / Filtering |
| 03 | [595](https://leetcode.com/problems/big-countries/) | [Big Countries](easy/03_595_big-countries.md) | Filtering / WHERE |
| 04 | [1148](https://leetcode.com/problems/article-views-i/) | [Article Views I](easy/04_1148_article-views-i.md) | Filtering / WHERE |
| 05 | [1683](https://leetcode.com/problems/invalid-tweets/) | [Invalid Tweets](easy/05_1683_invalid-tweets.md) | String Functions / LENGTH() |
| 06 | [1378](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/) | [Replace Employee ID With The Unique Identifier](easy/06_1378_replace-employee-id-with-the-unique-identifier.md) | JOIN / LEFT JOIN |
| 07 | [1068](https://leetcode.com/problems/product-sales-analysis-i/) | [Product Sales Analysis I](easy/07_1068_product-sales-analysis-i.md) | JOIN / INNER JOIN |
| 08 | [1581](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/) | [Customer Who Visited but Did Not Make Any Transactions](easy/08_1581_customer-who-visited-but-did-not-make-any-transactions.md) | LEFT JOIN / NULL / GROUP BY |
| 09 | [197](https://leetcode.com/problems/rising-temperature/) | [Rising Temperature](easy/09_197_rising-temperature.md) | Self JOIN / DATEDIFF |
| 10 | [1661](https://leetcode.com/problems/average-time-of-process-per-machine/) | [Average Time of Process per Machine](easy/10_1661_average-time-of-process-per-machine.md) | Self JOIN / Aggregation |
| 11 | [577](https://leetcode.com/problems/employee-bonus/) | [Employee Bonus](easy/11_577_employee-bonus.md) | LEFT JOIN / NULL Handling |
| 12 | [1280](https://leetcode.com/problems/students-and-examinations/) | [Students and Examinations](easy/12_1280_students-and-examinations.md) | CROSS JOIN / Aggregation |
| 13 | [620](https://leetcode.com/problems/not-boring-movies/) | [Not Boring Movies](easy/13_620_not-boring-movies.md) | WHERE / MOD |
| 14 | [1251](https://leetcode.com/problems/average-selling-price/) | [Average Selling Price](easy/14_1251_average-selling-price.md) | JOIN / CASE WHEN / AVG |
| 15 | [1075](https://leetcode.com/problems/project-employees-i/) | [Project Employees I](easy/15_1075_project-employees-i.md) | JOIN / AVG |
| 16 | [1633](https://leetcode.com/problems/percentage-of-users-attended-a-contest/) | [Percentage of Users Attended a Contest](easy/16_1633_percentage-of-users-attended-a-contest.md) | JOIN / Subquery / Aggregation |
| 17 | [1211](https://leetcode.com/problems/queries-quality-and-percentage/) | [Queries Quality and Percentage](easy/17_1211_queries-quality-and-percentage.md) | AVG / Conditional Aggregation |
| 18 | [2356](https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/) | [Number of Unique Subjects Taught by Each Teacher](easy/18_2356_number-of-unique-subjects-taught-by-each-teacher.md) | COUNT DISTINCT |
| 19 | [1141](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/) | [User Activity for the Past 30 Days I](easy/19_1141_user-activity-for-the-past-30-days-i.md) | Date Filtering / COUNT DISTINCT |
| 20 | [596](https://leetcode.com/problems/classes-more-than-5-students/) | [Classes More Than 5 Students](easy/20_596_classes-with-at-least-5-students.md) | GROUP BY / HAVING |
| 21 | [1729](https://leetcode.com/problems/find-followers-count/) | [Find Followers Count](easy/21_1729_find-followers-count.md) | GROUP BY / COUNT |
| 22 | [619](https://leetcode.com/problems/biggest-single-number/) | [Biggest Single Number](easy/22_619_biggest-single-number.md) | Subquery / MAX / HAVING |
| 23 | [1731](https://leetcode.com/problems/the-number-of-employees-which-report-to-each-employee/) | [Number of Employees Reporting to Each Employee](easy/23_1731_the-number-of-employees-which-report-to-each-employee.md) | Self JOIN / Aggregation |
| 24 | [1789](https://leetcode.com/problems/primary-department-for-each-employee/) | [Primary Department for Each Employee](easy/24_1789_primary-department-for-each-employee.md) | UNION / Filtering |
| 25 | [610](https://leetcode.com/problems/triangle-judgement/) | [Triangle Judgement](easy/25_610_triangle-judgement.md) | CASE WHEN |
| 26 | [1978](https://leetcode.com/problems/employees-whose-manager-left-the-company/) | [Employees Whose Manager Left the Company](easy/26_1978_employees-whose-manager-left-the-company.md) | Subquery / NOT IN |
| 27 | [1667](https://leetcode.com/problems/fix-names-in-a-table/) | [Fix Names in a Table](easy/27_1667_fix-names-in-a-table.md) | UPPER / LOWER / CONCAT / SUBSTR |
| 28 | [1527](https://leetcode.com/problems/patients-with-a-condition/) | [Patients With a Condition](easy/28_1527_patients-with-a-condition.md) | LIKE / String Matching |
| 29 | [196](https://leetcode.com/problems/delete-duplicate-emails/) | [Delete Duplicate Emails](easy/29_196_delete-duplicate-emails.md) | DELETE / Self JOIN |
| 30 | [1484](https://leetcode.com/problems/group-sold-products-by-the-date/) | [Group Sold Products By The Date](easy/30_1484_group-sold-products-by-the-date.md) | GROUP_CONCAT / GROUP BY |
| 31 | [1327](https://leetcode.com/problems/list-the-products-ordered-in-a-period/) | [List the Products Ordered in a Period](easy/31_1327_list-the-products-ordered-in-a-period.md) | JOIN / HAVING / Date Filter |
| 32 | [1517](https://leetcode.com/problems/find-users-with-valid-e-mails/) | [Find Users With Valid E-Mails](easy/32_1517_find-users-with-valid-e-mails.md) | REGEXP / Pattern Validation |

---

## 🟡 Medium — 17 Problems

| # | LC # | Problem | Topic |
|:---:|:---:|---------|-------|
| 01 | [570](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/) | [Managers with at Least 5 Direct Reports](medium/01_570_managers-with-at-least-5-direct-reports.md) | Self JOIN / GROUP BY / HAVING |
| 02 | [1934](https://leetcode.com/problems/confirmation-rate/) | [Confirmation Rate](medium/02_1934_confirmation-rate.md) | LEFT JOIN / SUM(condition) / IFNULL |
| 03 | [1193](https://leetcode.com/problems/monthly-transactions-i/) | [Monthly Transactions I](medium/03_1193_monthly-transactions-i.md) | CASE WHEN / Conditional Aggregation |
| 04 | [1174](https://leetcode.com/problems/immediate-food-delivery-ii/) | [Immediate Food Delivery II](medium/04_1174_immediate-food-delivery-ii.md) | Subquery / MIN / Conditional AVG |
| 05 | [550](https://leetcode.com/problems/game-play-analysis-iv/) | [Game Play Analysis IV](medium/05_550_game-play-analysis-iv.md) | DATE_ADD / Subquery / COUNT |
| 06 | [1070](https://leetcode.com/problems/product-sales-analysis-iii/) | [Product Sales Analysis III](medium/06_1070_product-sales-analysis-iii.md) | Subquery / IN with Tuple / MIN |
| 07 | [1045](https://leetcode.com/problems/customers-who-bought-all-products/) | [Customers Who Bought All Products](medium/07_1045_customers-who-bought-all-products.md) | GROUP BY / COUNT DISTINCT vs Scalar Subquery |
| 08 | [180](https://leetcode.com/problems/consecutive-numbers/) | [Consecutive Numbers](medium/08_180_consecutive-numbers.md) | Self JOIN / 3-way Join |
| 09 | [1164](https://leetcode.com/problems/product-price-at-a-given-date/) | [Product Price at a Given Date](medium/09_1164_product-price-at-a-given-date.md) | Subquery / UNION / Date Filtering |
| 10 | [1204](https://leetcode.com/problems/last-person-to-fit-in-the-bus/) | [Last Person to Fit in the Bus](medium/10_1204_last-person-to-fit-in-the-bus.md) | Window Functions / Cumulative SUM |
| 11 | [1907](https://leetcode.com/problems/count-salary-categories/) | [Count Salary Categories](medium/11_1907_count-salary-categories.md) | UNION ALL / Conditional COUNT |
| 12 | [626](https://leetcode.com/problems/exchange-seats/) | [Exchange Seats](medium/12_626_exchange-seats.md) | CASE WHEN / MOD / COUNT |
| 13 | [1341](https://leetcode.com/problems/movie-rating/) | [Movie Rating](medium/13_1341_movie-rating.md) | UNION ALL / GROUP BY / ORDER BY / LIMIT |
| 14 | [1321](https://leetcode.com/problems/restaurant-growth/) | [Restaurant Growth](medium/14_1321_restaurant-growth.md) | Window Functions / Moving Average / CTE |
| 15 | [602](https://leetcode.com/problems/friend-requests-ii-who-has-the-most-friends/) | [Friend Requests II: Who Has the Most Friends](medium/15_602_friend-requests-ii-who-has-the-most-friends.md) | UNION ALL / GROUP BY |
| 16 | [585](https://leetcode.com/problems/investments-in-2016/) | [Investments in 2016](medium/16_585_investments-in-2016.md) | Subquery / IN / COUNT > 1 |
| 17 | [176](https://leetcode.com/problems/second-highest-salary/) | [Second Highest Salary](medium/17_176_second-highest-salary.md) | LIMIT+OFFSET / IFNULL / Subquery |

---

## 🔴 Hard — 1 Problem

| # | LC # | Problem | Topic |
|:---:|:---:|---------|-------|
| 01 | [185](https://leetcode.com/problems/department-top-three-salaries/) | [Department Top Three Salaries](hard/01_185_department-top-three-salaries.md) | DENSE_RANK / PARTITION BY / Subquery |

---

## 🧩 Concept Index

Jump straight to any SQL technique and see every problem that uses it.

<details>
<summary><b>🔗 JOIN & NULL Handling</b> — click to expand</summary>

| Technique | Problems |
|-----------|---------|
| `INNER JOIN` | [1068](easy/07_1068_product-sales-analysis-i.md) · [1075](easy/15_1075_project-employees-i.md) · [570](medium/01_570_managers-with-at-least-5-direct-reports.md) · [185](hard/01_185_department-top-three-salaries.md) |
| `LEFT JOIN` | [1378](easy/06_1378_replace-employee-id-with-the-unique-identifier.md) · [1581](easy/08_1581_customer-who-visited-but-did-not-make-any-transactions.md) · [577](easy/11_577_employee-bonus.md) · [1934](medium/02_1934_confirmation-rate.md) |
| `CROSS JOIN` | [1280](easy/12_1280_students-and-examinations.md) |
| Self JOIN | [197](easy/09_197_rising-temperature.md) · [1731](easy/23_1731_the-number-of-employees-which-report-to-each-employee.md) · [570](medium/01_570_managers-with-at-least-5-direct-reports.md) · [180](medium/08_180_consecutive-numbers.md) |
| NULL Handling (`IS NULL`, `IFNULL`, `COALESCE`) | [584](easy/02_584_find-customer-referee.md) · [577](easy/11_577_employee-bonus.md) · [1934](medium/02_1934_confirmation-rate.md) · [176](medium/17_176_second-highest-salary.md) |

</details>

<details>
<summary><b>📊 Aggregation & Grouping</b> — click to expand</summary>

| Technique | Problems |
|-----------|---------|
| `GROUP BY` + `HAVING` | [596](easy/20_596_classes-with-at-least-5-students.md) · [1581](easy/08_1581_customer-who-visited-but-did-not-make-any-transactions.md) · [570](medium/01_570_managers-with-at-least-5-direct-reports.md) · [1045](medium/07_1045_customers-who-bought-all-products.md) |
| `COUNT DISTINCT` | [2356](easy/18_2356_number-of-unique-subjects-taught-by-each-teacher.md) · [1729](easy/21_1729_find-followers-count.md) · [1141](easy/19_1141_user-activity-for-the-past-30-days-i.md) |
| `SUM(condition)` trick | [1934](medium/02_1934_confirmation-rate.md) · [1211](easy/17_1211_queries-quality-and-percentage.md) |
| Conditional aggregation (`CASE WHEN` inside `SUM/AVG`) | [1193](medium/03_1193_monthly-transactions-i.md) · [1251](easy/14_1251_average-selling-price.md) · [1174](medium/04_1174_immediate-food-delivery-ii.md) |

</details>

<details>
<summary><b>🪟 Window Functions</b> — click to expand</summary>

| Technique | Problems |
|-----------|---------|
| `DENSE_RANK() OVER (PARTITION BY ...)` | [185](hard/01_185_department-top-three-salaries.md) |
| Cumulative `SUM() OVER (ORDER BY ...)` | [1204](medium/10_1204_last-person-to-fit-in-the-bus.md) |
| Moving Average (`AVG OVER ROWS BETWEEN`) | [1321](medium/14_1321_restaurant-growth.md) |

</details>

<details>
<summary><b>🔀 Subqueries & Set Operations</b> — click to expand</summary>

| Technique | Problems |
|-----------|---------|
| Scalar subquery in `WHERE` | [619](easy/22_619_biggest-single-number.md) · [1978](easy/26_1978_employees-whose-manager-left-the-company.md) · [176](medium/17_176_second-highest-salary.md) |
| Correlated subquery / `IN` with tuple | [1070](medium/06_1070_product-sales-analysis-iii.md) · [585](medium/16_585_investments-in-2016.md) |
| `UNION ALL` | [1789](easy/24_1789_primary-department-for-each-employee.md) · [1907](medium/11_1907_count-salary-categories.md) · [1341](medium/13_1341_movie-rating.md) · [602](medium/15_602_friend-requests-ii-who-has-the-most-friends.md) |
| `UNION` (distinct) | [1164](medium/09_1164_product-price-at-a-given-date.md) |

</details>

<details>
<summary><b>🔡 String & Pattern Matching</b> — click to expand</summary>

| Technique | Problems |
|-----------|---------|
| `LENGTH()` vs `CHAR_LENGTH()` | [1683](easy/05_1683_invalid-tweets.md) |
| `UPPER()` / `LOWER()` / `SUBSTR()` / `CONCAT()` | [1667](easy/27_1667_fix-names-in-a-table.md) |
| `LIKE` pattern | [1527](easy/28_1527_patients-with-a-condition.md) |
| `REGEXP` | [1517](easy/32_1517_find-users-with-valid-e-mails.md) |
| `GROUP_CONCAT()` | [1484](easy/30_1484_group-sold-products-by-the-date.md) |

</details>

<details>
<summary><b>📅 Date Functions</b> — click to expand</summary>

| Technique | Problems |
|-----------|---------|
| `DATEDIFF()` | [197](easy/09_197_rising-temperature.md) |
| `DATE_ADD()` | [550](medium/05_550_game-play-analysis-iv.md) |
| `DATE_FORMAT()` / month filtering | [1193](medium/03_1193_monthly-transactions-i.md) · [1141](easy/19_1141_user-activity-for-the-past-30-days-i.md) |

</details>

<details>
<summary><b>💡 Conditional Logic</b> — click to expand</summary>

| Technique | Problems |
|-----------|---------|
| `CASE WHEN` | [1251](easy/14_1251_average-selling-price.md) · [610](easy/25_610_triangle-judgement.md) · [1193](medium/03_1193_monthly-transactions-i.md) · [626](medium/12_626_exchange-seats.md) |
| `IFNULL()` / `COALESCE()` | [1934](medium/02_1934_confirmation-rate.md) · [176](medium/17_176_second-highest-salary.md) |
| `DELETE` with Self JOIN | [196](easy/29_196_delete-duplicate-emails.md) |

</details>

---

## 🧠 SQL Quick-Reference Cheatsheet

The most commonly tested patterns — pulled from these 50 problems.

```sql
-- ✅ Safe NULL comparison (never use = NULL)
WHERE column IS NULL
WHERE column IS NOT NULL

-- ✅ LEFT JOIN to include non-matching rows
SELECT a.id, b.value
FROM TableA a
LEFT JOIN TableB b ON a.id = b.a_id
WHERE b.a_id IS NULL      -- rows in A with NO match in B

-- ✅ SUM(condition) trick — count rows matching a condition
SELECT SUM(status = 'confirmed') / COUNT(*) AS rate  -- MySQL boolean
FROM Orders

-- ✅ DENSE_RANK for top-N per group (no gaps on ties)
SELECT *
FROM (
  SELECT name, salary,
    DENSE_RANK() OVER (PARTITION BY dept ORDER BY salary DESC) AS rnk
  FROM Employee
) t
WHERE rnk <= 3

-- ✅ Moving average — last N rows inclusive
SELECT AVG(amount) OVER (
  ORDER BY visit_date
  ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
) AS moving_avg

-- ✅ UNION ALL to combine then aggregate (preserve duplicates)
SELECT id FROM TableA
UNION ALL
SELECT id FROM TableB

-- ✅ GROUP_CONCAT for comma-separated strings per group
SELECT sell_date, COUNT(DISTINCT product) AS num_sold,
  GROUP_CONCAT(DISTINCT product ORDER BY product) AS products
FROM Activities
GROUP BY sell_date

-- ✅ Second highest salary (handles NULL edge case)
SELECT IFNULL(
  (SELECT DISTINCT salary FROM Employee ORDER BY salary DESC LIMIT 1 OFFSET 1),
  NULL
) AS SecondHighestSalary

-- ✅ DELETE with self-join (avoid correlated subquery trap)
DELETE p1
FROM Person p1
JOIN Person p2 ON p1.email = p2.email AND p1.id > p2.id
```

---

## 📊 Progress

```
✅ Easy    ████████████████████████████████  32 / 32
✅ Medium  █████████████████                 17 / 17
✅ Hard    █                                  1 /  1
─────────────────────────────────────────────────────
   Total  ██████████████████████████████████ 50 / 50
```

---

## 🤝 Contributing

Found a better approach or a bug in my solution? PRs are welcome.

1. Fork the repo
2. Create a branch: `git checkout -b fix/problem-number`
3. Commit your change: `git commit -m "fix: improved approach for #1934"`
4. Open a pull request

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:24243e,50:302b63,100:0f0c29&height=120&section=footer" />

**If this helped you, a ⭐ keeps it alive.**

[![GitHub](https://img.shields.io/badge/GitHub-Rushit004-181717?style=flat-square&logo=github)](https://github.com/Rushit004)
[![LeetCode](https://img.shields.io/badge/LeetCode-Profile-FFA116?style=flat-square&logo=leetcode&logoColor=white)](https://leetcode.com/)

</div>
