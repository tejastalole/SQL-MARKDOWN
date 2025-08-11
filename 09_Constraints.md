## 9. Constraints in SQL

Constraints define rules at the column or table level that restrict the types of data allowed in a table. They help ensure **data integrity** by preventing invalid data entries.

---

### 9.1 PRIMARY KEY

* Uniquely identifies each row in a table.
* Combines **NOT NULL** and **UNIQUE** constraints.
* There can be **only one primary key** per table.
* Primary key columns cannot contain NULL values.
* Often used as the main identifier for records.

**Example:**

```sql
CREATE TABLE Students (
  ID INT PRIMARY KEY,
  Name VARCHAR(50),
  Age INT
);
```

Here, `ID` is the primary key and must be unique for every student.

---

### 9.2 FOREIGN KEY

* Enforces a link between data in two tables.
* Ensures that a value in one table matches a valid value in another (referenced) table.
* Maintains **referential integrity**.
* Prevents inserting values in the foreign key column that don’t exist in the referenced primary key column.
* Can also specify actions on delete/update (CASCADE, SET NULL, etc.).

**Example:**

```sql
CREATE TABLE Enrollments (
  EnrollmentID INT PRIMARY KEY,
  StudentID INT,
  CourseID INT,
  FOREIGN KEY (StudentID) REFERENCES Students(ID),
  FOREIGN KEY (CourseID) REFERENCES Courses(ID)
);
```

This means `StudentID` in `Enrollments` must match an existing `ID` in `Students`.

---

### 9.3 UNIQUE

* Ensures all values in a column (or a group of columns) are **distinct**.
* Allows only unique values, but unlike primary key, **NULLs are allowed** (depending on DBMS).
* You can have multiple UNIQUE constraints in one table.

**Example:**

```sql
CREATE TABLE Employees (
  EmployeeID INT PRIMARY KEY,
  Email VARCHAR(100) UNIQUE,
  Phone VARCHAR(15) UNIQUE
);
```

No two employees can have the same email or phone number.

---

### 9.4 NOT NULL

* Ensures that a column **cannot contain NULL values**.
* Enforces that data **must be provided** for that column during insertion.

**Example:**

```sql
CREATE TABLE Products (
  ProductID INT PRIMARY KEY,
  ProductName VARCHAR(100) NOT NULL,
  Price DECIMAL(10, 2) NOT NULL
);
```

Every product must have a name and price.

---

### 9.5 DEFAULT

* Sets a **default value** for a column when no value is provided during insertion.
* Helps avoid NULLs or missing data by assigning sensible defaults.

**Example:**

```sql
CREATE TABLE Orders (
  OrderID INT PRIMARY KEY,
  OrderDate DATE DEFAULT CURDATE(),
  Status VARCHAR(20) DEFAULT 'Pending'
);
```

If `OrderDate` or `Status` are not specified during insert, they get default values.

---

### 9.6 CHECK

* Enforces **a condition** that each row must satisfy.
* Ensures values meet specific criteria.
* Not all DBMS fully support CHECK constraints, but many do.

**Example:**

```sql
CREATE TABLE Employees (
  EmployeeID INT PRIMARY KEY,
  Age INT CHECK (Age >= 18),
  Salary DECIMAL(10, 2) CHECK (Salary > 0)
);
```

* Employee age must be at least 18.
* Salary must be greater than 0.

---

### Summary Table

| Constraint  | Purpose                              | Example                                           | Notes                                |
| ----------- | ------------------------------------ | ------------------------------------------------- | ------------------------------------ |
| PRIMARY KEY | Unique row identifier                | `ID INT PRIMARY KEY`                              | Only one per table, no NULLs allowed |
| FOREIGN KEY | Referential integrity between tables | `FOREIGN KEY (StudentID) REFERENCES Students(ID)` | Links tables together                |
| UNIQUE      | Ensures unique column values         | `Email VARCHAR(100) UNIQUE`                       | Allows multiple unique constraints   |
| NOT NULL    | Disallows NULL values                | `Name VARCHAR(50) NOT NULL`                       | Forces value presence                |
| DEFAULT     | Sets default column value            | `Status VARCHAR(20) DEFAULT 'Pending'`            | Used if no value provided on insert  |
| CHECK       | Enforces condition on values         | `Age INT CHECK (Age >= 18)`                       | Validates data against custom rules  |

---
