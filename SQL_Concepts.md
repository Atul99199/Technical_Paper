# SQL Technical Notes
## 1. ACID
- **Atomicity** → All or nothing; failed transactions are undone. 
- **Consistency** → Keeps data valid before and after a transaction.
- **Isolation** → Keeps concurrent transactions safely separated.
- **Durability** → Keeps committed changes saved even after a failure.
## 2. CAP Theorem
```text
Server A  ---- X ----  Server B
```
- **X** → Communication failure between servers.
- **CP** → Stops some operations to keep data consistent.
- **AP** → Keeps responding even if data is temporarily different.
- **CAP** → Consistency, Availability, Partition Tolerance.
## 3. Joins
A JOIN combines related data from two or more tables.
For example, employees can be connected to their departments.
Employees may contain an employee name and a department ID.
Departments may contain a department ID and department name.
An INNER JOIN returns only rows that match in both tables.
Example:
```sql
SELECT e.name, d.department
FROM employees e
INNER JOIN departments d
ON e.department_id = d.id;
```
- A **LEFT JOIN** returns every row from the left table and matching rows from the right.
- A **RIGHT JOIN** returns every row from the right table and matching rows from the left.
- A **FULL JOIN** returns rows from both tables, including unmatched rows.
- A **CROSS JOIN** creates every possible combination of rows.
- A **SELF JOIN** joins a table with itself.

Easy to remember:
```text
INNER → Matching rows
LEFT  → Everything on the left
RIGHT → Everything on the right
FULL  → Everything from both
```
## 4. Aggregations and Filters
Aggregate functions perform calculations using multiple rows.
`COUNT()` counts rows.
`SUM()` calculates a total.
`AVG()` calculates an average.
`MIN()` finds the smallest value.
`MAX()` finds the largest value.
Example:
```sql
SELECT AVG(salary)
FROM employees;
```
`GROUP BY` puts rows into groups before an aggregate calculation.
Example:
```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```
`WHERE` filters individual rows before grouping.
Example:
```sql
SELECT *
FROM employees
WHERE salary > 50000;
```
`HAVING` filters groups after aggregation.
Example:
```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 2;
```
Easy difference: WHERE filters rows.
GROUP BY creates groups.
HAVING filters groups.
ORDER BY sorts the final results.
## 5. Normalization
Organizes tables to reduce duplicate data and avoid common data problems.
- **Primary key** → Uniquely identifies each row in a table.
- **Foreign key** → Connects one table to another using a related key.
- **1NF** (First Normal Form) → Each cell should contain only one value, not multiple values.
- **2NF** (Second Normal Form) → Removes partial dependencies, so non-key data depends on the complete key.
- **3NF** (Third Normal Form) → Removes transitive dependencies, so non-key data depends directly on the key.

Easy to remember:
```
1NF → Atomic values
2NF → No partial dependency
3NF → No transitive dependency
```
## 6. Indexes
An **index** is a database structure that helps find data faster. Without an index, the database may need to check many rows, while a useful index helps it find matching rows quickly, similar to using a book’s index to find a topic.


Example:
```sql
CREATE INDEX idx_employee_name
ON employees(name);
```
After creating the index, a search by name may become faster.
Example:
```sql
SELECT *
FROM employees
WHERE name = 'Rahul';
```
Indexes make data retrieval faster and can improve some sorting and join operations, but they use extra storage and can slow down INSERT, UPDATE, and DELETE operations. Too many indexes can reduce overall performance.

## 7. Transactions
A **transaction** is a group of database operations treated as one unit of work. For example, in a bank transfer, money is deducted from one account and added to another. If both operations succeed, the transaction is committed; if something fails, the transaction can be rolled back.

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
- `BEGIN` starts a transaction.
- `COMMIT` saves the transaction changes.
- `ROLLBACK` undoes uncommitted changes.
- `SAVEPOINT` creates a point that can be used for a partial rollback.

## 8. Locking Mechanism
**Locking** controls how multiple transactions access the same data and helps prevent lost updates or conflicting changes. A **shared lock** is used for reading and can be held by multiple transactions, while an **exclusive lock** is used when changing data and may make other conflicting operations wait.


Example in PostgreSQL:
```sql
SELECT *
FROM accounts
WHERE id = 1
FOR UPDATE;
```
`FOR UPDATE` locks the selected row for update.
A deadlock happens when transactions wait for each other.
Example:
```text
Transaction A → Locks Row 1 → Wants Row 2
Transaction B → Locks Row 2 → Wants Row 1
```
Neither transaction can continue normally while the circular wait remains.
The database can detect and resolve a deadlock.
Easy to remember: locking controls access to shared data.
## 9. Database Isolation Levels
- **Isolation levels** → Control what transactions can see.
- **READ COMMITTED** → Sees only committed data.
- **REPEATABLE READ** → Keeps a consistent view.
- **SERIALIZABLE** → Strongest isolation level.
- **Trade-off** → Higher isolation improves consistency but may reduce concurrency.
## 10. Triggers
A trigger is a database feature that automatically runs an action after a chosen event.
Common events are INSERT, UPDATE, and DELETE.
For example, a trigger can record salary changes in an audit table.
Example idea:
```text
UPDATE Employee
      ↓
   Trigger
      ↓
Insert record into Audit Table
```
In PostgreSQL, a trigger normally calls a trigger function.
Example:
```sql
CREATE TRIGGER employee_audit
AFTER UPDATE ON employees
FOR EACH ROW
EXECUTE FUNCTION log_employee_changes();
```
- **BEFORE** → Runs before the database operation and can validate or modify data before it is saved.
- **AFTER** → Runs after the operation is completed, commonly used for audit logs or related updates.
- **INSTEAD OF** → Runs instead of the original operation, mainly used with views.
- **ROW / STATEMENT** → ROW runs once for each affected row; STATEMENT runs once for the entire SQL statement.
## Reference

- PostgreSQL Documentation – Transaction Isolation  
   https://www.postgresql.org/docs/current/transaction-iso.html
- PostgreSQL Documentation – Indexes  
   https://www.postgresql.org/docs/current/indexes.html
- PostgreSQL Documentation – SQL SELECT and Joins  
   https://www.postgresql.org/docs/current/sql-select.html  

