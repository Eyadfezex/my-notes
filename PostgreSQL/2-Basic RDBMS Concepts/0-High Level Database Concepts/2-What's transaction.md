# Transactions in PostgreSQL

Transactions are a fundamental concept in PostgreSQL (and relational databases in general) that ensure data integrity and consistency. A transaction is a sequence of operations performed as a single logical unit of work. If all operations succeed, the transaction is committed, and changes are saved to the database. If any operation fails, the transaction is rolled back, and all changes are undone.

---

## Key Properties of Transactions (ACID)

PostgreSQL transactions adhere to the **ACID** properties:

1. **Atomicity**: Ensures that all operations within a transaction are treated as a single unit. Either all operations succeed, or none are applied.
2. **Consistency**: Ensures that the database remains in a valid state before and after the transaction.
3. **Isolation**: Ensures that concurrent transactions do not interfere with each other.
4. **Durability**: Ensures that once a transaction is committed, its changes are permanently saved, even in the event of a system failure.

---

## Transaction Commands in PostgreSQL

PostgreSQL provides the following commands to manage transactions:

1. **`BEGIN`**: Starts a new transaction block.
2. **`COMMIT`**: Saves the changes made during the transaction to the database.
3. **`ROLLBACK`**: Discards the changes made during the transaction and reverts to the previous state.
4. **`SAVEPOINT`**: Creates a point within a transaction to which you can later roll back.
5. **`ROLLBACK TO SAVEPOINT`**: Rolls back to a specific savepoint without ending the transaction.
6. **`RELEASE SAVEPOINT`**: Removes a savepoint so it can no longer be used.

---

## Basic Transaction Example

```sql
BEGIN; -- Start a transaction

UPDATE accounts SET balance = balance - 100 WHERE id = 1; -- Deduct $100 from account 1
UPDATE accounts SET balance = balance + 100 WHERE id = 2; -- Add $100 to account 2

COMMIT; -- Commit the transaction (save changes)
```

- If both `UPDATE` statements succeed, the transaction is committed, and the changes are saved.
- If either `UPDATE` fails, the transaction can be rolled back to undo the changes.

---

## Rolling Back a Transaction

```sql
BEGIN; -- Start a transaction

UPDATE accounts SET balance = balance - 100 WHERE id = 1; -- Deduct $100 from account 1
UPDATE accounts SET balance = balance + 100 WHERE id = 2; -- Add $100 to account 2

ROLLBACK; -- Roll back the transaction (discard changes)
```

- The `ROLLBACK` command undoes all changes made during the transaction.

---

## Using Savepoints

Savepoints allow you to create intermediate points within a transaction to which you can roll back without ending the entire transaction.

```sql
BEGIN; -- Start a transaction

UPDATE accounts SET balance = balance - 100 WHERE id = 1; -- Deduct $100 from account 1
SAVEPOINT my_savepoint; -- Create a savepoint

UPDATE accounts SET balance = balance + 100 WHERE id = 2; -- Add $100 to account 2

-- If something goes wrong, roll back to the savepoint
ROLLBACK TO SAVEPOINT my_savepoint;

COMMIT; -- Commit the transaction
```

- In this example, if the second `UPDATE` fails, you can roll back to `my_savepoint` without losing the first `UPDATE`.

---

## Nested Transactions

PostgreSQL does not support true nested transactions, but you can simulate them using savepoints.

```sql
BEGIN; -- Outer transaction

UPDATE accounts SET balance = balance - 100 WHERE id = 1; -- Deduct $100 from account 1
SAVEPOINT nested_transaction; -- Simulate a nested transaction

UPDATE accounts SET balance = balance + 100 WHERE id = 2; -- Add $100 to account 2

-- Roll back the nested transaction
ROLLBACK TO SAVEPOINT nested_transaction;

COMMIT; -- Commit the outer transaction
```

---

## Transaction Isolation Levels

PostgreSQL supports different isolation levels to control how transactions interact with each other:

1. **Read Uncommitted**: Allows dirty reads (not recommended).
2. **Read Committed**: Ensures that only committed data is read (default in PostgreSQL).
3. **Repeatable Read**: Ensures that if a transaction reads the same data multiple times, it will see the same values.
4. **Serializable**: Ensures complete isolation, as if transactions were executed one after the other.

To set an isolation level:

```sql
BEGIN TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

---

## Autocommit Mode

By default, PostgreSQL operates in **autocommit mode**, where each statement is treated as a separate transaction. To explicitly control transactions, you must use `BEGIN`, `COMMIT`, and `ROLLBACK`.

To disable autocommit in a session:

```sql
SET AUTOCOMMIT TO OFF;
```

---

## Best Practices for Transactions

1. **Keep transactions short**: Long-running transactions can lock resources and impact performance.
2. **Handle errors**: Use `ROLLBACK` to undo changes in case of errors.
3. **Use savepoints**: For complex transactions, use savepoints to manage partial rollbacks.
4. **Choose the right isolation level**: Select an isolation level that balances consistency and performance for your use case.

---

## Example: Error Handling in Transactions

```sql
BEGIN;

UPDATE accounts SET balance = balance - 100 WHERE id = 1; -- Deduct $100 from account 1
UPDATE accounts SET balance = balance + 100 WHERE id = 2; -- Add $100 to account 2

-- Check for errors
IF /* some condition */ THEN
    ROLLBACK; -- Roll back the transaction
ELSE
    COMMIT; -- Commit the transaction
END IF;
```
