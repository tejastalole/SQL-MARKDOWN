## 1. Basics of SQL

**SQL** (Structured Query Language) is a standard programming language used to manage and manipulate **relational databases**. It allows you to perform tasks such as creating databases and tables, inserting and updating data, querying data, controlling access, and managing transactions.

---

## 2. Types of SQL Commands

### 2.1 DDL (Data Definition Language)

DDL commands define or modify the structure of database objects like tables, indexes, and schemas. These commands deal with the schema or structure.

* **CREATE**
  Creates a new database object such as a table, view, or index.

  ```sql
  CREATE TABLE Students (
      ID INT PRIMARY KEY,
      Name VARCHAR(50),
      Age INT
  );
  ```

* **ALTER**
  Changes the structure of an existing database object. For example, add or drop columns from a table.

  ```sql
  ALTER TABLE Students ADD COLUMN Grade CHAR(1);
  ```

* **DROP**
  Deletes an existing database object and all its data permanently.

  ```sql
  DROP TABLE Students;
  ```

* **TRUNCATE**
  Deletes all rows from a table but keeps the structure intact. It’s faster than DELETE for removing all rows because it does not log individual row deletions.

  ```sql
  TRUNCATE TABLE Students;
  ```

---

### 2.2 DML (Data Manipulation Language)

DML commands deal with the **data itself** — inserting, updating, and deleting records in the database tables.

* **INSERT**
  Adds new rows (records) into a table.

  ```sql
  INSERT INTO Students (ID, Name, Age) VALUES (1, 'Alice', 21);
  ```

* **UPDATE**
  Modifies existing data in the table.

  ```sql
  UPDATE Students SET Age = 22 WHERE ID = 1;
  ```

* **DELETE**
  Removes rows from a table based on a condition.

  ```sql
  DELETE FROM Students WHERE ID = 1;
  ```

---

### 2.3 DQL (Data Query Language)

DQL is used to **query or fetch data** from the database.

* **SELECT**
  Retrieves data from one or more tables.

  ```sql
  SELECT * FROM Students;
  ```

  You can also filter, sort, and join data with SELECT.

---

### 2.4 DCL (Data Control Language)

DCL commands control **access and permissions** on the database objects.

* **GRANT**
  Gives users permissions to perform certain actions on database objects.

  ```sql
  GRANT SELECT, INSERT ON Students TO 'user1';
  ```

* **REVOKE**
  Removes previously granted permissions from users.

  ```sql
  REVOKE INSERT ON Students FROM 'user1';
  ```

---

### 2.5 TCL (Transaction Control Language)

TCL commands manage **transactions** in the database, ensuring data integrity.

* **COMMIT**
  Saves all changes made in the current transaction permanently.

  ```sql
  COMMIT;
  ```

* **ROLLBACK**
  Undoes all changes made in the current transaction since the last COMMIT.

  ```sql
  ROLLBACK;
  ```

* **SAVEPOINT**
  Creates a point within a transaction to which you can later roll back without affecting the entire transaction.

  ```sql
  SAVEPOINT Savepoint1;
  ```

  You can then rollback to this savepoint:

  ```sql
  ROLLBACK TO Savepoint1;
  ```

---
