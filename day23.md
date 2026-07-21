# Daily Diary – Day 23
`Date : 18/7/26`
**Subject:** Data Analytics
##### **Topic Covered:** SQL Joins – INNER, LEFT, RIGHT, FULL OUTER, SELF, CROSS JOIN

---

## 1. What is a JOIN? (Brief Theory)
A **JOIN** combines rows from two or more tables based on a related column (usually a primary key – foreign key pair).

```
Table 1: students    → has student info
Table 2: courses     → has course info
Common column        → course_id (links both tables)
JOIN                 → gives combined result in one output
```

---

## 2. Sample Tables

**Table: `students`**
```
+----+----------+-----+-----------+
| id | name     | age | course_id |
+----+----------+-----+-----------+
| 1  | Bhawna   | 21  | 101       |
| 2  | Taman    | 22  | 102       |
| 3  | Ram      | 20  | 101       |
| 4  | Sham     | 23  | 103       |
| 5  | Gita     | 21  | NULL      |
+----+----------+-----+-----------+
```

**Table: `courses`**
```
+-----+-------------+----------+
| id  | course_name | duration |
+-----+-------------+----------+
| 101 | Python      | 3 months |
| 102 | Java        | 4 months |
| 103 | SQL         | 2 months |
| 104 | Power BI    | 1 month  |
+-----+-------------+----------+
```

---

## 3. INNER JOIN
**Returns only rows that have a match in BOTH tables.**

```sql
SELECT s.name, s.age, c.course_name, c.duration
FROM students s
INNER JOIN courses c ON s.course_id = c.id;
```

**Output:**
```
+--------+-----+-------------+----------+
| name   | age | course_name | duration |
+--------+-----+-------------+----------+
| Bhawna | 21  | Python      | 3 months |
| Taman  | 22  | Java        | 4 months |
| Ram    | 20  | Python      | 3 months |
| Sham   | 23  | SQL         | 2 months |
+--------+-----+-------------+----------+
→ Gita (NULL course_id) excluded
→ Power BI (no student enrolled) excluded
```

---

## 4. LEFT JOIN
**Returns ALL rows from the LEFT table + matched rows from RIGHT table. Unmatched right → NULL.**

```sql
SELECT s.name, s.age, c.course_name
FROM students s
LEFT JOIN courses c ON s.course_id = c.id;
```

**Output:**
```
+--------+-----+-------------+
| name   | age | course_name |
+--------+-----+-------------+
| Bhawna | 21  | Python      |
| Taman  | 22  | Java        |
| Ram    | 20  | Python      |
| Sham   | 23  | SQL         |
| Gita   | 21  | NULL        |  ← Gita included, no course match
+--------+-----+-------------+
→ Power BI not shown (not in left table)
```

---

## 5. RIGHT JOIN
**Returns ALL rows from the RIGHT table + matched rows from LEFT table. Unmatched left → NULL.**

```sql
SELECT s.name, c.course_name, c.duration
FROM students s
RIGHT JOIN courses c ON s.course_id = c.id;
```

**Output:**
```
+--------+-------------+----------+
| name   | course_name | duration |
+--------+-------------+----------+
| Bhawna | Python      | 3 months |
| Ram    | Python      | 3 months |
| Taman  | Java        | 4 months |
| Sham   | SQL         | 2 months |
| NULL   | Power BI    | 1 month  |  ← Power BI included, no student
+--------+-------------+----------+
→ Gita not shown (NULL course_id, not in right table)
```

---

## 6. FULL OUTER JOIN
**Returns ALL rows from BOTH tables. Unmatched rows on either side → NULL.**

```sql
-- MySQL doesn't support FULL OUTER JOIN directly
-- Use UNION of LEFT and RIGHT JOIN

SELECT s.name, c.course_name
FROM students s
LEFT JOIN courses c ON s.course_id = c.id

UNION

SELECT s.name, c.course_name
FROM students s
RIGHT JOIN courses c ON s.course_id = c.id;
```

**Output:**
```
+--------+-------------+
| name   | course_name |
+--------+-------------+
| Bhawna | Python      |
| Taman  | Java        |
| Ram    | Python      |
| Sham   | SQL         |
| Gita   | NULL        |  ← student with no course
| NULL   | Power BI    |  ← course with no student
+--------+-------------+
→ Everyone from both tables included
```

---

## 7. SELF JOIN
**A table joined with itself. Used to compare rows within the same table.**

```sql
-- Find students in the same city
SELECT a.name AS Student1, b.name AS Student2, a.age
FROM students a
JOIN students s ON a.age = b.age
WHERE a.id != b.id;
```

**Real use case – Employee & Manager (same table):**
```sql
-- employees table has emp_id, name, manager_id
SELECT e.name AS Employee, m.name AS Manager
FROM employees e
JOIN employees m ON e.manager_id = m.emp_id;
```

---

## 8. CROSS JOIN
**Returns every combination of rows from both tables (Cartesian product). No ON condition needed.**

```sql
SELECT s.name, c.course_name
FROM students s
CROSS JOIN courses c;

-- 5 students × 4 courses = 20 rows output
-- Useful for generating combinations
```

---

## 9. JOIN with WHERE, GROUP BY, ORDER BY

```sql
-- Students in Python course with marks > 80
SELECT s.name, s.marks, c.course_name
FROM students s
INNER JOIN courses c ON s.course_id = c.id
WHERE c.course_name = 'Python' AND s.marks > 80
ORDER BY s.marks DESC;

-- Count students per course
SELECT c.course_name, COUNT(s.id) AS total_students
FROM courses c
LEFT JOIN students s ON c.id = s.course_id
GROUP BY c.course_name
ORDER BY total_students DESC;

-- Average marks per course
SELECT c.course_name, AVG(s.marks) AS avg_marks
FROM students s
INNER JOIN courses c ON s.course_id = c.id
GROUP BY c.course_name
HAVING AVG(s.marks) > 70;
```

---

## 10. Joining 3 Tables

```sql
-- students → enrollments → courses
SELECT s.name, c.course_name, e.score
FROM students s
INNER JOIN enrollments e ON s.id = e.student_id
INNER JOIN courses c     ON e.course_id = c.id
ORDER BY e.score DESC;
```

---

## 11. Visual Summary of All JOINs

```
Table A (students)          Table B (courses)

    [A only] [A ∩ B] [B only]

INNER JOIN  →  only [A ∩ B]         (matched rows only)
LEFT JOIN   →  [A only] + [A ∩ B]   (all of A)
RIGHT JOIN  →  [A ∩ B] + [B only]   (all of B)
FULL OUTER  →  [A only]+[A∩B]+[B only] (everyone)
CROSS JOIN  →  A × B                (every combination)
SELF JOIN   →  A joined with A      (compare within table)
```

---

## 12. Quick Reference

| JOIN Type | Returns | NULL side |
|---|---|---|
| INNER JOIN | Only matching rows | None |
| LEFT JOIN | All left + matched right | Right side |
| RIGHT JOIN | All right + matched left | Left side |
| FULL OUTER | All rows from both | Both sides |
| CROSS JOIN | Every combination | None |
| SELF JOIN | Table with itself | Depends |

---

## Practice Queries – Solved

```sql
-- Q1. List all students with their course names (only enrolled)
SELECT s.name, c.course_name
FROM students s INNER JOIN courses c ON s.course_id = c.id;

-- Q2. List all students including those with no course
SELECT s.name, c.course_name
FROM students s LEFT JOIN courses c ON s.course_id = c.id;

-- Q3. List all courses including those with no students enrolled
SELECT s.name, c.course_name
FROM students s RIGHT JOIN courses c ON s.course_id = c.id;

-- Q4. Count how many students in each course
SELECT c.course_name, COUNT(s.id) AS students
FROM courses c
LEFT JOIN students s ON c.id = s.course_id
GROUP BY c.course_name;

-- Q5. Top course by average marks
SELECT c.course_name, AVG(s.marks) AS avg_marks
FROM students s
INNER JOIN courses c ON s.course_id = c.id
GROUP BY c.course_name
ORDER BY avg_marks DESC
LIMIT 1;
```

---

## Summary of Day 23
Today I learned all **SQL JOIN types** — `INNER JOIN` (only matching rows), `LEFT JOIN` (all left table rows), `RIGHT JOIN` (all right table rows), `FULL OUTER JOIN` (all rows from both — via UNION in MySQL), `SELF JOIN` (table with itself — for hierarchical data), and `CROSS JOIN` (cartesian product). I also combined JOINs with `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY`, and joined 3 tables in a single query.

**Practice Questions for Tomorrow:**
1. Write a LEFT JOIN to find all students who haven't enrolled in any course.
2. Use INNER JOIN across 3 tables — students, enrollments, and courses.
3. Find courses that have zero students using RIGHT JOIN + WHERE NULL.
4. Use SELF JOIN on an employees table to find each employee's manager name.
5. Count total students per course sorted by highest enrollment using LEFT JOIN + GROUP BY.