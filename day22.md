# Daily Diary – Day 22
`Date : 17/7/26`
**Subject:** Data Analytics
#### **Topic Covered:** SQL Commands – DDL (CREATE, ALTER, DROP, TRUNCATE, RENAME), DML (INSERT, UPDATE, DELETE), TCL (COMMIT, ROLLBACK), Constraints, CASE, Subqueries

---

## 1. Types of SQL Commands (Brief Theory)

SQL commands are divided into categories based on what they do:

```
┌─────────────────────────────────────────────────────────┐
│              SQL COMMAND TYPES                          │
├──────────┬──────────────────────────────────────────────┤
│  DDL     │ Data Definition Language                     │
│          │ CREATE, ALTER, DROP, TRUNCATE, RENAME        │
│          │ → defines structure of tables                │
├──────────┼──────────────────────────────────────────────┤
│  DML     │ Data Manipulation Language                   │
│          │ INSERT, UPDATE, DELETE, MERGE                │
│          │ → modifies data inside tables                │
├──────────┼──────────────────────────────────────────────┤
│  DQL     │ Data Query Language                          │
│          │ SELECT                                       │
│          │ → retrieves data from tables                 │
├──────────┼──────────────────────────────────────────────┤
│  TCL     │ Transaction Control Language                 │
│          │ COMMIT, ROLLBACK, SAVEPOINT                  │
│          │ → manages transactions                       │
├──────────┼──────────────────────────────────────────────┤
│  DCL     │ Data Control Language                        │
│          │ GRANT, REVOKE                                │
│          │ → controls user permissions                  │
└──────────┴──────────────────────────────────────────────┘
```

---

## 2. Sample Tables Used Today

**Table: `students`**
```
+----+----------+-----+--------+---------+--------+
| id | name     | age | city   | course  | marks  |
+----+----------+-----+--------+---------+--------+
| 1  | Bhawna   | 21  | Delhi  | Python  | 85     |
| 2  | Taman    | 22  | Mumbai | Java    | 72     |
| 3  | Ram      | 20  | Delhi  | Python  | 90     |
| 4  | Sham     | 23  | Kota   | SQL     | 45     |
| 5  | Gita     | 21  | Mumbai | Python  | 78     |
+----+----------+-----+--------+---------+--------+
```

---

## PART A – DDL COMMANDS

---

## 3. CREATE – Create Database & Table

```sql
-- Create a new database
CREATE DATABASE school;

-- Use the database
USE school;

-- Create a table with all data types
CREATE TABLE students (
    id       INT           PRIMARY KEY AUTO_INCREMENT,
    name     VARCHAR(50)   NOT NULL,
    age      INT           NOT NULL,
    city     VARCHAR(50)   DEFAULT 'Unknown',
    course   VARCHAR(50),
    marks    INT           CHECK (marks >= 0 AND marks <= 100),
    email    VARCHAR(100)  UNIQUE,
    joined   DATE          DEFAULT CURRENT_DATE
);
```

---

## 4. ALTER – Modify Existing Table Structure

**Theory:** `ALTER TABLE` is used to add, modify, rename, or drop columns and constraints in an existing table — without losing data.

### ADD a new column
```sql
-- Add a single column
ALTER TABLE students
ADD grade VARCHAR(5);

-- Add multiple columns
ALTER TABLE students
ADD phone   VARCHAR(15),
ADD address VARCHAR(100);
```

### MODIFY an existing column
```sql
-- Change data type of a column
ALTER TABLE students
MODIFY marks DECIMAL(5, 2);

-- Change data type and set NOT NULL
ALTER TABLE students
MODIFY name VARCHAR(100) NOT NULL;
```

### RENAME a column
```sql
-- Rename column (MySQL 8.0+)
ALTER TABLE students
RENAME COLUMN city TO location;
```

### DROP a column
```sql
-- Remove a column permanently
ALTER TABLE students
DROP COLUMN phone;
```

### ADD a constraint
```sql
-- Add a UNIQUE constraint on email
ALTER TABLE students
ADD CONSTRAINT unique_email UNIQUE (email);

-- Add a CHECK constraint
ALTER TABLE students
ADD CONSTRAINT check_marks CHECK (marks BETWEEN 0 AND 100);
```

### DROP a constraint
```sql
ALTER TABLE students
DROP CONSTRAINT check_marks;
```

---

## 5. RENAME – Rename Table

```sql
-- Rename a table
RENAME TABLE students TO learners;

-- OR using ALTER
ALTER TABLE students RENAME TO learners;
```

---

## 6. DROP – Delete Table or Database Permanently

**Theory:** `DROP` permanently deletes the table/database along with all its data and structure. Cannot be undone.

```sql
-- Drop a table (table + all data deleted forever)
DROP TABLE students;

-- Drop only if it exists (no error if table doesn't exist)
DROP TABLE IF EXISTS students;

-- Drop a database (all tables inside also deleted)
DROP DATABASE school;

-- Drop a database only if exists
DROP DATABASE IF EXISTS school;
```

---

## 7. TRUNCATE – Delete All Data (Keep Structure)

**Theory:** `TRUNCATE` removes all rows from a table but **keeps the table structure intact**. Faster than `DELETE` and cannot be rolled back.

```sql
-- Remove all data but keep table structure
TRUNCATE TABLE students;

-- After TRUNCATE:
SELECT * FROM students;  -- returns empty table, columns still exist
```

**Difference between DROP, DELETE, TRUNCATE:**
```
DROP     → Removes table structure + data (table gone completely)
TRUNCATE → Removes all data, table stays (faster, can't rollback)
DELETE   → Removes specific rows, table stays (can rollback, slower)
```

---

## PART B – DML COMMANDS

---

## 8. INSERT – Add New Data (Append Rows)

**Theory:** `INSERT INTO` adds new rows to a table. This is how you **append** new data.

### Insert single row
```sql
INSERT INTO students (name, age, city, course, marks)
VALUES ('Bhawna', 21, 'Delhi', 'Python', 85);
```

### Insert multiple rows (Append many at once)
```sql
INSERT INTO students (name, age, city, course, marks)
VALUES
    ('Taman',  22, 'Mumbai', 'Java',   72),
    ('Ram',    20, 'Delhi',  'Python', 90),
    ('Sham',   23, 'Kota',   'SQL',    45),
    ('Gita',   21, 'Mumbai', 'Python', 78),
    ('Rohan',  19, 'Delhi',  'SQL',    60);
```

### Insert with only some columns (others get default/NULL)
```sql
INSERT INTO students (name, marks)
VALUES ('Priya', 88);
-- age, city, course → NULL or default value
```

### Insert from another table (Copy + Append)
```sql
-- Append all rows from old_students into students
INSERT INTO students (name, age, city, course, marks)
SELECT name, age, city, course, marks
FROM old_students;

-- Append only Python students from old_students
INSERT INTO students (name, age, city, course, marks)
SELECT name, age, city, course, marks
FROM old_students
WHERE course = 'Python';
```

---

## 9. UPDATE – Modify Existing Data

**Theory:** `UPDATE` changes values in existing rows. Always use `WHERE` — without it, ALL rows get updated.

### Update a single column
```sql
-- Update marks for one student
UPDATE students
SET marks = 95
WHERE name = 'Ram';
```

### Update multiple columns at once
```sql
UPDATE students
SET marks = 80,
    city  = 'Chandigarh',
    course = 'Data Science'
WHERE id = 4;
```

### Update using a calculation
```sql
-- Add 5 bonus marks to all students
UPDATE students
SET marks = marks + 5;

-- Add 10 marks only to Python students
UPDATE students
SET marks = marks + 10
WHERE course = 'Python';

-- Cap marks at 100 if they exceed 100
UPDATE students
SET marks = 100
WHERE marks > 100;
```

### Update based on another column condition
```sql
-- If age is less than 20, set course to 'Foundation'
UPDATE students
SET course = 'Foundation'
WHERE age < 20;
```

### Update with CASE (Conditional Update)
```sql
-- Assign grade based on marks
UPDATE students
SET grade = CASE
    WHEN marks >= 85 THEN 'A'
    WHEN marks >= 70 THEN 'B'
    WHEN marks >= 55 THEN 'C'
    WHEN marks >= 33 THEN 'D'
    ELSE 'Fail'
END;
```

---

## 10. DELETE – Remove Specific Rows

**Theory:** `DELETE` removes specific rows based on a condition. Table structure stays. Can be rolled back inside a transaction.

### Delete specific row
```sql
-- Delete by name
DELETE FROM students WHERE name = 'Sham';

-- Delete by ID
DELETE FROM students WHERE id = 4;
```

### Delete with condition
```sql
-- Delete all failing students
DELETE FROM students WHERE marks < 33;

-- Delete students from Kota
DELETE FROM students WHERE city = 'Kota';

-- Delete students older than 22
DELETE FROM students WHERE age > 22;
```

### Delete with multiple conditions
```sql
-- Delete students in Java course with marks below 60
DELETE FROM students
WHERE course = 'Java' AND marks < 60;
```

### Delete ALL rows (same as TRUNCATE but slower, can rollback)
```sql
DELETE FROM students;
```

---

## 11. MERGE (UPSERT) – Insert or Update

**Theory:** `MERGE` inserts a row if it doesn't exist, or updates it if it does — very useful for syncing data.

```sql
-- MySQL equivalent using INSERT ... ON DUPLICATE KEY UPDATE
INSERT INTO students (id, name, age, city, course, marks)
VALUES (1, 'Bhawna', 21, 'Ludhiana', 'Python', 90)
ON DUPLICATE KEY UPDATE
    city  = VALUES(city),
    marks = VALUES(marks);

-- If id=1 exists → UPDATE city and marks
-- If id=1 doesn't exist → INSERT new row
```

---

## PART C – TCL COMMANDS

---

## 12. COMMIT – Save Changes Permanently

```sql
-- Start a transaction
START TRANSACTION;

-- Make changes
UPDATE students SET marks = marks + 5 WHERE course = 'Python';
DELETE FROM students WHERE marks < 33;

-- Save all changes permanently
COMMIT;
```

---

## 13. ROLLBACK – Undo Changes

**Theory:** `ROLLBACK` undoes all changes made since the last `COMMIT` or `START TRANSACTION`. Acts as an undo button.

```sql
START TRANSACTION;

-- Accidentally delete all students
DELETE FROM students;

-- Oops! Undo it before committing
ROLLBACK;

-- Data is restored ✓
SELECT * FROM students;
```

---

## 14. SAVEPOINT – Partial Rollback

```sql
START TRANSACTION;

UPDATE students SET marks = marks + 5;
SAVEPOINT after_marks_update;         -- save this point

DELETE FROM students WHERE city = 'Kota';
SAVEPOINT after_kota_delete;          -- save this point

-- Oops, wrong delete — rollback only to last savepoint
ROLLBACK TO after_marks_update;       -- undoes Kota delete, keeps marks update

COMMIT;
```

---

## 15. CASE Statement – Conditional Logic in SQL

**Theory:** `CASE` works like `if-else` inside SQL queries — returns different values based on conditions.

```sql
-- Use CASE in SELECT
SELECT name, marks,
    CASE
        WHEN marks >= 85 THEN 'A'
        WHEN marks >= 70 THEN 'B'
        WHEN marks >= 55 THEN 'C'
        WHEN marks >= 33 THEN 'D'
        ELSE 'Fail'
    END AS grade
FROM students;

-- CASE for city label
SELECT name, city,
    CASE city
        WHEN 'Delhi'  THEN 'Capital'
        WHEN 'Mumbai' THEN 'Financial Hub'
        ELSE 'Other City'
    END AS city_type
FROM students;

-- CASE inside GROUP BY aggregation
SELECT
    CASE
        WHEN marks >= 60 THEN 'Pass'
        ELSE 'Fail'
    END AS result,
    COUNT(*) AS total_students
FROM students
GROUP BY result;
```

---

## 16. Subquery – Query Inside a Query

**Theory:** A **subquery** is a SELECT statement nested inside another query. The inner query runs first, its result is used by the outer query.

```sql
-- Students with marks above average
SELECT name, marks
FROM students
WHERE marks > (SELECT AVG(marks) FROM students);

-- Student with highest marks
SELECT name, marks
FROM students
WHERE marks = (SELECT MAX(marks) FROM students);

-- Students from the same city as Bhawna
SELECT name, city
FROM students
WHERE city = (SELECT city FROM students WHERE name = 'Bhawna');

-- Students NOT in the most popular course
SELECT name, course
FROM students
WHERE course NOT IN (
    SELECT course
    FROM students
    GROUP BY course
    ORDER BY COUNT(*) DESC
    LIMIT 1
);

-- Subquery in FROM (inline view)
SELECT avg_data.course, avg_data.avg_marks
FROM (
    SELECT course, AVG(marks) AS avg_marks
    FROM students
    GROUP BY course
) AS avg_data
WHERE avg_data.avg_marks > 70;
```

---

## 17. Constraints – Rules on Columns

```sql
CREATE TABLE students (
    id      INT           PRIMARY KEY,          -- unique + not null
    name    VARCHAR(50)   NOT NULL,              -- cannot be empty
    email   VARCHAR(100)  UNIQUE,                -- no duplicates
    marks   INT           CHECK (marks >= 0 AND marks <= 100),  -- valid range
    city    VARCHAR(50)   DEFAULT 'Unknown',     -- default if not provided
    dept_id INT           REFERENCES departments(id)  -- foreign key
);
```

| Constraint | Purpose |
|---|---|
| `PRIMARY KEY` | Uniquely identifies each row |
| `NOT NULL` | Column cannot be empty |
| `UNIQUE` | No duplicate values allowed |
| `CHECK` | Value must meet a condition |
| `DEFAULT` | Auto-fills value if none provided |
| `FOREIGN KEY` | Links to primary key of another table |

---

## 18. Practice Queries – Solved

```sql
-- Q1. Add a 'grade' column to students table
ALTER TABLE students ADD grade VARCHAR(5);

-- Q2. Update grade based on marks using CASE
UPDATE students
SET grade = CASE
    WHEN marks >= 85 THEN 'A'
    WHEN marks >= 70 THEN 'B'
    WHEN marks >= 55 THEN 'C'
    WHEN marks >= 33 THEN 'D'
    ELSE 'Fail'
END;

-- Q3. Append 3 new students into the table
INSERT INTO students (name, age, city, course, marks)
VALUES
    ('Anita', 21, 'Jaipur',  'SQL',    76),
    ('Vikas', 23, 'Delhi',   'Python', 92),
    ('Simran',20, 'Amritsar','Java',   65);

-- Q4. Give 5 bonus marks to all Python students
UPDATE students
SET marks = marks + 5
WHERE course = 'Python';

-- Q5. Delete all students who failed (marks < 33)
DELETE FROM students WHERE marks < 33;

-- Q6. Find students scoring above average marks
SELECT name, marks FROM students
WHERE marks > (SELECT AVG(marks) FROM students)
ORDER BY marks DESC;

-- Q7. Show each student's grade using CASE in SELECT
SELECT name, marks,
    CASE
        WHEN marks >= 85 THEN 'A'
        WHEN marks >= 70 THEN 'B'
        WHEN marks >= 55 THEN 'C'
        WHEN marks >= 33 THEN 'D'
        ELSE 'Fail'
    END AS grade
FROM students;

-- Q8. Remove the phone column added earlier
ALTER TABLE students DROP COLUMN phone;

-- Q9. Rename the students table to learners
RENAME TABLE students TO learners;

-- Q10. Use transaction to safely update and rollback if wrong
START TRANSACTION;
UPDATE students SET marks = 0 WHERE course = 'SQL';
-- Check result
SELECT * FROM students;
-- Oops, wrong! Undo it
ROLLBACK;
```

---

## 19. Quick Reference Table

| Command | Type | Purpose |
|---|---|---|
| `CREATE` | DDL | Create database/table |
| `ALTER` | DDL | Modify table structure |
| `RENAME` | DDL | Rename table/column |
| `DROP` | DDL | Delete table/database permanently |
| `TRUNCATE` | DDL | Delete all rows, keep structure |
| `INSERT` | DML | Add new rows (append) |
| `UPDATE` | DML | Modify existing rows |
| `DELETE` | DML | Remove specific rows |
| `MERGE` | DML | Insert or update (upsert) |
| `SELECT` | DQL | Retrieve data |
| `COMMIT` | TCL | Save changes permanently |
| `ROLLBACK` | TCL | Undo changes |
| `SAVEPOINT` | TCL | Mark a rollback point |
| `CASE` | — | Conditional logic in query |
| Subquery | — | Query inside a query |

---

## Summary of Day 22
Today I learned all major **SQL command types** — **DDL** (CREATE, ALTER with add/modify/rename/drop column, RENAME, DROP, TRUNCATE), **DML** (INSERT for appending single/multiple/copied rows, UPDATE with calculations and CASE, DELETE with conditions, MERGE/upsert), and **TCL** (COMMIT, ROLLBACK, SAVEPOINT for transaction control). I also learned **CASE** for conditional logic inside queries, **Subqueries** (query inside a query — in WHERE, FROM, SELECT), and all 6 **SQL Constraints** (PRIMARY KEY, NOT NULL, UNIQUE, CHECK, DEFAULT, FOREIGN KEY). Solved 10 practice queries combining all commands.

**Practice Questions for Tomorrow:**
1. Add a `salary` column to an employees table and update it based on department using CASE.
2. Write a query to copy all rows from `orders_2023` into `orders_all` using INSERT SELECT.
3. Use a subquery to find the city with the highest average marks.
4. Use SAVEPOINT to update marks, then rollback only that update while keeping a delete.
5. Write a MERGE/upsert to insert a student if not exists, or update marks if they do exist.