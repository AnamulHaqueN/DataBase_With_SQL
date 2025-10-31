#  Intro to Databases with SQL 

## What is DBMS
> A collection of data organized for creating, reading, updating, and deleting.
## Database Management System
> Software via which we can interact with a database.
### Database Management software
- MySQL
- Oracle
- PostgreSQL
- SQLite

## SQL (Structured Query Language)
> A language via which you can create, read, update, and delete data in a database.

## SELECT
> The SELECT statement in SQL is used to retrieve data from a database.
> SELECT * means choose all columns from a table
```sql
SELECT * FROM students; -- means all columns
SELECT name, age FROM students; -- get only name and age columns
```

## LIMIT
> It is used to restrict the number of rows returned by a query. 

```sql
      SELECT * FROM customers LIMIT 10;
```

## WHERE
> It allows me not all rows but some rows base on conditions is true
```sql
SELECT * FROM students WHERE age >= 18 LIMIT 3;
```


## Conditional Operators in SQL

Conditional operators are used in SQL to **filter, compare, and make decisions** in queries.  
They are mainly used in the `WHERE` clause or in expressions like `CASE`.

---

### Comparison Operators

| Operator | Meaning | Example |
|----------|---------|---------|
| `=`      | Equal to | `WHERE age = 20` |
| `<>` or `!=` | Not equal to | `WHERE city <> 'Dhaka'` |
| `>`      | Greater than | `WHERE salary > 50000` |
| `<`      | Less than | `WHERE age < 30` |
| `>=`     | Greater than or equal | `WHERE age >= 18` |
| `<=`     | Less than or equal | `WHERE age <= 25` |

```sql
-- Select students aged 18 or older
SELECT * FROM students WHERE age >= 18;

-- Select employees not in Dhaka
SELECT * FROM employees WHERE city <> 'Dhaka';

### Logical Operators

> Logical operators combine multiple conditions:

>Operator	Meaning	Example

-AND	Both conditions must be true	WHERE age >= 18 AND city = 'Dhaka'
-OR	At least one condition is true	WHERE city = 'Dhaka' OR city = 'Rajshahi'
-NOT	Negates a condition	WHERE NOT city = 'Chittagong'

```sql
-- Students who are adults AND live in Dhaka
SELECT * FROM students WHERE age >= 18 AND city = 'Dhaka';

-- Employees living in either Dhaka or Rajshahi
SELECT * FROM employees WHERE city = 'Dhaka' OR city = 'Rajshahi';

```


### Special Operators
> Operator	Purpose	Example
- BETWEEN ... AND ...	Select values within a range	WHERE   age   BETWEEN 18 AND 25
- IN	Match a set of values	WHERE city IN ('Dhaka', 'Rajshahi')
- LIKE	Pattern matching	WHERE name LIKE 'A%'
  IS NULL	Check for empty value	WHERE email IS NULL

```sql
-- Students aged 18 to 25
SELECT * FROM students WHERE age BETWEEN 18 AND 25;

-- Students living in specific cities
SELECT * FROM students WHERE city IN ('Dhaka', 'Rajshahi');

-- Students whose name starts with A
SELECT * FROM students WHERE name LIKE 'A%';

-- Students with missing email
SELECT * FROM students WHERE email IS NULL;
```

### Conditional Expression (CASE)

> The CASE statement works like IF-ELSE in SQL to return values based on conditions.

```sql
SELECT name, age,
  CASE 
    WHEN age < 18 THEN 'Minor'
    WHEN age >= 18 THEN 'Adult'
  END AS category
FROM students;
```