## 14. Triggers in SQL

---

### What is a Trigger?

* A **trigger** is a special kind of stored procedure that automatically executes (or "fires") when certain events occur in the database.
* Triggers help automate tasks, enforce complex business rules, maintain audit trails, or synchronize tables.
* They are attached to a specific table and react to data modification events.

---

### When Do Triggers Run?

Triggers execute **automatically** in response to one or more of these events on a table:

| Event      | Description                                    |
| ---------- | ---------------------------------------------- |
| **INSERT** | Trigger fires when a new row is added          |
| **UPDATE** | Trigger fires when an existing row is modified |
| **DELETE** | Trigger fires when a row is deleted            |

---

### Types of Triggers Based on Timing

| Trigger Type           | When It Runs                                                            |
| ---------------------- | ----------------------------------------------------------------------- |
| **BEFORE Trigger**     | Runs **before** the triggering operation (INSERT/UPDATE/DELETE) happens |
| **AFTER Trigger**      | Runs **after** the triggering operation has completed                   |
| **INSTEAD OF Trigger** | Runs **instead of** the triggering operation (mostly on views)          |

---

### Why Use Triggers?

* **Data validation and enforcement:** Automatically check or modify data before or after changes.
* **Auditing:** Keep track of changes by logging them in audit tables.
* **Derived column updates:** Update related tables or columns automatically.
* **Complex business logic:** Implement rules that are hard to enforce with constraints.

---

### Basic Syntax of a Trigger (MySQL Example)

```sql
CREATE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE
ON table_name
FOR EACH ROW
BEGIN
  -- SQL statements to execute
END;
```

---

### Example 1: Audit Insertions

Keep a log of every new employee inserted:

```sql
CREATE TRIGGER LogEmployeeInsert
AFTER INSERT ON Employees
FOR EACH ROW
BEGIN
  INSERT INTO EmployeeAudit (EmployeeID, Action, ActionDate)
  VALUES (NEW.EmployeeID, 'INSERT', NOW());
END;
```

* `NEW` refers to the newly inserted row.
* Whenever a new employee is added, a record is inserted into `EmployeeAudit`.

---

### Example 2: Prevent Negative Salary (BEFORE UPDATE)

```sql
CREATE TRIGGER PreventNegativeSalary
BEFORE UPDATE ON Employees
FOR EACH ROW
BEGIN
  IF NEW.Salary < 0 THEN
    SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Salary cannot be negative';
  END IF;
END;
```

* This trigger checks salary before update.
* Throws an error if salary is set below zero, preventing the update.

---

### Key Points

* Triggers are **table-level** objects.
* They execute **automatically** without explicit calls.
* `NEW` and `OLD` keywords represent new and old row data inside triggers.
* Triggers can affect performance if overused, so use judiciously.
* Complex logic can be placed inside triggers, but maintainability should be considered.

---

### Summary Table

| Aspect            | Description                             |
| ----------------- | --------------------------------------- |
| What is a trigger | Auto-executed code on table events      |
| Trigger events    | INSERT, UPDATE, DELETE                  |
| Timing            | BEFORE, AFTER, INSTEAD OF               |
| Uses              | Auditing, validation, automatic updates |
| Keywords          | `NEW` (new row), `OLD` (old row)        |

---
