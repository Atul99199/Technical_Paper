# SQL and Database Concepts – Technical Paper

## 1. ACID

**ACID** is a set of properties that makes database transactions reliable and safe.

ACID stands for:

* **Atomicity** – A transaction is completed fully or not at all.
* **Consistency** – Data must remain valid before and after a transaction.
* **Isolation** – Multiple transactions should not incorrectly affect each other.
* **Durability** – Once data is committed, it should not be lost.

### Example

In a bank transfer:

```sql
BEGIN;

UPDATE accounts SET balance = balance - 1000 WHERE id = 1;
UPDATE accounts SET balance = balance + 1000 WHERE id = 2;

COMMIT;
```

If something fails, we can use:

```sql
ROLLBACK;
```

**Easy to remember:**
**Atomicity = All or Nothing**

---

## 2. CAP Theorem

The **CAP Theorem** is mainly used for distributed databases.

CAP stands for:

* **Consistency** – Every user gets the latest correct data.
* **Availability** – The system always gives a response.
* **Partition Tolerance** – The system continues working even if servers cannot communicate.

When a network partition occurs, a distributed system generally has to choose between **Consistency** and **Availability**.

### Example

If two database servers cannot communicate:

```text
Server A  ---- X ----  Server B
```

The system can:

* Stop some operations to maintain **Consistency** → **CP**
* Continue responding while allowing temporary differences → **AP**

**Easy to remember:**
**CAP = Consistency, Availability, Partition Tolerance**

---

## 3. Joins

A **JOIN** combines data from two or more related tables.

Suppose we have:

### Employees

| id | name  | department_id |
| -: | ----- | ------------: |
|  1 | Rahul |            10 |
|  2 | Priya |            20 |

### Departments

| id | department |
| -: | ---------- |
| 10 | IT         |
| 20 | HR         |

### INNER JOIN

Returns only matching records.

```sql
SELECT e.name, d.department
FROM employees e
INNER JOIN departments d
ON e.department_id = d.id;
```

### Common JOIN Types

| JOIN           | Meaning                                |
| -------------- | -------------------------------------- |
| **INNER JOIN** | Matching records only                  |
| **LEFT JOIN**  | All records from left table + matches  |
| **RIGHT JOIN** | All records from right table + matches |
| **FULL JOIN**  | All records from both tables           |
| **CROSS JOIN** | Every possible combination             |
| **SELF JOIN**  | A table joined with itself             |

**Easy to remember:**

```text
INNER → Matching
LEFT  → Everything on left
RIGHT → Everything on right
FULL  → Everything
```

---

## 4. Aggregations and Filters in Queries

### Aggregate Functions

Aggregate functions perform calculations on multiple rows.

| Function  | Purpose            |
| --------- | ------------------ |
| `COUNT()` | Counts rows        |
| `SUM()`   | Calculates total   |
| `AVG()`   | Calculates average |
| `MIN()`   | Finds minimum      |
| `MAX()`   | Finds maximum      |

Example:

```sql
SELECT AVG(salary)
FROM employees;
```

### GROUP BY

`GROUP BY` creates groups before performing aggregation.

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```

### WHERE

`WHERE` filters individual rows.

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

### HAVING

`HAVING` filters groups after aggregation.

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 2;
```

### Easy Difference

```text
WHERE   → Filters rows
GROUP BY → Creates groups
HAVING  → Filters groups
ORDER BY → Sorts results
```

---

## 5. Normalization

**Normalization** is the process of organizing database tables to **reduce duplicate data and prevent data problems**.

For example, instead of storing department information repeatedly:

```text
Employee
-------------------------
ID | Name | Department
```

we can separate it into:

```text
Employees
-------------------------
ID | Name | Department_ID

Departments
-------------------------
ID | Department_Name
```

The tables are connected using **primary keys and foreign keys**.

### Normal Forms

| Normal Form | Main Idea                         |
| ----------- | --------------------------------- |
| **1NF**     | Each cell contains a single value |
| **2NF**     | No partial dependency             |
| **3NF**     | No transitive dependency          |

### Benefits

* Reduces duplicate data
* Improves data consistency
* Prevents update, insert, and delete problems
* Makes the database easier to maintain

**Easy to remember:**

```text
1NF → Atomic values
2NF → No partial dependency
3NF → No transitive dependency
```

---

## 6. Indexes

An **index** is a database structure that helps find data faster.

It is similar to the **index of a book**.

Without an index:

```text
Database → Search many rows → Find data
```

With an index:

```text
Database → Index → Find data faster
```

### Create an Index

```sql
CREATE INDEX idx_employee_name
ON employees(name);
```

Now searches using `name` may become faster:

```sql
SELECT *
FROM employees
WHERE name = 'Rahul';
```

### Advantages

* Faster data retrieval
* Faster searches
* Can improve some sorting and join operations

### Disadvantages

* Requires extra storage
* Can slow down `INSERT`, `UPDATE`, and `DELETE`
* Too many indexes can hurt performance

**Easy to remember:**

> **Index = Faster reads, but extra storage and write cost.**

---

## 7. Transactions

A **transaction** is a group of SQL operations treated as **one unit of work**.

Example:

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 1000
WHERE id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE id = 2;

COMMIT;
```

If something goes wrong:

```sql
ROLLBACK;
```

### Important Commands

| Command     | Purpose                              |
| ----------- | ------------------------------------ |
| `BEGIN`     | Starts a transaction                 |
| `COMMIT`    | Saves changes                        |
| `ROLLBACK`  | Undoes uncommitted changes           |
| `SAVEPOINT` | Creates a point for partial rollback |

### Real Example

For a bank transfer:

```text
Debit Account A
      ↓
Credit Account B
      ↓
Both successful?
   ↙       ↘
 YES        NO
 ↓           ↓
COMMIT    ROLLBACK
```

**Easy to remember:**

> **Transaction = A group of operations that should succeed or fail together.**

---

## 8. Locking Mechanism

**Locking** controls how multiple transactions access the same data at the same time.

It helps prevent problems such as:

* Lost updates
* Conflicting changes
* Incorrect concurrent operations

### Shared Lock

A **Shared Lock** is mainly used when data is being read with locking requirements.

Multiple compatible shared locks can exist at the same time.

### Exclusive Lock

An **Exclusive Lock** is used when data needs to be modified.

Other conflicting operations must wait.

### Example

In PostgreSQL:

```sql
SELECT *
FROM accounts
WHERE id = 1
FOR UPDATE;
```

This locks the selected row for update.

### Deadlock

A **deadlock** happens when two transactions wait for each other.

```text
Transaction A → Locks Row 1 → Wants Row 2
Transaction B → Locks Row 2 → Wants Row 1
```

Neither can continue until the database detects and resolves the conflict.

**Easy to remember:**

> **Locking = Controlling access to shared data.**

---

## 9. Database Isolation Levels

**Isolation levels** control how much one transaction can see from other transactions running at the same time.

The common isolation levels are:

1. **READ UNCOMMITTED**
2. **READ COMMITTED**
3. **REPEATABLE READ**
4. **SERIALIZABLE**

### 1. READ UNCOMMITTED

Allows the weakest isolation.

A transaction may read data that another transaction has not committed yet.

This can cause a **dirty read**.

### 2. READ COMMITTED

A transaction sees only committed data.

**This is the default isolation level in PostgreSQL.**

### 3. REPEATABLE READ

A transaction gets a consistent view of data during its execution.

### 4. SERIALIZABLE

The strongest standard isolation level.

Transactions behave as if they were executed one after another.

### Comparison

| Level            | Isolation | Performance |
| ---------------- | --------- | ----------- |
| READ UNCOMMITTED | Lowest    | High        |
| READ COMMITTED   | Medium    | High        |
| REPEATABLE READ  | Higher    | Medium      |
| SERIALIZABLE     | Highest   | Lower       |

### Common Problems

* **Dirty Read** – Reading uncommitted data
* **Non-Repeatable Read** – Same row gives different values
* **Phantom Read** – A repeated query returns a different set of rows

**Easy to remember:**

> **Higher isolation = stronger consistency but potentially less concurrency.**

---

## 10. Triggers

A **trigger** is a database feature that automatically performs an action when a specific event occurs.

Common events are:

```text
INSERT
UPDATE
DELETE
```

### Example

Suppose we want to automatically record salary changes.

```text
UPDATE Employee
      ↓
Trigger
      ↓
Insert record into Audit Table
```

In PostgreSQL, a trigger usually calls a trigger function:

```sql
CREATE TRIGGER employee_audit
AFTER UPDATE ON employees
FOR EACH ROW
EXECUTE FUNCTION log_employee_changes();
```

### Types

| Type           | Meaning                                           |
| -------------- | ------------------------------------------------- |
| **BEFORE**     | Runs before the operation                         |
| **AFTER**      | Runs after the operation                          |
| **INSTEAD OF** | Runs instead of the operation, commonly for views |
| **ROW**        | Runs once for each affected row                   |
| **STATEMENT**  | Runs once for the whole SQL statement             |

### `OLD` and `NEW`

In row-level triggers:

```text
OLD → Previous value
NEW → New value
```

### Common Uses

* Audit logging
* Automatic timestamps
* Data validation
* Maintaining related data

**Easy to remember:**

> **Trigger = An automatic database action caused by an event.**

---
## Reference

- PostgreSQL Documentation – Transaction Isolation  
   https://www.postgresql.org/docs/current/transaction-iso.html
- PostgreSQL Documentation – Indexes  
   https://www.postgresql.org/docs/current/indexes.html
- PostgreSQL Documentation – SQL SELECT and Joins  
   https://www.postgresql.org/docs/current/sql-select.html  

