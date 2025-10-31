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


## SQL Clauses
> In SQL, a clause is a component of a SQL statement that performs a specific task. There are several main SQL clauses commonly used.

### Common SQL Clauses

`
Clause	Purpose
- SELECT	Retrieve data from one or more tables
- FROM	Specify the table(s) to query
- WHERE	Filter rows based on conditions
- ORDER BY	Sort the result set
- GROUP BY	Group rows that share a value
- HAVING	Filter groups (like WHERE but for grouped data)
- LIMIT / TOP	Limit the number of rows returned (depends on - SQL dialect)
- JOIN	Combine rows from multiple tables
- DISTINCT	Remove duplicate rows
- INSERT INTO	Add new rows into a table
- UPDATE	Modify existing rows
- DELETE	Delete rows from a table
- CREATE	Create tables or databases
- ALTER	Modify table structure
- DROP	Delete tables or databases

`



### SELECT
> The SELECT statement in SQL is used to retrieve data from a database.
> SELECT * means choose all columns from a table
```sql
SELECT * FROM students; -- means all columns
SELECT name, age FROM students; -- get only name and age columns
```

### LIMIT
> It is used to restrict the number of rows returned by a query. 

```sql
      SELECT * FROM customers LIMIT 10;
```

### WHERE
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
- IS NULL	Check for empty value	WHERE email IS NULL


```sql
-- Students aged 18 to 25
SELECT * FROM students WHERE age BETWEEN 18 AND 25;

-- Students living in specific cities
SELECT * FROM students WHERE city IN ('Dhaka', 'Rajshahi');

-- Students with missing email
SELECT * FROM students WHERE email IS NULL;
```


#### SQL LIKE Operator

- LIKE is used in a WHERE clause to match patterns in string data.

> There are two special wildcards:
- `%	- Zero or more characters	'A%' matches Amin, Ali`
- `_	- Exactly one character	'A_i_' matches Amin, Avid`

```sql
-- Names starting with A
SELECT * FROM students WHERE name LIKE 'A%';

-- Names containing "mi" anywhere
SELECT * FROM students WHERE name LIKE '%mi%';

-- Names with 4 letters, starting with A
SELECT * FROM students WHERE name LIKE 'A___';

-- Names starting with A, 4 or more letters, third letter is 'i'
SELECT * FROM students WHERE name LIKE 'A_i%';

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


## SQL ORDER BY Clause

> ORDER BY is used to sort the result set of a query by one or more columns.

- Default sorting is ascending (ASC).

- You can also sort descending (DESC).

<p>Sort by one column (descending)</p>

```sql
SELECT name, age, city
FROM students
ORDER BY age DESC;

```

<p>Sort by multiple columns</p>

```sql
-- Sort students by city first, then by age within each city
SELECT name, age, city
FROM students
ORDER BY city ASC, age DESC
LIMIT 5;

```


## SQL Aggregate Functions

> Aggregate functions perform a calculation on a set of values and return a single value. They are often used with GROUP BY, but can also be used alone.

<p> Common SQL Aggregate Functions </p>

<p> 1. COUNT() – Counts the number of rows. </p>

```sql
SELECT COUNT(*) AS total_students
FROM students;
```

<p> 2. SUM() – Adds up numeric values. </p>

```sql
SELECT SUM(salary) AS total_salary
FROM employees;
```

<p> 3. AVG() – Calculates the average of numeric values. </p>

```sql
SELECT AVG(age) AS avg_age
FROM students;
```

<p> 4. MIN() – Finds the minimum value. </p>

```sql
SELECT MIN(age) AS youngest_student
FROM students;
```

<p> 5. MAX() – Finds the maximum value. </p>

```sql
SELECT MAX(age) AS oldest_student
FROM students;
```

<p> Using Aggregate Functions with GROUP BY </p>

If you want summaries per category, you can combine aggregates with GROUP BY.

Example:

```sql
SELECT class, COUNT(*) AS total_students, AVG(age) AS avg_age
FROM students
GROUP BY class;
```

Result: For each class, you get the number of students and the average age.

Important Notes

> Aggregate functions ignore NULLs (except COUNT(*)).
You can use HAVING to filter after aggregation:

```sql
SELECT class, COUNT(*) AS total_students
FROM students
GROUP BY class
HAVING COUNT(*) > 10;
```

`HAVING is like WHERE but works after aggregation.`


## SQL DISTINCT Clause

> The DISTINCT clause is used to remove duplicate rows from the result set of a SELECT query.
It ensures that only unique values appear in the output.

Example: Without vs With DISTINCT

```sql
-- Without DISTINCT
SELECT city FROM students;

-- With DISTINCT
SELECT DISTINCT city FROM students;
```