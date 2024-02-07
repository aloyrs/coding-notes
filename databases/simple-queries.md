## CREATE Query

```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    age INT
);
```

- Creates a new table named `employees` with columns `id`, `name`, and `age`.

## SELECT Query

```sql
SELECT * FROM employees;
```

- Retrieves all columns and rows from the `employees` table.

## UPDATE Query

```sql
UPDATE employees SET age = 35 WHERE name = 'John Doe';
```

- Modifies the `age` of the employee named 'John Doe' to 35.

## DELETE Query

```sql
DELETE FROM employees WHERE name = 'John Doe';
```

- Deletes the employee named 'John Doe' from the `employees` table.
