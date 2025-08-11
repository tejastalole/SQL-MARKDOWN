## 11. Views in SQL

### What is a View?

* A **View** is a **virtual table** created by a query.
* It does **not store data** physically but displays data stored in one or more underlying tables.
* Acts like a saved SELECT query that you can reuse.
* Can simplify complex queries, enhance security, and present data in a specific format.

---

### How to Create a View

You create a view using the `CREATE VIEW` statement with a SELECT query.

**Syntax:**

```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

**Example:**

```sql
CREATE VIEW ActiveStudents AS
SELECT ID, Name, Age
FROM Students
WHERE Status = 'Active';
```

`ActiveStudents` is a view showing only students whose status is Active.

---

### Using Views

* Query a view like a regular table:

```sql
SELECT * FROM ActiveStudents;
```

* Views help encapsulate complex joins or filters behind a simple interface.

---

### Updating Views

* Views **can be updated** (INSERT, UPDATE, DELETE) if they meet certain conditions.
* Generally, views are updatable if:

  * Based on a **single table** (no joins).
  * Do **not** contain aggregate functions (`SUM`, `COUNT`), GROUP BY, DISTINCT, UNION.
  * Do not include computed columns.
  * Contain all NOT NULL columns without default values from the underlying table when inserting.

**Example of updatable view:**

```sql
CREATE VIEW StudentNames AS
SELECT ID, Name FROM Students;
```

You can update the `Name` column through the view:

```sql
UPDATE StudentNames SET Name = 'John Doe' WHERE ID = 1;
```

This updates the actual `Students` table.

---

### Non-updatable Views

* Views based on:

  * Joins of multiple tables.
  * Aggregation or GROUP BY.
  * DISTINCT, UNION.
  * Subqueries in SELECT.

  Usually **cannot be updated** directly.

---

### Benefits of Views

* **Simplify complex queries:** Hide complexity from users.
* **Security:** Restrict access to specific columns or rows.
* **Data abstraction:** Present data in a user-friendly way without exposing the full table.
* **Reusability:** Use the same query logic across multiple queries.

---

### Summary Table

| Aspect         | Details                                                                       |
| -------------- | ----------------------------------------------------------------------------- |
| What is a View | Virtual table based on a SELECT query                                         |
| Storage        | Does **not** store data physically                                            |
| Creation       | `CREATE VIEW view_name AS SELECT ...`                                         |
| Querying       | Used like normal tables (`SELECT * FROM view`)                                |
| Updatable      | Yes, if based on single table without aggregation, joins, or computed columns |
| Non-updatable  | Views with joins, aggregates, UNION, DISTINCT                                 |

---
