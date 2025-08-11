## 12. Transactions in SQL

---

### What is a Transaction?

* A **transaction** is a sequence of one or more SQL operations executed as a **single unit of work**.
* All operations in a transaction must **succeed together** or **fail together**.
* Transactions ensure data integrity, especially when multiple operations depend on each other.

---

### Transaction Commands

| Command               | Purpose                                                                                                |
| --------------------- | ------------------------------------------------------------------------------------------------------ |
| **START TRANSACTION** | Begins a new transaction                                                                               |
| **COMMIT**            | Saves all changes made during the transaction                                                          |
| **ROLLBACK**          | Undoes all changes since the last COMMIT or START TRANSACTION                                          |
| **SAVEPOINT**         | Creates a point within a transaction to which you can rollback without aborting the entire transaction |

---

### How Transactions Work

* Begin with `START TRANSACTION`.
* Perform multiple SQL operations (INSERT, UPDATE, DELETE).
* Use `COMMIT` to save all changes permanently.
* Use `ROLLBACK` to undo all changes if an error occurs.
* Use `SAVEPOINT` to mark intermediate points; can rollback to these points if needed.

---

### Example:

```sql
START TRANSACTION;

UPDATE Accounts SET Balance = Balance - 500 WHERE AccountID = 101;
UPDATE Accounts SET Balance = Balance + 500 WHERE AccountID = 102;

COMMIT;
```

* Transfers 500 from Account 101 to Account 102.
* Both updates succeed together, or if any fails, no change occurs.

---

### ACID Properties of Transactions

Transactions follow **ACID** principles to ensure reliable processing:

| Property        | Meaning                                       | Explanation                                                                                                        |
| --------------- | --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **Atomicity**   | All or nothing                                | Either all operations in a transaction are done, or none are. Partial completion is not allowed.                   |
| **Consistency** | Valid data states                             | Transaction must transform the database from one valid state to another, preserving all rules and constraints.     |
| **Isolation**   | Transactions do not interfere with each other | Intermediate changes of a transaction are invisible to other transactions until committed, preventing dirty reads. |
| **Durability**  | Once committed, changes are permanent         | After a commit, changes survive system crashes or failures. Data is safely stored on disk.                         |

---

### More on Isolation Levels

* Different **isolation levels** control how strictly transactions are isolated.
* Common levels: **READ UNCOMMITTED**, **READ COMMITTED**, **REPEATABLE READ**, **SERIALIZABLE**.
* Higher isolation reduces concurrency but increases data accuracy.

---

### SAVEPOINT Usage Example

```sql
START TRANSACTION;

UPDATE Accounts SET Balance = Balance - 500 WHERE AccountID = 101;

SAVEPOINT BeforeCredit;

UPDATE Accounts SET Balance = Balance + 500 WHERE AccountID = 102;

-- Something goes wrong here
ROLLBACK TO SAVEPOINT BeforeCredit;

COMMIT;
```

* Rolls back only the last update, not the entire transaction.

---

### Summary Table

| Command           | Function                                            |
| ----------------- | --------------------------------------------------- |
| START TRANSACTION | Begin a transaction                                 |
| COMMIT            | Make all changes permanent                          |
| ROLLBACK          | Undo changes since transaction start or last commit |
| SAVEPOINT         | Create a rollback point inside a transaction        |

| ACID Property | Purpose                                             |
| ------------- | --------------------------------------------------- |
| Atomicity     | All-or-nothing execution                            |
| Consistency   | Maintains database rules and constraints            |
| Isolation     | Transactions don’t see each other’s partial changes |
| Durability    | Changes persist after commit                        |

---
