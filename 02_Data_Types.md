## 2. Data Types in SQL

Data types specify what kind of data a column can store. Choosing the right data type helps ensure data accuracy, optimize storage, and improve query performance.

---

### 2.1 Numeric Data Types

Used to store numbers. They can be integers (whole numbers) or floating-point numbers (with decimals).

* **INT (INTEGER)**
  Stores whole numbers without decimals.
  Typically 4 bytes in size.
  Example values: `-2147483648` to `2147483647` (depends on implementation).
  Used when you need to store counts, IDs, or any whole number data.

  ```sql
  Age INT;
  ```

* **FLOAT**
  Stores approximate floating-point numbers with decimal points.
  Used for scientific calculations or when precision is not strict.
  Note: FLOAT may introduce rounding errors because it stores data approximately.

  ```sql
  Price FLOAT;
  ```

* **DECIMAL (or NUMERIC)**
  Stores exact numeric values with fixed precision and scale.
  You specify the total number of digits and the number of digits after the decimal point.
  Useful for financial and monetary data where accuracy matters.

  Syntax:

  ```sql
  DECIMAL(precision, scale)
  ```

  * `precision`: total number of digits (before and after decimal)
  * `scale`: number of digits after the decimal point

  Example:

  ```sql
  Salary DECIMAL(10, 2);
  ```

  This means the Salary can store numbers up to 10 digits long, with 2 digits after the decimal point (e.g., 12345678.90).

---

### 2.2 String Data Types

Used to store text or character data.

* **CHAR(n)**
  Fixed-length character string.
  Always stores `n` characters. If the input is shorter, it pads with spaces to the right.
  Efficient for storing data with consistent length, e.g., country codes, fixed-length IDs.

  ```sql
  CountryCode CHAR(3);
  ```

  If you store "IN" in `CHAR(3)`, it will store `"IN "` (with one space).

* **VARCHAR(n)**
  Variable-length character string.
  Stores up to `n` characters, but uses only as much space as needed.
  More flexible and space-efficient than CHAR when length varies.

  ```sql
  Name VARCHAR(50);
  ```

  If you store "Alice" in `VARCHAR(50)`, it uses only 5 characters worth of space.

* **TEXT**
  Used to store large amounts of text data, typically longer than what VARCHAR can store.
  Usually used for descriptions, comments, articles, or any large textual data.

  ```sql
  Description TEXT;
  ```

  The maximum size depends on the database system (can be very large).

---

### 2.3 Date/Time Data Types

Used to store date and time values, supporting date calculations and formatting.

* **DATE**
  Stores only the date part: year, month, and day.
  Format: `YYYY-MM-DD`

  ```sql
  BirthDate DATE;
  ```

  Example value: `2025-08-11`

* **DATETIME**
  Stores both date and time.
  Format: `YYYY-MM-DD HH:MM:SS`

  ```sql
  CreatedAt DATETIME;
  ```

  Example value: `2025-08-11 14:30:00`

* **TIMESTAMP**
  Stores both date and time, similar to DATETIME but usually tracks time in UTC (Coordinated Universal Time).
  Often used to record when a row was last modified.
  Automatically updated in some DBMS when a row changes.

  ```sql
  UpdatedAt TIMESTAMP;
  ```

  Example value: `2025-08-11 08:30:00` (UTC time)

---

### Summary Table

| Data Type  | Description                      | Example Usage                   |
| ---------- | -------------------------------- | ------------------------------- |
| INT        | Whole numbers                    | Age, Quantity                   |
| FLOAT      | Approximate decimal numbers      | Scientific values, measurements |
| DECIMAL    | Exact decimal numbers            | Prices, Salary                  |
| CHAR(n)    | Fixed-length strings             | Country codes, Fixed IDs        |
| VARCHAR(n) | Variable-length strings          | Names, Emails                   |
| TEXT       | Large text data                  | Descriptions, Articles          |
| DATE       | Date only                        | Birthdate, Event date           |
| DATETIME   | Date and time                    | Order time, Login timestamp     |
| TIMESTAMP  | Date and time with timezone info | Last updated time               |

---
