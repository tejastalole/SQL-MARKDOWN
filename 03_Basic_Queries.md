## 3. Basic SQL Queries

### 3.1 SELECT – Retrieve Data

The **SELECT** statement is the most common SQL command. It is used to **fetch data** from one or more tables in the database.

* You specify the columns you want to retrieve after `SELECT`.
* Use `*` to select all columns.
* Can select from one or more tables, possibly with joins.

**Example:**

```sql
SELECT Name, Age FROM Students;
```

This returns the `Name` and `Age` columns for all rows in the `Students` table.

**To select all columns:**

```sql
SELECT * FROM Students;
```

---

### 3.2 WHERE – Filter Results

The **WHERE** clause filters records returned by the SELECT query (or affects UPDATE/DELETE commands). It specifies a condition that rows must satisfy to be included.

* Filters rows based on conditions (e.g., equals, greater than, LIKE, IN).
* Multiple conditions can be combined using `AND`, `OR`.

**Example:**

```sql
SELECT * FROM Students WHERE Age > 20;
```

Returns only students older than 20.

**Using multiple conditions:**

```sql
SELECT * FROM Students WHERE Age > 20 AND Grade = 'A';
```

Only students older than 20 **and** with grade 'A' will be returned.

---

### 3.3 ORDER BY – Sort Results

The **ORDER BY** clause sorts the result set by one or more columns.

* Default order is **ascending** (`ASC`).
* You can specify descending order using `DESC`.
* Useful to organize results by date, name, price, etc.

**Example:**

```sql
SELECT Name, Age FROM Students ORDER BY Age ASC;
```

Sorts students by age from youngest to oldest.

```sql
SELECT Name, Age FROM Students ORDER BY Age DESC;
```

Sorts students from oldest to youngest.

You can sort by multiple columns:

```sql
SELECT Name, Age, Grade FROM Students ORDER BY Grade ASC, Age DESC;
```

Sorts first by Grade ascending, then within each grade by Age descending.

---

### 3.4 DISTINCT – Remove Duplicates

The **DISTINCT** keyword removes duplicate rows from the result set.

* Useful when you want only unique values.
* Can be used with one or more columns.

**Example:**

```sql
SELECT DISTINCT Grade FROM Students;
```

Returns a list of unique grades without duplicates.

**Using DISTINCT with multiple columns:**

```sql
SELECT DISTINCT Grade, Age FROM Students;
```

Returns unique combinations of Grade and Age.

---

### 3.5 LIMIT – Restrict Number of Rows

The **LIMIT** clause restricts the number of rows returned by a query.

* Useful for pagination or previewing data.
* The exact syntax varies slightly between database systems (MySQL, PostgreSQL use `LIMIT`; SQL Server uses `TOP`).

**Example (MySQL/PostgreSQL):**

```sql
SELECT * FROM Students LIMIT 5;
```

Returns only the first 5 rows from the Students table.

**Combined with ORDER BY:**

```sql
SELECT * FROM Students ORDER BY Age DESC LIMIT 3;
```

Returns the 3 oldest students.

---

## Summary Table

| Clause   | Purpose                    | Example                                     |
| -------- | -------------------------- | ------------------------------------------- |
| SELECT   | Retrieve data              | `SELECT Name, Age FROM Students;`           |
| WHERE    | Filter rows                | `SELECT * FROM Students WHERE Age > 20;`    |
| ORDER BY | Sort result                | `SELECT * FROM Students ORDER BY Age DESC;` |
| DISTINCT | Remove duplicate rows      | `SELECT DISTINCT Grade FROM Students;`      |
| LIMIT    | Restrict number of results | `SELECT * FROM Students LIMIT 10;`          |

---
