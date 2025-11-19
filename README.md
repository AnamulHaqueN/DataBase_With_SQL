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


DataBase Relationship, ISBN, 
Id, primary key, foreign key, subqueries
IN, ON, JOIN, Left join, right join, NATURAL JOIN,
Sets, INTERSECT, UNION, EXCEPT, GROUPS, GROUPED BY,
HAVING, COLUMN Contrains






























____________________________________________

# Basic SQL Command

```sql
create database if not exists student;
use student;
create table student (
  id INT PRIMARY KEY,
  name VARCHAR(255)
);
INSERT INTO student values(1, 'anamul');
Insert Into student values(2, 'khalid');
SELECT * FROM student;
```


```sql
create database drg;

show databases;

use drg;


create table worker(
worker_id int not null auto_increment primary key,
first_name varchar(25),
last_name char(25),
salary int,
joining_date DATETIME,
department char(25)
);
drop table worker;

INSERT INTO worker (first_name, last_name, salary, joining_date, department) VALUES
('John', 'Doe', 50000, '2020-01-15 09:30:00', 'IT'),
('Jane', 'Smith', 60000, '2019-03-10 10:00:00', 'HR'),
('Michael', 'Johnson', 55000, '2021-07-22 11:15:00', 'Finance'),
('Emily', 'Davis', 48000, '2020-05-18 09:45:00', 'Marketing'),
('William', 'Brown', 62000, '2018-11-02 08:30:00', 'IT'),
('Olivia', 'Jones', 53000, '2022-01-05 10:30:00', 'HR'),
('James', 'Garcia', 59000, '2019-08-12 09:00:00', 'Finance'),
('Sophia', 'Miller', 51000, '2021-04-28 10:15:00', 'Marketing'),
('Benjamin', 'Wilson', 57000, '2020-09-14 09:30:00', 'IT'),
('Ava', 'Moore', 54000, '2019-12-01 11:00:00', 'HR'),
('Lucas', 'Taylor', 60000, '2021-06-19 08:45:00', 'Finance'),
('Mia', 'Anderson', 52000, '2020-03-23 09:15:00', 'Marketing'),
('Alexander', 'Thomas', 61000, '2018-07-30 10:30:00', 'IT'),
('Isabella', 'Jackson', 53000, '2022-02-14 09:45:00', 'HR'),
('Ethan', 'White', 58000, '2019-05-20 10:00:00', 'Finance'),
('Charlotte', 'Harris', 50000, '2020-08-10 09:30:00', 'Marketing'),
('Daniel', 'Martin', 59000, '2018-12-25 08:30:00', 'IT'),
('Amelia', 'Thompson', 54000, '2021-03-12 10:15:00', 'HR'),
('Matthew', 'Garcia', 60000, '2019-10-05 09:45:00', 'Finance'),
('Harper', 'Martinez', 52000, '2020-06-17 09:00:00', 'Marketing');

select * from worker;


create table bonus(
worker_ref_id int,
bonus_date DATETIME,
foreign key (worker_ref_id) references worker(worker_id) on delete cascade);
insert into bonus (worker_ref_id,bonus_date) values
(1, '2020-12-25 10:00:00'),
(1, '2021-12-25 10:00:00'),
(2, '2019-12-31 09:30:00'),
(2, '2020-12-31 09:30:00'),
(3, '2021-01-15 11:00:00'),
(3, '2022-01-15 11:00:00'),
(4, '2020-06-30 10:15:00'),
(5, '2019-11-15 09:45:00'),
(5, '2020-11-15 09:45:00'),
(6, '2022-03-01 10:30:00'),
(7, '2020-08-20 09:00:00'),
(8, '2021-05-10 10:15:00'),
(9, '2020-12-01 09:30:00'),
(10, '2019-12-25 10:00:00'),
(11, '2021-06-30 08:45:00'),
(12, '2020-03-31 09:15:00'),
(13, '2018-12-31 10:30:00'),
(14, '2022-02-14 09:45:00'),
(15, '2020-05-20 10:00:00'),
(16, '2020-08-10 09:30:00'),
(17, '2018-12-25 08:30:00'),
(18, '2021-03-12 10:15:00'),
(19, '2019-10-05 09:45:00'),
(20, '2020-06-17 09:00:00');


create table title(
worker_ref_id int,
worker_title char(25),
affected_from DATETIME,
foreign key (worker_ref_id) references worker(worker_id) on delete cascade);


INSERT INTO title (worker_ref_id, worker_title, affected_from) VALUES
(1, 'Software Engineer', '2020-01-15 09:30:00'),
(2, 'HR Manager', '2019-03-10 10:00:00'),
(3, 'Finance Analyst', '2021-07-22 11:15:00'),
(4, 'Marketing Executive', '2020-05-18 09:45:00'),
(5, 'IT Specialist', '2018-11-02 08:30:00'),
(6, 'HR Executive', '2022-01-05 10:30:00'),
(7, 'Financial Officer', '2019-08-12 09:00:00'),
(8, 'Marketing Manager', '2021-04-28 10:15:00'),
(9, 'IT Administrator', '2020-09-14 09:30:00'),
(10, 'HR Coordinator', '2019-12-01 11:00:00'),
(11, 'Finance Manager', '2021-06-19 08:45:00'),
(12, 'Marketing Analyst', '2020-03-23 09:15:00'),
(13, 'IT Consultant', '2018-07-30 10:30:00'),
(14, 'HR Director', '2022-02-14 09:45:00'),
(15, 'Financial Planner', '2020-05-20 10:00:00'),
(16, 'Marketing Lead', '2020-08-10 09:30:00'),
(17, 'IT Support', '2018-12-25 08:30:00'),
(18, 'HR Officer', '2021-03-12 10:15:00'),
(19, 'Finance Executive', '2019-10-05 09:45:00'),
(20, 'Marketing Coordinator', '2020-06-17 09:00:00');
select * from title;

select first_name as worker_name from worker;

select upper(first_name) as worker_name from worker;
select * from worker;

select  department from worker group by department;

select count(*) as Number_of_Person,department, avg(salary) from worker group by department;




select * from worker where first_name='Sophia';
select instr(first_name,'I') from worker where first_name='Sophia';


select LTRIM(first_name) from worker;
```

## Which Language SQL Engines Are Written In?

> SQL is a high-level declarative language.
The database engine (written in C/C++) converts SQL into efficient machine operations.

## SQL vs C/C++ — Which Is Faster?

> C and C++ are far faster than SQL, because they are low-level, compiled languages that run directly on the CPU.

SQL, however:

- is a high-level **declarative language**  
- runs inside a database engine written in **C/C++**  
- cannot control memory, CPU, threads, pointers, or hardware  
- cannot outperform the language it is implemented in  

So raw computing speed:  
🏆 **C/C++ >>> SQL**


## Then why does SQL feel fast?

> Because the database engine (written in C/C++) does the heavy lifting.

SQL itself is **NOT** fast.  
The database engine is fast.  

SQL is fast for **data queries**, not for computation.  

SQL is extremely fast at:

- ✅ Searching  
- ✅ Filtering  
- ✅ Joining tables  
- ✅ Sorting  
- ✅ Indexing  

But C/C++ is faster at:

- ⚡ Loops  
- ⚡ Math / computation  
- ⚡ Memory operations  
- ⚡ Algorithms  
- ⚡ Real-time systems

## Why Indexing Important in DBMS ?
> Indexing is one of the most important concepts in DBMS because it dramatically improves query performance

## What is an Index?
- An index is a data structure that allows the database to find rows without scanning the entire table.

- Think of it like an index in a book: instead of reading every page to find a topic, you check the index and jump directly to the page.

Common types of indexes:

- B+ Tree index → most common, used for range queries

- Hash index → very fast for exact matches


## Why Indexing is Important
### a) Faster Search
Without index:
```sql
SELECT * FROM employees WHERE employee_id = 1001;
```
- DB scans every row → O(n) time

With index:

- DB can directly locate the row → O(log n) time for B+ Tree

### b) Efficient Sorting

Indexes store data in sorted order (for B+ Trees), which helps with:

- ORDER BY
- GROUP BY
- DISTINCT

No need to sort the entire table manually → faster query execution

### c) Faster Joins
Indexes on foreign keys help join operations.
Example:

```sql
SELECT * 
FROM orders o 
JOIN customers c ON o.customer_id = c.customer_id;
```
- If customer_id is indexed → join is much faster

### d) Helps with Uniqueness

- PRIMARY KEY and UNIQUE automatically create indexes
- Ensures data integrity efficiently

### e) Reduces Disk I/O

- Without index → full table scan → many disk reads
- With index → directly jump to required rows → fewer disk accesses

## 3 Drawbacks of Indexing

⚠️ Indexing is not free:

- Extra storage → indexes take disk space
- Slower writes → INSERT, UPDATE, DELETE need to update indexes too
- Too many indexes → can slow down updates and inserts

## Example
```sql
-- Create index on employee_id
CREATE INDEX idx_employee_id ON employees(employee_id);

-- Query becomes faster
SELECT * FROM employees WHERE employee_id = 1001;
```

Key Idea:
Indexing improves read performance significantly but can slow down writes. So choose indexes carefully based on query patterns.

## Simple Rule-of-Thumb
## ✔️ Add an index if:

- Query time becomes slow
- Column is used in WHERE
- Column is used in JOIN
- Column sorts data (ORDER BY)
- Column has high uniqueness

## ❌ Do NOT add an index if:

- Table is small
- Column changes very often
- Column has only a few possible values

## Where are indexes stored in our system?**

Indexes are not stored separately as files you see manually.
They are stored inside the database’s storage engine, automatically managed by MySQL/PostgreSQL.


## How Indexes Work to Search Values

> Indexes are special data structures (usually B-Trees or Hash Tables) that help the database find rows quickly without scanning the whole table.

1. Index as a Lookup Table
Think of an index like a sorted map:
```sql
Value   → Row location
101     → Row 5
102     → Row 1
105     → Row 8
```
- The database doesn’t scan the full table.
- It directly goes to the pointer in the index to find the row.

2. Common Index Types
a) B-Tree Index (most common)

Values are stored in a balanced tree.

Leaf nodes contain row pointers.

Searching is logarithmic O(log n).

Example: Search email = 'abc@example.com'

Start at root node.

Compare email value.

Go left or right depending on comparison.

Reach the leaf node → row pointer → fetch actual data.

b) Hash Index

Values are stored with a hash function.

Lookup is constant time O(1).

Good for exact matches (WHERE column = value), not ranges (BETWEEN).

c) Full-text Index

Specialized for text search.

Breaks text into words and maps them to row locations.

Used for MATCH...AGAINST queries.

3. Step-by-Step Search Using B-Tree Index

Suppose a table users with 1,000,000 rows and an index on user_id
```sql
SELECT * FROM users WHERE user_id = 345678;
```
<b>Without index:</b> Full table scan → 1,000,000 comparisons.
<b>With index:</b>

- Start at root of B-tree.
- Compare 345678 with current node.
- Follow the correct branch.
- Repeat until reaching the leaf node.
- Leaf node contains pointer to the actual row.
- Fetch the row → much faster.

### 4. Why It’s Faster

- Table scan = O(n) → slow for large tables.
- B-tree search = O(log n) → fast even for millions of rows.
- Only relevant rows are fetched.

### 5. Behind the Scenes

- Index stores column values + pointer to row.
- Database optimizer automatically chooses the index if    it improves query performance.
- Leaf nodes can point directly to row data (InnoDB: clustered index) or row location (secondary index).

## Interview-ready Answer

- “When a database uses an index to search a value, it doesn’t scan the full table. Instead, it searches the index, which is usually a B-tree or hash table. The index maps column values to row locations. For a B-tree, the database starts at the root, traverses the tree using comparisons, reaches the leaf node, and fetches the row. This reduces search time from O(n) to O(log n), making queries much faster.”



________________________________________________

# Some advance database 

## Recursive query

```sql
with recursive Sequence as(
-- anchor query
Select
1 as Curent_number

UNION ALL

-- Recursive query
select 
Curent_number + 1
from Sequence
where Curent_number < 20
)

select * from Sequence;

```


```sql
-- Print even from 1 - 1000; 
WITH RECURSIVE PRIME AS (
-- Anchor query 
SELECT 
2 as EVEN

UNION ALL

-- Recursive query 
SELECT
EVEN + 2
FROM PRIME
WHERE EVEN < 1000
)

SELECT * FROM PRIME;

```






## Loop in sql

```sql
-- For loop TO print sequence

DELIMITER $$

CREATE PROCEDURE print_sequence()
BEGIN
	DECLARE i INT DEFAULT 2;
    
    CREATE TEMPORARY TABLE IF NOT EXISTS tmp_numbers(sequence INT); 
    myLoop: LOOP
         INSERT INTO tmp_numbers (sequence) VALUES(i);
         SET i = i + 3;
         
		IF i > 20 THEN
			   LEAVE myLoop;
		END IF;
    END LOOP;
    
END$$

DELIMITER ;

CALL print_sequence();
SELECT * FROM tmp_numbers;
DROP TEMPORARY TABLE IF EXISTS tmp_numbers;
DROP PROCEDURE IF EXISTS print_sequence;
```

Generate Prime no using Loop
```sql
DELIMITER $$
CREATE PROCEDURE prime_Gen()
BEGIN
    DECLARE i INT DEFAULT 2;
    DECLARE isPrime INT;
    DECLARE j INT DEFAULT 2;
    
    DROP TEMPORARY Table IF EXISTS primes;
    CREATE TEMPORARY Table primes(n INT);
    outer_loop: LOOP
        IF i > 1000 THEN
               LEAVE outer_loop;
		END IF;
        
		SET j = 2;
        SET isPrime = 1;
        inner_loop: LOOP
                   IF j >= i THEN
                         LEAVE inner_loop;
					END IF;
                    
                   IF MOD(i, j) = 0 THEN 
						SET isPrime = 0;
                        LEAVE inner_loop;
					END IF;
                    SET j = j + 1;
					END LOOP inner_loop;
                    
		IF isPrime = 1 THEN INSERT INTO primes (n) VALUES(i);
        END IF;
		SET i = i + 1;
	END LOOP outer_loop;
END$$
DELIMITER ;

call prime_Gen();
SELECT GROUP_CONCAT(n ORDER BY n SEPARATOR '&') FROM primes;
DROP TEMPORARY TABLE IF EXISTS prime;
DROP PROCEDURE IF EXISTS prime_Gen;
```



## Pivoting rows into columns with ranking
OLD Mathod

```sql
-- Step 1: Initialize row number variables for each occupation

SET @doctor_rn := 0;
SET @professor_rn := 0;
SET @singer_rn := 0;
SET @actor_rn := 0;

-- Step 2: Pivot table query
SELECT 
     MAX(CASE WHEN Occupation = 'Doctor' THEN Name END) AS Doctor, 
     MAX(CASE WHEN Occupation = 'Professor' THEN Name END) AS Professor,
     MAX(CASE WHEN Occupation = 'Singer' THEN Name END) AS Singer,
     MAX(CASE WHEN Occupation = 'Actor' THEN Name END) AS Actor
     
FROM (
	SELECT Name, Occupation, 
             CASE Occupation
				WHEN 'Doctor' THEN (@doctor_rn := @doctor_rn + 1)
                WHEN 'Professor' THEN (@professor_rn := @professor_rn + 1)
                WHEN 'Singer' THEN (@singer_rn := @singer_rn + 1)
                WHEN 'Actor' THEN (@actor_rn := @actor_rn + 1)
			END AS rn
		FROM OCCUPATIONS
        ORDER BY Occupation, Name 
	) AS ranked
    GROUP BY rn
    ORDER BY rn;
```

## CTE(commont Table Expression)

```sql
Pivoting rows into columns with ranking    
USING CTE 


WITH ranked AS(
	SELECT 
	   Name, 
	   Occupation, 
	   ROW_NUMBER() OVER(PARTITION BY Occupation ORDER BY Name) AS rn
	FROM OCCUPATIONS
)

SELECT 
	MAX(CASE WHEN Occupation = 'Doctor' THEN Name END) AS Doctor,
    MAX(CASE WHEN Occupation = 'Professor' THEN Name END) AS Professor,
    MAX(CASE WHEN Occupation = 'Singer' THEN Name END) AS Singer,
    MAX(CASE WHEN Occupation = 'Actor' THEN Name END) AS Actor
FROM ranked
GROUP BY rn
ORDER BY rn;

```