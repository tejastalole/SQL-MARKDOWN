## 4. Filtering Data in SQL

Filtering lets you narrow down the rows returned by a query based on specific conditions. You mostly use these in the **WHERE** clause.

---

### 4.1 Comparison Operators

Used to compare values in columns.

| Operator | Meaning                  | Example                    | Explanation                               |
| -------- | ------------------------ | -------------------------- | ----------------------------------------- |
| =        | Equal to                 | `WHERE Age = 20`           | Matches rows where Age is exactly 20      |
| != or <> | Not equal to             | `WHERE Status != 'Active'` | Matches rows where Status is not 'Active' |
| <        | Less than                | `WHERE Price < 100`        | Matches rows with Price less than 100     |
| >        | Greater than             | `WHERE Age > 30`           | Matches rows with Age greater than 30     |
| <=       | Less than or equal to    | `WHERE Score <= 50`        | Matches rows with Score 50 or less        |
| >=       | Greater than or equal to | `WHERE Salary >= 50000`    | Matches rows with Salary 50000 or more    |

---

### 4.2 Logical Operators

Combine multiple conditions.

| Operator | Meaning                      | Example                                   | Explanation                                 |
| -------- | ---------------------------- | ----------------------------------------- | ------------------------------------------- |
| AND      | Both conditions must be true | `WHERE Age > 20 AND Grade = 'A'`          | Both Age > 20 **and** Grade = 'A'           |
| OR       | Either condition can be true | `WHERE City = 'Mumbai' OR City = 'Delhi'` | City is either Mumbai **or** Delhi          |
| NOT      | Negates the condition        | `WHERE NOT Status = 'Inactive'`           | Matches rows where Status is NOT 'Inactive' |

---

### 4.3 Pattern Matching: LIKE and NOT LIKE

Used for searching text with wildcards.

* `%` matches zero or more characters.
* `_` matches exactly one character.

| Syntax        | Example                                         | Matches                      |
| ------------- | ----------------------------------------------- | ---------------------------- |
| `LIKE 'A%'`   | Names starting with A                           | 'Alice', 'Adam', 'Alex'      |
| `LIKE '%son'` | Names ending with 'son'                         | 'Jackson', 'Wilson'          |
| `LIKE '%a%'`  | Names containing 'a' anywhere                   | 'Sarah', 'Adam', 'James'     |
| `LIKE 'A_'`   | Names with exactly 2 characters starting with A | 'Al', 'An'                   |
| `NOT LIKE`    | Does not match the pattern                      | Names that don’t contain 'a' |

**Example:**

```sql
SELECT * FROM Employees WHERE Name LIKE 'J%n';
```

Matches employees whose names start with 'J' and end with 'n' like 'John', 'Jordan'.

---

### 4.4 Sets: IN and NOT IN

Test if a value matches any value in a list.

* **IN** checks if the value is in the specified set.
* **NOT IN** checks if the value is not in the set.

**Example:**

```sql
SELECT * FROM Students WHERE Grade IN ('A', 'B', 'C');
```

Selects students whose grade is either A, B, or C.

```sql
SELECT * FROM Students WHERE City NOT IN ('Mumbai', 'Delhi');
```

Selects students not from Mumbai or Delhi.

---

### 4.5 Ranges: BETWEEN and NOT BETWEEN

Check if a value is within or outside a range (inclusive).

* **BETWEEN** includes both boundary values.
* **NOT BETWEEN** excludes values in the range.

**Example:**

```sql
SELECT * FROM Products WHERE Price BETWEEN 100 AND 500;
```

Selects products priced from 100 to 500 inclusive.

```sql
SELECT * FROM Employees WHERE Age NOT BETWEEN 30 AND 40;
```

Selects employees younger than 30 or older than 40.

---

### 4.6 Null Check: IS NULL and IS NOT NULL

Used to check for missing or unknown values.

* **IS NULL** finds rows where the value is NULL (no data).
* **IS NOT NULL** finds rows where the value exists.

**Example:**

```sql
SELECT * FROM Orders WHERE ShippedDate IS NULL;
```

Finds orders that have not been shipped yet.

```sql
SELECT * FROM Customers WHERE Email IS NOT NULL;
```

Finds customers who have provided their email addresses.

---

## Summary Table

| Operator                 | Usage                         | Example                             | Result                               |
| ------------------------ | ----------------------------- | ----------------------------------- | ------------------------------------ |
| `=`                      | Equal                         | `WHERE Age = 25`                    | Rows where Age is 25                 |
| `!=` or `<>`             | Not equal                     | `WHERE Status != 'Active'`          | Rows where Status is not 'Active'    |
| `<`, `>`, `<=`, `>=`     | Less than, greater than, etc. | `WHERE Salary >= 50000`             | Rows with Salary 50000 or more       |
| `AND`, `OR`, `NOT`       | Combine conditions            | `WHERE Age > 20 AND Grade = 'A'`    | Rows meeting both conditions         |
| `LIKE`, `NOT LIKE`       | Pattern matching              | `WHERE Name LIKE 'A%'`              | Names starting with 'A'              |
| `IN`, `NOT IN`           | Matches any in list           | `WHERE City IN ('Delhi', 'Mumbai')` | Rows from either Delhi or Mumbai     |
| `BETWEEN`, `NOT BETWEEN` | Check range                   | `WHERE Price BETWEEN 100 AND 200`   | Prices between 100 and 200 inclusive |
| `IS NULL`, `IS NOT NULL` | Null check                    | `WHERE Email IS NULL`               | Rows with missing Email values       |

---
