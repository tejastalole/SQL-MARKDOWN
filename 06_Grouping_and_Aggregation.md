## 6. Grouping & Aggregation in SQL

When you want to **summarize** data by categories or groups—like total sales per region, or average salary per department—you use `GROUP BY` and `HAVING`.

---

### 6.1 GROUP BY – Group Rows by One or More Columns

* The `GROUP BY` clause groups rows that have the same values in specified columns into summary rows.
* It’s mainly used with **aggregate functions** (like COUNT, SUM, AVG) to calculate values per group.
* When you use `GROUP BY`, **all** columns in the `SELECT` list must either be:

  * Included in the `GROUP BY` clause, or
  * Used inside aggregate functions.

**Syntax:**

```sql
SELECT column1, aggregate_function(column2)
FROM table
GROUP BY column1;
```

**Example:**

```sql
SELECT Department, COUNT(*) AS EmployeeCount
FROM Employees
GROUP BY Department;
```

This query counts how many employees are in each department. The result will have one row per department.

---

### 6.2 HAVING – Filter Groups After Aggregation

* `HAVING` is like a **WHERE** clause but applies to groups **after** aggregation.
* It filters groups based on conditions on aggregate functions.
* Use it to restrict the grouped result set.

**Syntax:**

```sql
SELECT column1, aggregate_function(column2)
FROM table
GROUP BY column1
HAVING aggregate_function(column2) condition;
```

**Example:**

```sql
SELECT Department, COUNT(*) AS EmployeeCount
FROM Employees
GROUP BY Department
HAVING COUNT(*) > 10;
```

This query returns only departments that have **more than 10 employees**.

---

### Important Notes:

* You **cannot** use aggregate functions directly in the `WHERE` clause — that’s what `HAVING` is for.
* `WHERE` filters rows **before** grouping.
* `HAVING` filters groups **after** grouping and aggregation.

---

### Combined Example:

```sql
SELECT Department, AVG(Salary) AS AvgSalary
FROM Employees
WHERE Age > 25          -- filter rows before grouping
GROUP BY Department
HAVING AVG(Salary) > 50000;  -- filter groups after aggregation
```

* First, only employees older than 25 are considered.
* Then, employees are grouped by department.
* Finally, only departments with average salary greater than 50,000 are returned.

---

### Summary Table

| Clause   | Purpose                           | When it applies | Example                |
| -------- | --------------------------------- | --------------- | ---------------------- |
| WHERE    | Filter individual rows            | Before grouping | `WHERE Age > 25`       |
| GROUP BY | Group rows based on columns       | Groups rows     | `GROUP BY Department`  |
| HAVING   | Filter groups based on aggregates | After grouping  | `HAVING COUNT(*) > 10` |

---
