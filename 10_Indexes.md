## 10. Indexes in SQL

### Purpose of Indexes

* **Indexes** are special data structures that improve the **speed** of data retrieval operations on a database table.
* They allow the database engine to quickly locate rows without scanning the entire table.
* Like an index in a book, it points to where the data is stored.
* Indexes can significantly improve query performance, especially on large tables.
* However, indexes **slow down write operations** (INSERT, UPDATE, DELETE) because the index also needs updating.
* Indexes consume additional storage space.

---

### How Indexes Work (Simplified)

* Internally, indexes are often implemented using balanced trees (e.g., B-trees).
* When you query using indexed columns, the database uses the index to jump directly to the matching rows instead of scanning every row.

---

## Types of Indexes

---

### 10.1 Normal Index (or Non-Unique Index)

* The most basic type.
* Speeds up queries on columns where duplicate values are allowed.
* Does **not enforce uniqueness** — multiple rows can have the same indexed value.

**Example:**

```sql
CREATE INDEX idx_lastname ON Employees(LastName);
```

This index speeds up searches filtering or sorting by `LastName`.

---

### 10.2 Unique Index

* Ensures all values in the indexed column(s) are **unique**.
* Automatically created when you define a **PRIMARY KEY** or **UNIQUE** constraint.
* Prevents duplicate values in the indexed columns.

**Example:**

```sql
CREATE UNIQUE INDEX idx_email ON Employees(Email);
```

Prevents multiple employees from having the same email address.

---

### 10.3 Composite Index (Multi-column Index)

* An index on **two or more columns**.
* Useful when queries filter or sort by multiple columns together.
* The order of columns in the index matters for how it’s used.

**Example:**

```sql
CREATE INDEX idx_name_dob ON Employees(LastName, DateOfBirth);
```

This index speeds up queries filtering by `LastName` and `DateOfBirth` together.

* It can also speed queries filtering just by `LastName` (the leftmost column).
* But it won’t help if filtering only by `DateOfBirth` without `LastName`.

---

### 10.4 Full-text Index

* Specialized index for **text searching** in large text columns.
* Enables fast searching for words or phrases inside text data (e.g., articles, descriptions).
* Supports advanced text search features like relevance ranking and boolean text search.

**Example (MySQL):**

```sql
CREATE FULLTEXT INDEX idx_description ON Articles(Description);
```

Allows queries like:

```sql
SELECT * FROM Articles
WHERE MATCH(Description) AGAINST('database');
```

to quickly find articles containing the word "database".

---

## When to Use Indexes

* Use indexes on columns used frequently in `WHERE`, `JOIN`, `ORDER BY`, and `GROUP BY` clauses.
* Use unique indexes for columns that must have unique values.
* Avoid over-indexing as it can slow down data modification and consume storage.
* Consider composite indexes for multi-column filtering.

---

## Summary Table

| Index Type      | Purpose                              | Example                                                          | Key Characteristics                       |
| --------------- | ------------------------------------ | ---------------------------------------------------------------- | ----------------------------------------- |
| Normal Index    | Speed up search on columns           | `CREATE INDEX idx_lastname ON Employees(LastName);`              | Allows duplicates, no uniqueness enforced |
| Unique Index    | Enforce uniqueness + speed up search | `CREATE UNIQUE INDEX idx_email ON Employees(Email);`             | No duplicate values allowed               |
| Composite Index | Index on multiple columns            | `CREATE INDEX idx_name_dob ON Employees(LastName, DateOfBirth);` | Useful for queries on multiple columns    |
| Full-text Index | Fast text search inside large text   | `CREATE FULLTEXT INDEX idx_desc ON Articles(Description);`       | Supports advanced text searching          |

---
