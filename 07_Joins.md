## 7. Joins in SQL

Joins are used to retrieve related data stored in multiple tables by matching columns, usually keys. They help combine rows based on relationships.

---

### 7.1 INNER JOIN – Matching Rows in Both Tables

* Returns **only rows with matching values** in both tables.
* If a row in one table has no matching row in the other, it **won’t appear** in the result.

**Syntax:**

```sql
SELECT columns
FROM table1
INNER JOIN table2 ON table1.key = table2.key;
```

**Example:**

```sql
SELECT Students.Name, Courses.CourseName
FROM Students
INNER JOIN Enrollments ON Students.ID = Enrollments.StudentID
INNER JOIN Courses ON Enrollments.CourseID = Courses.ID;
```

This returns students who are enrolled in courses along with course names.

---

### 7.2 LEFT JOIN (or LEFT OUTER JOIN) – All Rows from Left + Matches from Right

* Returns **all rows from the left table**, and matched rows from the right table.
* If no match is found in the right table, columns from the right table will be `NULL`.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2 ON table1.key = table2.key;
```

**Example:**

```sql
SELECT Students.Name, Enrollments.CourseID
FROM Students
LEFT JOIN Enrollments ON Students.ID = Enrollments.StudentID;
```

This returns all students, even those **not enrolled** in any course. For students without enrollments, `CourseID` will be `NULL`.

---

### 7.3 RIGHT JOIN (or RIGHT OUTER JOIN) – All Rows from Right + Matches from Left

* Returns **all rows from the right table**, and matched rows from the left table.
* If no match is found in the left table, columns from the left table will be `NULL`.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2 ON table1.key = table2.key;
```

**Example:**

```sql
SELECT Students.Name, Enrollments.CourseID
FROM Students
RIGHT JOIN Enrollments ON Students.ID = Enrollments.StudentID;
```

Returns all enrollments, including those without matching students (if any). Students columns will be `NULL` for unmatched rows.

---

### 7.4 FULL JOIN (or FULL OUTER JOIN) – All Rows from Both Sides

* Returns **all rows from both tables**.
* When there is a match, rows are combined.
* If no match, unmatched rows from either side have `NULL` for the other side’s columns.
* **Note:** MySQL doesn’t support `FULL JOIN` directly.

**Workaround in MySQL:**

Use `UNION` of `LEFT JOIN` and `RIGHT JOIN`:

```sql
SELECT *
FROM table1
LEFT JOIN table2 ON table1.key = table2.key

UNION

SELECT *
FROM table1
RIGHT JOIN table2 ON table1.key = table2.key;
```

---

### 7.5 CROSS JOIN – Cartesian Product

* Returns **all possible combinations** of rows from both tables.
* If table1 has `m` rows and table2 has `n` rows, result will have `m * n` rows.
* Use carefully, as it can produce large result sets.

**Syntax:**

```sql
SELECT *
FROM table1
CROSS JOIN table2;
```

**Example:**

```sql
SELECT Students.Name, Courses.CourseName
FROM Students
CROSS JOIN Courses;
```

Generates every possible combination of students and courses (useful for scenarios like creating all test combinations).

---

### 7.6 SELF JOIN – Join a Table with Itself

* The table is joined with itself to compare rows within the same table.
* Requires using **table aliases** to differentiate between the two instances.

**Syntax:**

```sql
SELECT A.column1, B.column2
FROM table A
JOIN table B ON A.key = B.key;
```

**Example:**

Find pairs of employees who work in the same department:

```sql
SELECT E1.Name AS Employee1, E2.Name AS Employee2, E1.Department
FROM Employees E1
JOIN Employees E2 ON E1.Department = E2.Department AND E1.ID != E2.ID;
```

Returns pairs of employees from the same department (excluding pairing with themselves).

---

### Summary Table

| Join Type  | Description                                  | Result                                                                                |
| ---------- | -------------------------------------------- | ------------------------------------------------------------------------------------- |
| INNER JOIN | Rows with matching keys in both tables       | Only matched rows                                                                     |
| LEFT JOIN  | All rows from left + matched rows from right | All rows in left table; right columns NULL if no match                                |
| RIGHT JOIN | All rows from right + matched rows from left | All rows in right table; left columns NULL if no match                                |
| FULL JOIN  | All rows from both tables                    | All matched + unmatched rows from both tables (MySQL uses UNION of LEFT & RIGHT JOIN) |
| CROSS JOIN | Cartesian product of rows                    | All combinations of rows from both tables                                             |
| SELF JOIN  | Table joined with itself                     | Compare or relate rows within same table using aliases                                |

---
