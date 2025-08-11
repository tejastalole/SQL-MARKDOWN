## 8. Subqueries in SQL

A **subquery** is a query nested inside another SQL query. It can be used in various clauses like `SELECT`, `WHERE`, or `FROM`. Subqueries allow you to perform operations step-by-step, filtering or calculating data inside the main query.

---

### 8.1 Single-row Subquery

* Returns **one value** (one row, one column).
* Used when the subquery result is a single scalar value.
* Typically used with comparison operators like `=`, `<`, `>`, `<=`, `>=`.

**Example:**

Find students whose age equals the maximum age in the table:

```sql
SELECT Name, Age
FROM Students
WHERE Age = (SELECT MAX(Age) FROM Students);
```

The subquery `(SELECT MAX(Age) FROM Students)` returns a single value (the highest age), which is compared with the Age in the main query.

---

### 8.2 Multi-row Subquery

* Returns **multiple values** (multiple rows, usually one column).
* Used with operators that accept lists like `IN`, `NOT IN`.
* Cannot be used with single-value comparison operators directly.

**Example:**

Find students enrolled in courses with IDs 1, 2, or 3 (assuming CourseID is stored in Enrollments):

```sql
SELECT Name FROM Students
WHERE ID IN (SELECT StudentID FROM Enrollments WHERE CourseID IN (1, 2, 3));
```

The subquery returns multiple `StudentID`s who are enrolled in those courses.

---

### 8.3 EXISTS / NOT EXISTS

* Tests whether the subquery **returns any rows**.
* Returns `TRUE` if subquery returns one or more rows, else `FALSE`.
* Often used for checking the existence of related data.
* Efficient because it stops searching as soon as it finds a matching row.

**Syntax:**

```sql
SELECT columns
FROM table
WHERE EXISTS (subquery);
```

**Example:**

Find students who are enrolled in any course:

```sql
SELECT Name FROM Students S
WHERE EXISTS (
  SELECT 1 FROM Enrollments E WHERE E.StudentID = S.ID
);
```

* The subquery checks for enrollment rows matching each student.
* If at least one enrollment exists, the student is included.

**NOT EXISTS** works oppositely — it selects rows where the subquery returns no rows.

---

### 8.4 IN / NOT IN with Subqueries

* Checks if a value matches **any value in the subquery result**.
* `IN` includes rows where the value matches any returned by the subquery.
* `NOT IN` excludes rows where the value matches any returned by the subquery.

**Example:**

Find students **not enrolled** in any course:

```sql
SELECT Name FROM Students
WHERE ID NOT IN (SELECT StudentID FROM Enrollments);
```

---

### 8.5 Correlated Subqueries

* The subquery depends on the outer query for its values.
* Executed **once per row** of the outer query.
* Can be slower for large datasets but useful for complex filtering.

**Syntax:**

```sql
SELECT columns
FROM table1 outer
WHERE column OPERATOR (SELECT column FROM table2 inner WHERE inner.key = outer.key);
```

**Example:**

Find students whose age is greater than the average age of their department:

```sql
SELECT Name, Age, Department
FROM Students S1
WHERE Age > (
  SELECT AVG(Age)
  FROM Students S2
  WHERE S2.Department = S1.Department
);
```

* The subquery calculates average age for the department of each outer row.
* The outer query compares each student’s age with their department’s average.

---

### Summary Table

| Subquery Type       | Returns              | Used With          | Example Use Case                                |
| ------------------- | -------------------- | ------------------ | ----------------------------------------------- |
| Single-row subquery | One value            | =, <, >, <=, >=    | Find students with max age                      |
| Multi-row subquery  | Multiple values      | IN, NOT IN         | Find students enrolled in certain courses       |
| EXISTS / NOT EXISTS | Boolean (true/false) | EXISTS, NOT EXISTS | Find students who have enrollments              |
| Correlated subquery | Depends on outer row | Any operator       | Compare each row with aggregated data per group |

---
