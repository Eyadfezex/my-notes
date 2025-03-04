# Lateral Joins in PostgreSQL

A **Lateral Join** is a special type of join in PostgreSQL that allows a subquery to reference columns from the main table in the same query. It’s like running a mini-query for each row of the main table, which makes it super flexible for dynamic calculations and row-specific logic. Below are examples of lateral joins along with their expected responses.

---

## Example 1: Get Top Salary for Each Employee

**Query**:

```sql
SELECT e.employee_id, e.name, s.salary
FROM employees e,
LATERAL (
    SELECT salary
    FROM salaries
    WHERE employee_id = e.employee_id
    ORDER BY salary DESC
    LIMIT 1
) AS s;
```

**Response**:

| employee_id | name    | salary |
| ----------- | ------- | ------ |
| 1           | Alice   | 90000  |
| 2           | Bob     | 85000  |
| 3           | Charlie | 80000  |

- For each employee (`e`), the subquery finds their top salary and joins it with their details.

---

## Example 2: Generate Monthly Dates for Each Employee

**Query**:

```sql
SELECT e.employee_id, e.name, d.date
FROM employees e,
LATERAL (
    SELECT generate_series(e.hire_date, CURRENT_DATE, '1 month') AS date
) AS d;
```

**Response**:

| employee_id | name  | date       |
| ----------- | ----- | ---------- |
| 1           | Alice | 2022-01-01 |
| 1           | Alice | 2022-02-01 |
| 2           | Bob   | 2021-05-01 |
| 2           | Bob   | 2021-06-01 |

- For each employee, the `generate_series` function creates a list of monthly dates starting from their hire date.

---

## Example 3: Extract JSON Data

**Query**:

```sql
SELECT o.order_id, i.item_id, i.item_name, i.quantity
FROM orders o,
LATERAL (
    SELECT *
    FROM jsonb_to_recordset(o.items) AS i(item_id INT, item_name TEXT, quantity INT)
) AS i;
```

**Response**:

| order_id | item_id | item_name | quantity |
| -------- | ------- | --------- | -------- |
| 101      | 1       | Laptop    | 2        |
| 101      | 2       | Mouse     | 5        |
| 102      | 3       | Keyboard  | 1        |

- The `jsonb_to_recordset` function converts the JSONB array into rows.
- The lateral join lets the subquery use `o.items` for each order.

---

## Example 4: Calculate Running Totals

**Query**:

```sql
SELECT t.account_id, t.transaction_date, t.amount, rt.running_total
FROM transactions t,
LATERAL (
    SELECT SUM(amount) AS running_total
    FROM transactions
    WHERE account_id = t.account_id
      AND transaction_date <= t.transaction_date
) AS rt;
```

**Response**:

| account_id | transaction_date | amount | running_total |
| ---------- | ---------------- | ------ | ------------- |
| 1          | 2023-01-01       | 100    | 100           |
| 1          | 2023-01-02       | 200    | 300           |
| 2          | 2023-01-01       | 150    | 150           |

- For each transaction, the subquery calculates the running total by summing all previous transactions for the same account.

---

## When to Use Lateral Joins

1. **Row-Specific Logic**: When you need to perform calculations or lookups for each row.
2. **Dynamic Queries**: When the subquery depends on values from the main table.
3. **Complex Data**: When working with JSON, arrays, or hierarchical data.

---

## Performance Tips

- **Be Careful with Large Data**: Lateral joins run the subquery for each row, which can be slow for big datasets.
- **Use Indexes**: Make sure the subquery can use indexes to speed things up.
- **Test and Optimize**: Always check the performance for your specific use case.

---

## Lateral Join vs Regular Join

| Feature         | Lateral Join                        | Regular Join                           |
| --------------- | ----------------------------------- | -------------------------------------- |
| **Correlation** | Can use columns from the main table | Cannot use columns from the main table |
| **Execution**   | Runs for each row                   | Runs for the entire dataset            |
| **Use Case**    | Dynamic, row-specific logic         | Static, set-based logic                |
