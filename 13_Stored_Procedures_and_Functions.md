### 13. Stored Procedures & Functions

---

## Stored Procedure

* A **Stored Procedure** is a precompiled collection of SQL statements and optional control-flow statements, stored in the database.
* It can perform operations such as modifying data, complex business logic, and can take input parameters.
* Stored Procedures **do not have to return a value**, but they can return result sets or output parameters.
* Useful for encapsulating repetitive or complex tasks to be executed on demand.

### Key Points:

* Created once and stored in the database.
* Can have input, output, and input-output parameters.
* Can perform multiple SQL statements.
* Cannot be used directly in SQL queries like SELECT.
* Executed using the `CALL` statement.

### Example: Stored Procedure to add a new student

```sql
DELIMITER //

CREATE PROCEDURE AddStudent(
    IN studentName VARCHAR(50),
    IN studentAge INT
)
BEGIN
    INSERT INTO Students (Name, Age)
    VALUES (studentName, studentAge);
END;
//

DELIMITER ;

-- To call the procedure:
CALL AddStudent('Tejas', 22);
```

---

## Function

* A **Function** is also a stored set of SQL statements, but it **must return a single value**.
* Functions can be called inside SQL queries like `SELECT`, `WHERE`, or `ORDER BY`.
* Typically used for calculations or returning a derived value.
* Functions can have input parameters but **cannot** have output parameters.

### Key Points:

* Must return a value using the `RETURN` statement.
* Can be used within SQL expressions.
* Cannot modify database tables (no INSERT, UPDATE, DELETE inside functions in MySQL).
* Useful for reusable calculations or formatting.

### Example: Function to calculate age next year

```sql
DELIMITER //

CREATE FUNCTION NextYearAge(currentAge INT)
RETURNS INT
DETERMINISTIC
BEGIN
    RETURN currentAge + 1;
END;
//

DELIMITER ;

-- Use in SELECT:
SELECT Name, Age, NextYearAge(Age) AS AgeNextYear
FROM Students;
```

---

## Differences Between Stored Procedure and Function

| Feature       | Stored Procedure                             | Function                                   |
| ------------- | -------------------------------------------- | ------------------------------------------ |
| Returns       | Zero or more result sets or output params    | Must return a single value                 |
| Usage         | Executed with `CALL` statement               | Can be used in SQL queries (SELECT, WHERE) |
| Side Effects  | Can modify database (INSERT, UPDATE, DELETE) | Generally should not modify database       |
| Parameters    | IN, OUT, INOUT parameters                    | Only IN parameters                         |
| Usage context | Complex business logic, batch operations     | Calculations, value-returning operations   |

---
