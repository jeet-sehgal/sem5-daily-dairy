# Daily Diary – Day 21
`Date : 16/7/26`
**Subject:** Data Analytics
#### **Topic Covered:** SQL Basics – Database, Tables, SELECT, WHERE, ORDER BY, LIMIT, DISTINCT, Aggregate Functions, GROUP BY, HAVING

---

## 1. What is SQL? (Brief Theory)
**SQL (Structured Query Language)** is a standard language used to **store, manage, and retrieve data** from a relational database. Every company that stores data uses SQL — it is the most important skill in data analytics.

```
SQL is used to:
  ✅ Create tables and databases
  ✅ Insert, update, delete data
  ✅ Retrieve and filter data
  ✅ Aggregate and summarize data
  ✅ Join multiple tables together
```

**Popular SQL Databases:**
| Database | Used By |
|---|---|
| MySQL | Web apps, startups |
| PostgreSQL | Data engineering |
| SQLite | Local/offline apps |
| MS SQL Server | Enterprise |
| BigQuery | Google Cloud |
| Snowflake | Data warehouses |

---

## 2. Key Terms

```
Database  → A container that holds multiple tables
Table     → Rows and columns (like an Excel sheet)
Row       → One record (one student, one order)
Column    → One attribute (Name, Age, Marks)
Primary Key → Unique identifier for each row (e.g., Student_ID)
Query     → A SQL command/question asked to the database
```

---

## 3. Sample Table Used Today

**Table Name: `students`**

```
+----+----------+-----+--------+---------+--------+
| id | name     | age | city   | course  | marks  |
+----+----------+-----+--------+---------+--------+
| 1  | Bhawna   | 21  | Delhi  | Python  | 85     |
| 2  | Taman    | 22  | Mumbai | Java    | 72     |
| 3  | Ram      | 20  | Delhi  | Python  | 90     |
| 4  | Sham     | 23  | Kota   | SQL     | 45     |
| 5  | Gita     | 21  | Mumbai | Python  | 78     |
| 6  | Rohan    | 19  | Delhi  | SQL     | 60     |
| 7  | Priya    | 20  | Kota   | Java    | 88     |
| 8  | Neha     | 22  | Delhi  | SQL     | 33     |
+----+----------+-----+--------+---------+--------+
```

---

## 4. CREATE DATABASE & TABLE

```sql
-- Create a database
CREATE DATABASE school;

-- Use the database
USE school;

-- Create a table
CREATE TABLE students (
    id      INT PRIMARY KEY AUTO_INCREMENT,
    name    VARCHAR(50),
    age     INT,
    city    VARCHAR(50),
    course  VARCHAR(50),
    marks   INT
);
```

---

## 5. INSERT Data

```sql
-- Insert one row
INSERT INTO students (name, age, city, course, marks)
VALUES ('Bhawna', 21, 'Delhi', 'Python', 85);

-- Insert multiple rows
INSERT INTO students (name, age, city, course, marks)
VALUES
    ('Taman',  22, 'Mumbai', 'Java',   72),
    ('Ram',    20, 'Delhi',  'Python', 90),
    ('Sham',   23, 'Kota',   'SQL',    45),
    ('Gita',   21, 'Mumbai', 'Python', 78),
    ('Rohan',  19, 'Delhi',  'SQL',    60),
    ('Priya',  20, 'Kota',   'Java',   88),
    ('Neha',   22, 'Delhi',  'SQL',    33);
```

---

## 6. SELECT – Retrieve Data

```sql
-- Select all columns
SELECT * FROM students;

-- Select specific columns
SELECT name, marks FROM students;

-- Select with column alias (rename in output)
SELECT name AS "Student Name", marks AS "Score"
FROM students;

-- Select with calculation
SELECT name, marks, marks + 5 AS "Bonus Marks"
FROM students;
```

---

## 7. DISTINCT – Remove Duplicates

```sql
-- See all unique cities
SELECT DISTINCT city FROM students;

-- Count unique cities
SELECT COUNT(DISTINCT city) FROM students;

-- Unique course names
SELECT DISTINCT course FROM students;
```

---

## 8. WHERE – Filter Rows

```sql
-- Single condition
SELECT * FROM students WHERE city = 'Delhi';

SELECT * FROM students WHERE marks >= 75;

SELECT * FROM students WHERE course = 'Python';

-- Multiple conditions (AND)
SELECT * FROM students
WHERE city = 'Delhi' AND marks >= 75;

-- Multiple conditions (OR)
SELECT * FROM students
WHERE city = 'Delhi' OR city = 'Mumbai';

-- NOT condition
SELECT * FROM students
WHERE NOT course = 'SQL';

-- BETWEEN (range)
SELECT * FROM students
WHERE marks BETWEEN 60 AND 90;

-- IN (multiple values in one column)
SELECT * FROM students
WHERE city IN ('Delhi', 'Mumbai');

-- NOT IN
SELECT * FROM students
WHERE course NOT IN ('SQL', 'Java');

-- LIKE (pattern matching)
SELECT * FROM students WHERE name LIKE 'B%';    -- starts with B
SELECT * FROM students WHERE name LIKE '%a';    -- ends with a
SELECT * FROM students WHERE name LIKE '%am%';  -- contains am
SELECT * FROM students WHERE name LIKE '_ama%'; -- 2nd char is a
```

---

## 9. ORDER BY – Sort Results

```sql
-- Sort ascending (default)
SELECT * FROM students ORDER BY marks;

-- Sort descending
SELECT * FROM students ORDER BY marks DESC;

-- Sort by name A-Z
SELECT * FROM students ORDER BY name ASC;

-- Sort by multiple columns
-- First by city A-Z, then marks highest first
SELECT * FROM students
ORDER BY city ASC, marks DESC;
```

---

## 10. LIMIT – Restrict Number of Rows

```sql
-- Show only first 3 rows
SELECT * FROM students LIMIT 3;

-- Top 3 students by marks
SELECT * FROM students
ORDER BY marks DESC
LIMIT 3;

-- Skip first 2, show next 3 (OFFSET)
SELECT * FROM students
ORDER BY marks DESC
LIMIT 3 OFFSET 2;
```

---

## 11. Aggregate Functions

**Theory:** Aggregate functions perform calculations on a set of rows and return a single value.

| Function | Purpose |
|---|---|
| `COUNT()` | Count number of rows |
| `SUM()` | Total of a numeric column |
| `AVG()` | Average of a numeric column |
| `MAX()` | Highest value |
| `MIN()` | Lowest value |

```sql
-- Count total students
SELECT COUNT(*) AS Total_Students FROM students;

-- Count students in Delhi
SELECT COUNT(*) FROM students WHERE city = 'Delhi';

-- Total marks of all students
SELECT SUM(marks) AS Total_Marks FROM students;

-- Average marks
SELECT AVG(marks) AS Avg_Marks FROM students;

-- Highest marks
SELECT MAX(marks) AS Highest FROM students;

-- Lowest marks
SELECT MIN(marks) AS Lowest FROM students;

-- All in one query
SELECT
    COUNT(*)     AS Total_Students,
    SUM(marks)   AS Total_Marks,
    AVG(marks)   AS Avg_Marks,
    MAX(marks)   AS Highest,
    MIN(marks)   AS Lowest
FROM students;
```

---

## 12. GROUP BY – Group & Aggregate

**Theory:** `GROUP BY` groups rows with the same value in a column and applies aggregate functions to each group — like `groupby()` in Pandas.

```sql
-- Count students per city
SELECT city, COUNT(*) AS Total_Students
FROM students
GROUP BY city;

-- Average marks per course
SELECT course, AVG(marks) AS Avg_Marks
FROM students
GROUP BY course;

-- Total students and avg marks per city
SELECT city,
       COUNT(*) AS Students,
       AVG(marks) AS Avg_Marks,
       MAX(marks) AS Top_Score
FROM students
GROUP BY city
ORDER BY Avg_Marks DESC;

-- Count students per course per city
SELECT course, city, COUNT(*) AS Students
FROM students
GROUP BY course, city
ORDER BY course;
```

---

## 13. HAVING – Filter After GROUP BY

**Theory:** `WHERE` filters rows **before** grouping. `HAVING` filters groups **after** `GROUP BY`. You cannot use aggregate functions in `WHERE` — use `HAVING` instead.

```sql
-- Cities with more than 2 students
SELECT city, COUNT(*) AS Total
FROM students
GROUP BY city
HAVING COUNT(*) > 2;

-- Courses where avg marks > 70
SELECT course, AVG(marks) AS Avg_Marks
FROM students
GROUP BY course
HAVING AVG(marks) > 70;

-- Cities where total marks > 200
SELECT city, SUM(marks) AS Total_Marks
FROM students
GROUP BY city
HAVING SUM(marks) > 200;
```

---

## 14. UPDATE & DELETE

```sql
-- Update a single value
UPDATE students
SET marks = 95
WHERE name = 'Ram';

-- Update multiple columns
UPDATE students
SET marks = 80, city = 'Chandigarh'
WHERE id = 4;

-- Delete a specific row
DELETE FROM students
WHERE name = 'Neha';

-- Delete all rows (table stays, data gone)
DELETE FROM students;
```

---

## 15. SQL Query Execution Order

**Theory:** SQL does NOT execute in the order you write it. Knowing this helps debug errors.

```
Order of Execution:
1. FROM       → which table
2. WHERE      → filter rows
3. GROUP BY   → group the filtered rows
4. HAVING     → filter the groups
5. SELECT     → pick columns & aggregates
6. ORDER BY   → sort the result
7. LIMIT      → restrict output rows

Writing order vs Execution order:
  You write  → SELECT ... FROM ... WHERE ... GROUP BY ... HAVING ... ORDER BY ... LIMIT
  SQL runs   → FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT
```

---

## 16. Practice Queries – Solved

```sql
-- Q1. Show all students from Delhi
SELECT * FROM students WHERE city = 'Delhi';

-- Q2. Show top 3 students by marks
SELECT name, marks FROM students
ORDER BY marks DESC LIMIT 3;

-- Q3. Count students in each course
SELECT course, COUNT(*) AS Total
FROM students GROUP BY course;

-- Q4. Average marks per city, sorted highest first
SELECT city, AVG(marks) AS Avg_Marks
FROM students
GROUP BY city
ORDER BY Avg_Marks DESC;

-- Q5. Students who scored between 60 and 90
SELECT name, marks FROM students
WHERE marks BETWEEN 60 AND 90;

-- Q6. Cities with more than 1 student
SELECT city, COUNT(*) AS Students
FROM students
GROUP BY city
HAVING COUNT(*) > 1;

-- Q7. Show all Python students sorted by marks descending
SELECT name, marks FROM students
WHERE course = 'Python'
ORDER BY marks DESC;

-- Q8. Find highest and lowest marks in each course
SELECT course, MAX(marks) AS Highest, MIN(marks) AS Lowest
FROM students
GROUP BY course;

-- Q9. Names of students whose name starts with 'B' or 'R'
SELECT name FROM students
WHERE name LIKE 'B%' OR name LIKE 'R%';

-- Q10. Count distinct cities in the table
SELECT COUNT(DISTINCT city) AS Unique_Cities FROM students;
```

---

## 17. Quick Reference – SQL Clauses

| Clause | Purpose | Example |
|---|---|---|
| `SELECT` | Pick columns | `SELECT name, marks` |
| `FROM` | Source table | `FROM students` |
| `WHERE` | Filter rows | `WHERE marks > 60` |
| `DISTINCT` | Unique values | `SELECT DISTINCT city` |
| `ORDER BY` | Sort results | `ORDER BY marks DESC` |
| `LIMIT` | Restrict rows | `LIMIT 5` |
| `GROUP BY` | Group rows | `GROUP BY course` |
| `HAVING` | Filter groups | `HAVING COUNT(*) > 2` |
| `COUNT()` | Count rows | `COUNT(*)` |
| `SUM()` | Total | `SUM(marks)` |
| `AVG()` | Average | `AVG(marks)` |
| `MAX()` | Maximum | `MAX(marks)` |
| `MIN()` | Minimum | `MIN(marks)` |
| `LIKE` | Pattern match | `LIKE 'B%'` |
| `IN` | Multiple values | `IN ('Delhi','Mumbai')` |
| `BETWEEN` | Range filter | `BETWEEN 60 AND 90` |

---

## Summary of Day 21
Today I learned **SQL Basics** — the foundation of data analytics. I covered creating databases and tables, inserting data, and all core SQL clauses — `SELECT` (with aliases and calculations), `DISTINCT` (unique values), `WHERE` (with AND/OR/NOT/BETWEEN/IN/LIKE), `ORDER BY` (ASC/DESC, multiple columns), `LIMIT` with `OFFSET`, all **5 aggregate functions** (`COUNT`, `SUM`, `AVG`, `MAX`, `MIN`), `GROUP BY` (grouping with aggregation), and `HAVING` (filtering groups). I also practiced `UPDATE` and `DELETE` and solved 10 practice queries on a students table.

**Practice Questions for Tomorrow:**
1. Write a query to find the 2nd highest marks in the students table.
2. List all courses with more than 2 students enrolled.
3. Find students whose marks are above the average marks of all students.
4. Show each city with its student count and average marks, only for cities where avg > 65.
5. Find all students whose name contains the letter 'a' and sorted by marks descending.