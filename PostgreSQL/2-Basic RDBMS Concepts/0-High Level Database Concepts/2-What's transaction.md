# What is a Transaction?

## Overview

A **transaction** is a sequence of operations performed on a database as a single logical unit of work. It ensures that a set of related changes to the database are executed in a way that maintains **data integrity** and **consistency**. Transactions are fundamental to database systems, enabling reliable and predictable behavior even in the face of errors or system failures.

---

## Key Properties of Transactions (ACID)

Transactions are defined by the **ACID** properties, which guarantee reliability and consistency:

1. **Atomicity**:

   - Ensures that a transaction is treated as a single, indivisible unit.
   - Either **all** operations in the transaction are completed, or **none** are.
   - Example: If a transaction involves transferring money between two accounts, both the debit and credit operations must succeed. If one fails, the entire transaction is rolled back.

2. **Consistency**:

   - Ensures that a transaction brings the database from one **valid state** to another.
   - All data must adhere to predefined rules (e.g., constraints, triggers) after the transaction.
   - Example: If a database has a rule that account balances cannot be negative, a transaction violating this rule will be aborted.

3. **Isolation**:

   - Ensures that concurrent transactions do not interfere with each other.
   - Each transaction operates as if it is the only one running, even if multiple transactions are executing simultaneously.
   - Example: If two transactions are updating the same data, one will wait for the other to complete before proceeding.

4. **Durability**:
   - Ensures that once a transaction is committed, its changes are permanent and survive system failures.
   - Example: After a successful transaction, the data is saved to disk and will not be lost even if the database crashes.

---

## Transaction States

A transaction goes through several states during its lifecycle:

1. **Active**: The transaction is executing.
2. **Partially Committed**: All operations are completed, but changes are not yet saved to disk.
3. **Committed**: Changes are permanently saved, and the transaction is complete.
4. **Failed**: An error occurs, and the transaction cannot proceed.
5. **Aborted**: The transaction is rolled back, and the database is restored to its state before the transaction started.

---

## Transaction Control Commands

Databases provide commands to manage transactions:

1. **BEGIN**: Starts a new transaction.
2. **COMMIT**: Saves all changes made during the transaction permanently.
3. **ROLLBACK**: Undoes all changes made during the transaction and restores the previous state.
4. **SAVEPOINT**: Creates a point within a transaction to which you can later roll back.
5. **SET TRANSACTION**: Configures transaction properties (e.g., isolation level).

---

## Example of a Transaction

Consider a banking system where money is transferred from Account A to Account B:

```sql
BEGIN; -- Start the transaction

UPDATE accounts SET balance = balance - 100 WHERE account_id = 'A'; -- Debit Account A
UPDATE accounts SET balance = balance + 100 WHERE account_id = 'B'; -- Credit Account B

COMMIT; -- Save changes permanently
```

- If both updates succeed, the transaction is **committed**.
- If either update fails, the transaction is **rolled back**, and no changes are applied.

---

## Importance of Transactions

1. **Data Integrity**: Ensures that the database remains in a consistent state.
2. **Error Recovery**: Provides mechanisms to undo changes in case of errors.
3. **Concurrency Control**: Manages simultaneous access to data by multiple users or applications.
4. **Reliability**: Guarantees that changes are permanent once committed.

---

## Real-World Use Cases

1. **Banking Systems**: Transferring funds between accounts.
2. **E-Commerce**: Processing orders and updating inventory.
3. **Reservation Systems**: Booking tickets or rooms.
4. **Inventory Management**: Updating stock levels.

---

## References

- Database System Concepts by Abraham Silberschatz, Henry F. Korth, and S. Sudarshan
- [PostgreSQL Documentation on Transactions](https://www.postgresql.org/docs/current/tutorial-transactions.html)
