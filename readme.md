![header](https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6&height=200&section=header&text=SQL%2050%20%E2%80%94%20LeetCode&fontSize=50&fontAlignY=35&desc=Solving%20%26%20Documenting%20All%2050%20SQL%20Problems&descAlignY=55&animation=fadeIn)

<h1 align="center">🗄️ SQL 50 — LeetCode</h1>

<p align="center"><i>A structured walkthrough of all 50 SQL problems — clean solutions, detailed approaches, and key takeaways for every problem.</i></p>

<p align="center">
  <img src="https://img.shields.io/badge/Language-MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white" />
  <img src="https://img.shields.io/badge/Platform-LeetCode-FFA116?style=flat-square&logo=leetcode&logoColor=black" />
  <img src="https://img.shields.io/badge/Problems-50-6D28D9?style=flat-square" />
  <img src="https://img.shields.io/badge/Easy-32-22C55E?style=flat-square" />
  <img src="https://img.shields.io/badge/Medium-17-F59E0B?style=flat-square" />
  <img src="https://img.shields.io/badge/Hard-1-EF4444?style=flat-square" />
</p>

---

<p align="center">
  <a href="#-about">About</a> &nbsp;•&nbsp;
  <a href="#-progress">Progress</a> &nbsp;•&nbsp;
  <a href="#-folder-structure">Structure</a> &nbsp;•&nbsp;
  <a href="#-problem-list">Problems</a> &nbsp;•&nbsp;
  <a href="#-topics-covered">Topics</a> &nbsp;•&nbsp;
  <a href="#-my-reflection">Reflection</a>
</p>

---

## 🧭 About

> **Who** — Rushit Tholiya , B.Tech CSE student at Nirma University, Ahmedabad.  
> **What** — A complete, well-documented solution set for the LeetCode SQL 50 study plan — covering Select, Joins, Aggregations, Subqueries, String Functions, and more.  
> **Why** — To build strong SQL fundamentals through consistent practice and maintain a clean, referenceable knowledge base for every concept encountered along the way.

---

## 📊 Progress

| Difficulty | Solved | Total | Completion |
|------------|--------|-------|------------|
| 🟢 Easy | 8 | 32 | 25% |
| 🟡 Medium | 2 | 17 | 12% |
| 🔴 Hard | 0 | 1 | 0% |
| **Total** | **10** | **50** | **20%** |

---

## 📁 Folder Structure

```
sql-50-leetcode/
├── easy/
│   ├── 584-find-customer-referee.md
│   ├── 595-big-countries.md
│   ├── 1148-article-views-i.md
│   └── ...
├── medium/
│   ├── 570-managers-with-at-least-5-direct-reports.md
│   ├── 1934-confirmation-rate.md
│   └── ...
├── hard/
│   └── 185-department-top-three-salaries.md
└── README.md
```

---

## 📋 Problem List

### 🟢 Easy — 8 / 32 Solved

| # | Problem | Topic | Status |
|---|---------|-------|--------|
| 196 | [Delete Duplicate Emails](./easy/196-delete-duplicate-emails.md) | DELETE / Self JOIN | ⬜ |
| 197 | [Rising Temperature](./easy/197-rising-temperature.md) | Self JOIN / DATEDIFF() | ✅ |
| 577 | [Employee Bonus](./easy/577-employee-bonus.md) | LEFT JOIN / NULL Handling | ✅ |
| 584 | [Find Customer Referee](./easy/584-find-customer-referee.md) | NULL Handling / Filtering | ✅ |
| 595 | [Big Countries](./easy/595-big-countries.md) | WHERE / Filtering | ✅ |
| 596 | [Classes More Than 5 Students](./easy/596-classes-more-than-5-students.md) | GROUP BY / HAVING | ⬜ |
| 610 | [Triangle Judgement](./easy/610-triangle-judgement.md) | CASE WHEN | ⬜ |
| 619 | [Biggest Single Number](./easy/619-biggest-single-number.md) | MAX() / Subquery | ⬜ |
| 620 | [Not Boring Movies](./easy/620-not-boring-movies.md) | WHERE / MOD() / ORDER BY | ⬜ |
| 1068 | [Product Sales Analysis I](./easy/1068-product-sales-analysis-i.md) | INNER JOIN | ✅ |
| 1075 | [Project Employees I](./easy/1075-project-employees-i.md) | AVG() / JOIN / GROUP BY | ⬜ |
| 1141 | [User Activity for the Past 30 Days I](./easy/1141-user-activity-for-the-past-30-days-i.md) | DATE Functions / GROUP BY | ⬜ |
| 1148 | [Article Views I](./easy/1148-article-views-i.md) | DISTINCT / Self-reference Filter | ✅ |
| 1211 | [Queries Quality and Percentage](./easy/1211-queries-quality-and-percentage.md) | AVG() / ROUND() / GROUP BY | ⬜ |
| 1251 | [Average Selling Price](./easy/1251-average-selling-price.md) | AVG() / JOIN / GROUP BY | ⬜ |
| 1280 | [Students and Examinations](./easy/1280-students-and-examinations.md) | LEFT JOIN / GROUP BY | ⬜ |
| 1327 | [List the Products Ordered in a Period](./easy/1327-list-the-products-ordered-in-a-period.md) | JOIN / GROUP BY / HAVING | ⬜ |
| 1378 | [Replace Employee ID With The Unique Identifier](./easy/1378-replace-employee-id-with-the-unique-identifier.md) | LEFT JOIN | ✅ |
| 1484 | [Group Sold Products By The Date](./easy/1484-group-sold-products-by-the-date.md) | GROUP_CONCAT() / GROUP BY | ⬜ |
| 1517 | [Find Users With Valid E-Mails](./easy/1517-find-users-with-valid-e-mails.md) | REGEXP | ⬜ |
| 1527 | [Patients With a Condition](./easy/1527-patients-with-a-condition.md) | LIKE / Pattern Matching | ⬜ |
| 1581 | [Customer Who Visited but Did Not Make Any Transactions](./easy/1581-customer-who-visited-but-did-not-make-any-transactions.md) | LEFT JOIN / Subquery | ⬜ |
| 1633 | [Percentage of Users Attended a Contest](./easy/1633-percentage-of-users-attended-a-contest.md) | COUNT() / GROUP BY | ⬜ |
| 1661 | [Average Time of Process per Machine](./easy/1661-average-time-of-process-per-machine.md) | AVG() / GROUP BY | ⬜ |
| 1667 | [Fix Names in a Table](./easy/1667-fix-names-in-a-table.md) | CONCAT() / UPPER() / LOWER() | ⬜ |
| 1683 | [Invalid Tweets](./easy/1683-invalid-tweets.md) | String Functions / LENGTH() | ✅ |
| 1729 | [Find Followers Count](./easy/1729-find-followers-count.md) | COUNT() / GROUP BY | ⬜ |
| 1731 | [The Number of Employees Which Report to Each Employee](./easy/1731-the-number-of-employees-which-report-to-each-employee.md) | Self JOIN / COUNT() | ⬜ |
| 1757 | [Recyclable and Low Fat Products](./easy/1757-recyclable-and-low-fat-products.md) | WHERE / Filtering | ⬜ |
| 1789 | [Primary Department for Each Employee](./easy/1789-primary-department-for-each-employee.md) | GROUP BY / HAVING / UNION | ⬜ |
| 1978 | [Employees Whose Manager Left the Company](./easy/1978-employees-whose-manager-left-the-company.md) | Subquery / IS NULL | ⬜ |
| 2356 | [Number of Unique Subjects Taught by Each Teacher](./easy/2356-number-of-unique-subjects-taught-by-each-teacher.md) | COUNT(DISTINCT) / GROUP BY | ⬜ |

---

### 🟡 Medium — 2 / 17 Solved

| # | Problem | Topic | Status |
|---|---------|-------|--------|
| 176 | [Second Highest Salary](./medium/176-second-highest-salary.md) | IFNULL() / Subquery / LIMIT | ⬜ |
| 180 | [Consecutive Numbers](./medium/180-consecutive-numbers.md) | Self JOIN / DISTINCT | ⬜ |
| 550 | [Game Play Analysis IV](./medium/550-game-play-analysis-iv.md) | DATE / Subquery / ROUND() | ⬜ |
| 570 | [Managers with at Least 5 Direct Reports](./medium/570-managers-with-at-least-5-direct-reports.md) | Self JOIN / GROUP BY / HAVING | ✅ |
| 585 | [Investments in 2016](./medium/585-investments-in-2016.md) | SUM() / Subquery / Grouping | ⬜ |
| 602 | [Friend Requests II: Who Has the Most Friends](./medium/602-friend-requests-ii-who-has-the-most-friends.md) | UNION / GROUP BY / COUNT() | ⬜ |
| 626 | [Exchange Seats](./medium/626-exchange-seats.md) | CASE WHEN / MOD() | ⬜ |
| 1045 | [Customers Who Bought All Products](./medium/1045-customers-who-bought-all-products.md) | GROUP BY / HAVING / COUNT(DISTINCT) | ⬜ |
| 1070 | [Product Sales Analysis III](./medium/1070-product-sales-analysis-iii.md) | Subquery / GROUP BY | ⬜ |
| 1164 | [Product Price at a Given Date](./medium/1164-product-price-at-a-given-date.md) | CASE WHEN / Subquery | ⬜ |
| 1174 | [Immediate Food Delivery II](./medium/1174-immediate-food-delivery-ii.md) | CASE WHEN / AVG() | ⬜ |
| 1193 | [Monthly Transactions I](./medium/1193-monthly-transactions-i.md) | GROUP BY / DATE_FORMAT() | ⬜ |
| 1204 | [Last Person to Fit in the Bus](./medium/1204-last-person-to-fit-in-the-bus.md) | Cumulative SUM / Subquery | ⬜ |
| 1321 | [Restaurant Growth](./medium/1321-restaurant-growth.md) | Window Functions / AVG() | ⬜ |
| 1341 | [Movie Rating](./medium/1341-movie-rating.md) | UNION / GROUP BY / LIMIT | ⬜ |
| 1907 | [Count Salary Categories](./medium/1907-count-salary-categories.md) | CASE WHEN / UNION | ⬜ |
| 1934 | [Confirmation Rate](./medium/1934-confirmation-rate.md) | LEFT JOIN / IFNULL() / ROUND() | ✅ |

---

### 🔴 Hard — 0 / 1 Solved

| # | Problem | Topic | Status |
|---|---------|-------|--------|
| 185 | [Department Top Three Salaries](./hard/185-department-top-three-salaries.md) | DENSE_RANK() / Window Functions | ⬜ |

---

## 🧠 Topics Covered

`SELECT` `WHERE` `Filtering` `NULL Handling` `IS NULL` `DISTINCT` `ORDER BY`  
`GROUP BY` `HAVING` `INNER JOIN` `LEFT JOIN` `Self JOIN`  
`COUNT()` `SUM()` `AVG()` `MAX()` `MIN()` `ROUND()` `IFNULL()`  
`CASE WHEN` `LENGTH()` `UPPER()` `LOWER()` `CONCAT()` `GROUP_CONCAT()`  
`DATEDIFF()` `DATE_FORMAT()` `MOD()` `REGEXP` `LIKE`  
`Subqueries` `Window Functions` `UNION` `DELETE` `Three-Valued Logic`

---

## ✍️ My Reflection

SQL has always felt like a language that rewards clear thinking more than clever syntax. This challenge pushed me to stop treating queries as one-liners and start thinking in layers — what data do I have, what shape do I need it in, and which tool gets me there cleanly. The NULL traps, the aggregation gotchas, and the self-join patterns were the moments that actually stuck. Every `.md` here is a note to my future self — not just *what* the answer is, but *why* it works.

---

![footer](https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6&height=100&section=footer)
