## 15. Advanced SQL Concepts

---

### 15.1 Normalization

Normalization is a process of organizing data in a database to reduce **redundancy** and improve **data integrity**. It divides large tables into smaller, related tables.

#### Normal Forms:

* **1NF (First Normal Form):**

  * Each column contains atomic (indivisible) values.
  * Each record is unique.
  * No repeating groups or arrays.

* **2NF (Second Normal Form):**

  * Must be in 1NF.
  * All non-key columns are fully functionally dependent on the entire primary key (no partial dependency).
  * Applies to tables with composite primary keys.

* **3NF (Third Normal Form):**

  * Must be in 2NF.
  * No transitive dependency: non-key columns depend only on the primary key, not other non-key columns.

* **BCNF (Boyce-Codd Normal Form):**

  * Stronger version of 3NF.
  * Every determinant is a candidate key.
  * Deals with certain anomalies not covered by 3NF.

---

### 15.2 Denormalization

* The opposite of normalization.
* Intentionally adds **redundancy** to improve **read performance** by reducing the number of joins.
* Used in scenarios like data warehouses or reporting where read speed is critical.
* Increases storage and potential for data anomalies.

---

### 15.3 Window Functions

Window functions perform calculations across a set of table rows related to the current row, **without collapsing the rows** like aggregate functions.

| Function          | Description                              | Example                                    |
| ----------------- | ---------------------------------------- | ------------------------------------------ |
| **ROW\_NUMBER()** | Assigns unique sequential number to rows | `ROW_NUMBER() OVER (ORDER BY Salary DESC)` |
| **RANK()**        | Assigns rank with gaps for ties          | `RANK() OVER (ORDER BY Score DESC)`        |
| **LEAD()**        | Accesses next row’s value                | `LEAD(Salary) OVER (ORDER BY EmployeeID)`  |
| **LAG()**         | Accesses previous row’s value            | `LAG(Salary) OVER (ORDER BY EmployeeID)`   |

**Example:**

```sql
SELECT Name, Salary,
       ROW_NUMBER() OVER (ORDER BY Salary DESC) AS RowNum,
       LAG(Salary) OVER (ORDER BY Salary DESC) AS PrevSalary
FROM Employees;
```

---

### 15.4 CTE (Common Table Expressions) – WITH Clause

* Temporary named result set for use within a query.
* Improves readability and modularity of complex queries.
* Defined using `WITH` clause.

**Syntax:**

```sql
WITH cte_name AS (
  SELECT ...
)
SELECT * FROM cte_name WHERE ...;
```

**Example:**

```sql
WITH DeptAvg AS (
  SELECT Department, AVG(Salary) AS AvgSalary
  FROM Employees
  GROUP BY Department
)
SELECT Name, Department, Salary
FROM Employees E
JOIN DeptAvg D ON E.Department = D.Department
WHERE Salary > AvgSalary;
```

---

### 15.5 UNION vs UNION ALL

| Operator      | Description                                      | Removes Duplicates? | Use Case                            |
| ------------- | ------------------------------------------------ | ------------------- | ----------------------------------- |
| **UNION**     | Combines result sets and removes duplicates      | Yes                 | When you want unique combined rows  |
| **UNION ALL** | Combines result sets without removing duplicates | No                  | Faster, when duplicates are allowed |

---

### 15.6 OFFSET for Pagination

* Used with `LIMIT` to skip a number of rows in result set.
* Useful for paging through large result sets.

**Syntax:**

```sql
SELECT * FROM Employees
ORDER BY EmployeeID
LIMIT 10 OFFSET 20;
```

* Skips first 20 rows and returns next 10 rows.

---

### 15.7 EXPLAIN – Check Query Execution Plan

* Shows how the database engine executes a query.
* Helps identify performance bottlenecks (e.g., full table scans, missing indexes).
* Displays info like table scans, join methods, indexes used.

**Example:**

```sql
EXPLAIN SELECT * FROM Employees WHERE Department = 'Sales';
```

* Output explains how MySQL scans tables and uses indexes.

---
