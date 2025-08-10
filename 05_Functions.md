## 5. Functions in SQL

Functions are built-in commands that take inputs (arguments) and return a processed value. They help manipulate data and perform calculations.

---

### 5.1 Aggregate Functions

Aggregate functions operate on multiple rows and return a single summary value.

| Function    | Purpose                                    | Example                              | Explanation                    |
| ----------- | ------------------------------------------ | ------------------------------------ | ------------------------------ |
| **COUNT()** | Counts number of rows (or non-null values) | `SELECT COUNT(*) FROM Students;`     | Counts total rows in the table |
| **SUM()**   | Adds values in a column                    | `SELECT SUM(Salary) FROM Employees;` | Total sum of all salaries      |
| **AVG()**   | Calculates average value                   | `SELECT AVG(Age) FROM Students;`     | Average age of students        |
| **MAX()**   | Returns maximum value                      | `SELECT MAX(Price) FROM Products;`   | Highest price among products   |
| **MIN()**   | Returns minimum value                      | `SELECT MIN(Age) FROM Students;`     | Youngest student age           |

**Notes:**

* Aggregate functions ignore NULLs (except COUNT(\*))
* Often used with `GROUP BY` to summarize data per group.

---

### 5.2 String Functions

Used to manipulate and query text data.

| Function        | Purpose                    | Example                                                   | Explanation                                |
| --------------- | -------------------------- | --------------------------------------------------------- | ------------------------------------------ |
| **CONCAT()**    | Joins two or more strings  | `SELECT CONCAT(FirstName, ' ', LastName) FROM Employees;` | Combines first and last names with a space |
| **LENGTH()**    | Returns length of string   | `SELECT LENGTH(Name) FROM Students;`                      | Number of characters in the name           |
| **UPPER()**     | Converts text to uppercase | `SELECT UPPER(Name) FROM Students;`                       | Converts name to all uppercase             |
| **LOWER()**     | Converts text to lowercase | `SELECT LOWER(Name) FROM Students;`                       | Converts name to all lowercase             |
| **SUBSTRING()** | Extracts part of string    | `SELECT SUBSTRING(Name, 1, 3) FROM Students;`             | First 3 characters of the name             |

---

### 5.3 Date Functions

Used to handle date and time values.

| Function           | Purpose                           | Example                                  | Explanation                                       |
| ------------------ | --------------------------------- | ---------------------------------------- | ------------------------------------------------- |
| **NOW()**          | Returns current date and time     | `SELECT NOW();`                          | Current date & time (e.g., '2025-08-11 14:30:00') |
| **CURDATE()**      | Returns current date only         | `SELECT CURDATE();`                      | Current date (e.g., '2025-08-11')                 |
| **DATE\_FORMAT()** | Formats date in specified pattern | `SELECT DATE_FORMAT(NOW(), '%d-%m-%Y');` | Formats current date as '11-08-2025'              |

**Common format specifiers for `DATE_FORMAT()`**:

* `%Y` – Year (4 digits)
* `%m` – Month (2 digits)
* `%d` – Day of month (2 digits)
* `%H` – Hour (24-hour)
* `%i` – Minutes
* `%s` – Seconds

---

### 5.4 Math Functions

Used to perform mathematical operations.

| Function    | Purpose                           | Example                     | Explanation                                |
| ----------- | --------------------------------- | --------------------------- | ------------------------------------------ |
| **ROUND()** | Rounds a number to given decimals | `SELECT ROUND(3.14159, 2);` | Returns 3.14 (rounded to 2 decimal places) |
| **ABS()**   | Returns absolute (positive) value | `SELECT ABS(-15);`          | Returns 15                                 |
| **CEIL()**  | Returns smallest integer ≥ number | `SELECT CEIL(4.2);`         | Returns 5                                  |
| **FLOOR()** | Returns largest integer ≤ number  | `SELECT FLOOR(4.8);`        | Returns 4                                  |

---

### Example Combining Functions

```sql
SELECT 
  COUNT(*) AS TotalStudents,
  AVG(Age) AS AverageAge,
  MAX(Salary) AS HighestSalary,
  CONCAT(UPPER(FirstName), ' ', UPPER(LastName)) AS FullName,
  ROUND(AVG(Salary), 2) AS AvgSalaryRounded,
  DATE_FORMAT(NOW(), '%d-%m-%Y') AS TodayDate
FROM Employees;
```

This query:

* Counts total students
* Calculates average age
* Finds highest salary
* Joins first and last names in uppercase
* Rounds average salary to 2 decimals
* Formats current date as dd-mm-yyyy

---
