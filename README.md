# SQL Basics

## Step 1: Create a Database

```sql
CREATE DATABASE startersql;

USE startersql;
```

In MySQL Workbench:

* Right-click the database
* Select **Set as Default Schema**

---

## Step 2: Create a Table

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    gender ENUM('Male', 'Female', 'Other'),
    date_of_birth DATE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## Step 3: Drop the Database

```sql
DROP DATABASE startersql;
```

⚠️ This will delete the entire database and all its tables.

---

# Data Types Explained

### INT

Used for whole numbers.

```sql
age INT
```

### VARCHAR(100)

Variable-length string up to 100 characters.

```sql
name VARCHAR(100)
```

### ENUM

Allows only predefined values.

```sql
gender ENUM('Male', 'Female', 'Other')
```

### DATE

Stores date values.

```sql
date_of_birth DATE
```

### TIMESTAMP

Stores date and time automatically.

```sql
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
```

### BOOLEAN

Stores TRUE or FALSE values.

```sql
is_active BOOLEAN
```

### DECIMAL(10,2)

Stores exact numeric values.

```sql
salary DECIMAL(10,2)
```

---

# Constraints Explained

### AUTO_INCREMENT

Automatically generates unique numbers.

```sql
id INT AUTO_INCREMENT
```

### PRIMARY KEY

Uniquely identifies each row.

```sql
id INT PRIMARY KEY
```

### NOT NULL

Does not allow NULL values.

```sql
name VARCHAR(100) NOT NULL
```

### UNIQUE

Prevents duplicate values.

```sql
email VARCHAR(100) UNIQUE
```

### DEFAULT

Assigns a default value if none is provided.

```sql
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
```

```sql
is_active BOOLEAN DEFAULT TRUE
```


# Working with Tables in MySQL

## Selecting Data from a Table

### Select All Columns

```sql
SELECT * FROM users;
```

Fetches all columns and all rows from the `users` table.

---

### Select Specific Columns

```sql
SELECT name, email FROM users;
```

Fetches only the `name` and `email` columns from all rows.

---

## Renaming a Table

### Rename Table

```sql
RENAME TABLE users TO customers;
```

---

### Rename Back

```sql
RENAME TABLE customers TO users;
```

---

## Altering a Table

The `ALTER TABLE` statement is used to modify an existing table.

### Add a Column

```sql
ALTER TABLE users
ADD COLUMN is_active BOOLEAN DEFAULT TRUE;
```

Adds a new column named `is_active`.

---

### Drop a Column

```sql
ALTER TABLE users
DROP COLUMN is_active;
```

Removes the `is_active` column.

---

### Modify a Column Type

```sql
ALTER TABLE users
MODIFY COLUMN name VARCHAR(150);
```

Changes the size of the `name` column from 100 to 150 characters.

---

### Move a Column to the First Position

```sql
ALTER TABLE users
MODIFY COLUMN email VARCHAR(100) FIRST;
```

Moves the `email` column to the first position in the table.

---

### Move a Column After Another Column

```sql
ALTER TABLE users
MODIFY COLUMN gender ENUM('Male', 'Female', 'Other') AFTER name;
```

Moves the `gender` column after the `name` column.

---

# Concepts Covered

* SELECT *
* SELECT Specific Columns
* RENAME TABLE
* ALTER TABLE
* ADD COLUMN
* DROP COLUMN
* MODIFY COLUMN
* FIRST
* AFTER



# MySQL CRUD Operations & Constraints

## Inserting Data into MySQL Tables

To add data into a table, we use the `INSERT INTO` statement.

### Insert Without Specifying Column Names (Full Row Insert)

This method requires you to provide values for all columns in order, except columns with default values or `AUTO_INCREMENT`.

```sql
INSERT INTO users VALUES
(1, 'Alice', 'alice@example.com', 'Female', '1995-05-14', DEFAULT);
```

**Note:** Not recommended if your table structure might change (e.g., new columns added later).

---

### Insert by Specifying Column Names (Best Practice)

This method is safer and more readable. You only insert into specific columns.

```sql
INSERT INTO users (name, email, gender, date_of_birth) VALUES
('Bob', 'bob@example.com', 'Male', '1990-11-23');
```

Or for multiple rows:

```sql
INSERT INTO users (name, email, gender, date_of_birth) VALUES
('Bob', 'bob@example.com', 'Male', '1990-11-23'),
('Charlie', 'charlie@example.com', 'Other', '1988-02-17');
```

The remaining columns like `id` (which is `AUTO_INCREMENT`) and `created_at` (which has a default) are automatically handled by MySQL.

---

### Insert Multiple Rows at Once

```sql
INSERT INTO users (name, email, gender, date_of_birth) VALUES
('Charlie', 'charlie@example.com', 'Other', '1988-02-17'),
('David', 'david@example.com', 'Male', '2000-08-09'),
('Eva', 'eva@example.com', 'Female', '1993-12-30');
```

This is more efficient than inserting rows one by one.

---

# Querying Data in MySQL using `SELECT`

The `SELECT` statement is used to query data from a table.

## Basic Syntax

```sql
SELECT column1, column2 FROM table_name;
```

To select all columns:

```sql
SELECT * FROM users;
```

---

## Filtering Rows with `WHERE`

### Equal To

```sql
SELECT * FROM users WHERE gender = 'Male';
```

### Not Equal To

```sql
SELECT * FROM users WHERE gender != 'Female';
```

or

```sql
SELECT * FROM users WHERE gender <> 'Female';
```

### Greater Than / Less Than

```sql
SELECT * FROM users WHERE date_of_birth < '1995-01-01';
```

```sql
SELECT * FROM users WHERE id > 10;
```

### Greater Than or Equal / Less Than or Equal

```sql
SELECT * FROM users WHERE id >= 5;
```

```sql
SELECT * FROM users WHERE id <= 20;
```

### Working with NULL

#### IS NULL

```sql
SELECT * FROM users WHERE date_of_birth IS NULL;
```

#### IS NOT NULL

```sql
SELECT * FROM users WHERE date_of_birth IS NOT NULL;
```

### BETWEEN

```sql
SELECT * FROM users WHERE date_of_birth BETWEEN '1990-01-01' AND '2000-12-31';
```

### IN

```sql
SELECT * FROM users WHERE gender IN ('Male', 'Other');
```

### LIKE (Pattern Matching)

Starts with A

```sql
SELECT * FROM users WHERE name LIKE 'A%';
```

Ends with a

```sql
SELECT * FROM users WHERE name LIKE '%a';
```

Contains 'li'

```sql
SELECT * FROM users WHERE name LIKE '%li%';
```

### AND / OR

```sql
SELECT * FROM users WHERE gender = 'Female' AND date_of_birth > '1990-01-01';
```

```sql
SELECT * FROM users WHERE gender = 'Male' OR gender = 'Other';
```

### ORDER BY

```sql
SELECT * FROM users ORDER BY date_of_birth ASC;
```

```sql
SELECT * FROM users ORDER BY name DESC;
```

### LIMIT

```sql
SELECT * FROM users LIMIT 5;
```

Top 5 rows

```sql
SELECT * FROM users LIMIT 10 OFFSET 5;
```

Skip first 5 rows, then get next 10

```sql
SELECT * FROM users LIMIT 5, 10;
```

Get 10 rows starting from the 6th row (Same as above)

```sql
SELECT * FROM users ORDER BY created_at DESC LIMIT 10;
```

---

## Quick Quiz

What does the following queries do?

```sql
SELECT * FROM users WHERE salary > 60000 ORDER BY created_at DESC LIMIT 5;
```

```sql
SELECT * FROM users ORDER BY salary DESC;
```

```sql
SELECT * FROM users WHERE salary BETWEEN 50000 AND 70000;
```

---

# UPDATE - Modifying Existing Data

The `UPDATE` statement is used to change values in one or more rows.

## Basic Syntax

```sql
UPDATE table_name
SET column1 = value1, column2 = value2
WHERE condition;
```

---

### Example: Update One Column

```sql
UPDATE users
SET name = 'Alicia'
WHERE id = 1;
```

This changes the name of the user with `id = 1` to "Alicia".

---

### Example: Update Multiple Columns

```sql
UPDATE users
SET name = 'Robert', email = 'robert@example.com'
WHERE id = 2;
```

---

### Without WHERE Clause (Warning)

```sql
UPDATE users
SET gender = 'Other';
```

This updates every row in the table. Be very careful when omitting the `WHERE` clause.

---

## Quick Quiz: Practice Your UPDATE Skills

Try answering or running these queries based on your `users` table.

### 1. Update the salary of user with `id = 5` to ₹70,000.

```sql
UPDATE users
SET salary = 70000
WHERE id = 5;
```

### 2. Change the name of the user with email `aisha@example.com` to `Aisha Khan`.

```sql
UPDATE users
SET name = 'Aisha Khan'
WHERE email = 'aisha@example.com';
```

### 3. Increase salary by ₹10,000 for all users whose salary is less than ₹60,000.

```sql
UPDATE users
SET salary = salary + 10000
WHERE salary < 60000;
```

### 4. Set the gender of user `Ishaan` to `Other`.

```sql
UPDATE users
SET gender = 'Other'
WHERE name = 'Ishaan';
```

### 5. Reset salary of all users to ₹50,000 (Careful - affects all rows).

```sql
UPDATE users
SET salary = 50000;
```

**Note:** This query will overwrite salary for every user. Use with caution!

---

# DELETE - Removing Data from a Table

The `DELETE` statement removes rows from a table.

## Basic Syntax

```sql
DELETE FROM table_name
WHERE condition;
```

---

### Example: Delete One Row

```sql
DELETE FROM users
WHERE id = 3;
```

### Delete Multiple Rows

```sql
DELETE FROM users
WHERE gender = 'Other';
```

### Delete All Rows (but keep table structure)

```sql
DELETE FROM users;
```

### Drop the Entire Table (use with caution)

```sql
DROP TABLE users;
```

This removes the table structure and all data permanently.

---

## Best Practices

* Always use `WHERE` unless you're intentionally updating/deleting everything.
* Consider running a `SELECT` with the same `WHERE` clause first to confirm what will be affected:

```sql
SELECT * FROM users WHERE id = 3;
```

* Always back up important data before performing destructive operations.

---

## Quick Quiz: Practice Your DELETE Skills

What will happen if you run these queries?

```sql
DELETE FROM users
WHERE salary < 50000;
```

```sql
DELETE FROM users
WHERE salary IS NULL;
```

---

# MySQL Constraints

Constraints in MySQL are rules applied to table columns to ensure the accuracy, validity, and integrity of the data.

---

## 1. UNIQUE Constraint

Ensures that all values in a column are different.

Example (during table creation):

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

Add `UNIQUE` using `ALTER TABLE`:

```sql
ALTER TABLE users
ADD CONSTRAINT unique_email UNIQUE (email);
```

---

## 2. NOT NULL Constraint

Ensures that a column cannot contain NULL values.

Example:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

Change an existing column to NOT NULL:

```sql
ALTER TABLE users
MODIFY COLUMN name VARCHAR(100) NOT NULL;
```

Make a column nullable again:

```sql
ALTER TABLE users
MODIFY COLUMN name VARCHAR(100) NULL;
```

---

## 3. CHECK Constraint

Ensures that values in a column satisfy a specific condition.

Example: Allow only dates of birth after Jan 1, 2000

```sql
ALTER TABLE users
ADD CONSTRAINT chk_dob CHECK (date_of_birth > '2000-01-01');
```

Naming the constraint (`chk_dob`) helps if you want to drop it later.

---

## 4. DEFAULT Constraint

Sets a default value for a column if none is provided during insert.

Example:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    is_active BOOLEAN DEFAULT TRUE
);
```

Add DEFAULT using `ALTER TABLE`:

```sql
ALTER TABLE users
ALTER COLUMN is_active SET DEFAULT TRUE;
```

---

## 5. PRIMARY KEY Constraint

Uniquely identifies each row. Must be `NOT NULL` and `UNIQUE`.

Example:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

Add later with `ALTER TABLE`:

```sql
ALTER TABLE users
ADD PRIMARY KEY (id);
```

---

## 6. AUTO_INCREMENT

Used with `PRIMARY KEY` to automatically assign the next number.

Example:

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100)
);
```

Each new row gets the next available integer value in `id`.

---

# Summary Table

| Constraint     | Purpose                                |
| -------------- | -------------------------------------- |
| UNIQUE         | Prevents duplicate values              |
| NOT NULL       | Ensures value is not NULL              |
| CHECK          | Restricts values using a condition     |
| DEFAULT        | Sets a default value                   |
| PRIMARY KEY    | Uniquely identifies each row           |
| AUTO_INCREMENT | Automatically generates sequential IDs |




# SQL Functions (MySQL)

SQL functions help you analyze, transform, or summarize data in your tables.

We’ll use the **`users`** table which includes:

- `id`
- `name`
- `email`
- `gender`
- `date_of_birth`
- `salary`
- `created_at`

---

# 1. Aggregate Functions

These return a single value from a set of rows.

## `COUNT()`

Count total number of users:

```sql
SELECT COUNT(*) FROM users;
```

Count users who are Female:

```sql
SELECT COUNT(*) FROM users WHERE gender = 'Female';
```

---

## `MIN()` and `MAX()`

Get the minimum and maximum salary:

```sql
SELECT MIN(salary) AS min_salary,
       MAX(salary) AS max_salary
FROM users;
```

---

## `SUM()`

Calculate total salary payout:

```sql
SELECT SUM(salary) AS total_payroll
FROM users;
```

---

## `AVG()`

Find average salary:

```sql
SELECT AVG(salary) AS avg_salary
FROM users;
```

---

## Grouping with `GROUP BY`

Average salary by gender:

```sql
SELECT gender,
       AVG(salary) AS avg_salary
FROM users
GROUP BY gender;
```

---

# 2. String Functions

## `LENGTH()`

Length of user names:

```sql
SELECT name,
       LENGTH(name) AS name_length
FROM users;
```

---

## `LOWER()` and `UPPER()`

Convert names to lowercase:

```sql
SELECT name,
       LOWER(name) AS lowercase_name
FROM users;
```

Convert names to uppercase:

```sql
SELECT name,
       UPPER(name) AS uppercase_name
FROM users;
```

---

## `CONCAT()`

Combine name and email:

```sql
SELECT CONCAT(name, ' <', email, '>') AS user_contact
FROM users;
```

---

# 3. Date Functions

## `NOW()`

Current date and time:

```sql
SELECT NOW();
```

---

## `YEAR()`, `MONTH()`, `DAY()`

Extract parts of `date_of_birth`.

### Birth Year

```sql
SELECT name,
       YEAR(date_of_birth) AS birth_year
FROM users;
```

### Birth Month

```sql
SELECT name,
       MONTH(date_of_birth) AS birth_month
FROM users;
```

### Birth Day

```sql
SELECT name,
       DAY(date_of_birth) AS birth_day
FROM users;
```

---

## `DATEDIFF()`

Find number of days between today and birthdate:

```sql
SELECT name,
       DATEDIFF(CURDATE(), date_of_birth) AS days_lived
FROM users;
```

---

## `TIMESTAMPDIFF()`

Calculate age in years:

```sql
SELECT name,
       TIMESTAMPDIFF(YEAR, date_of_birth, CURDATE()) AS age
FROM users;
```

---

# 4. Mathematical Functions

## `ROUND()`, `FLOOR()`, `CEIL()`

```sql
SELECT salary,
       ROUND(salary) AS rounded,
       FLOOR(salary) AS floored,
       CEIL(salary) AS ceiled
FROM users;
```

---

## `MOD()`

Find even or odd user IDs:

```sql
SELECT id,
       MOD(id, 2) AS remainder
FROM users;
```

---

# 5. Conditional Functions

## `IF()`

```sql
SELECT name,
       gender,
       IF(gender = 'Female', 'Yes', 'No') AS is_female
FROM users;
```

---

# Summary Table

| Function | Purpose |
|----------|---------|
| `COUNT()` | Count rows |
| `SUM()` | Total of a column |
| `AVG()` | Average of values |
| `MIN()` / `MAX()` | Lowest / Highest value |
| `LENGTH()` | String length |
| `LOWER()` | Convert text to lowercase |
| `UPPER()` | Convert text to uppercase |
| `CONCAT()` | Merge strings |
| `NOW()` | Current date and time |
| `YEAR()` | Extract year from a date |
| `MONTH()` | Extract month from a date |
| `DAY()` | Extract day from a date |
| `DATEDIFF()` | Difference between two dates (days) |
| `TIMESTAMPDIFF()` | Difference between dates in a specified unit |
| `ROUND()` | Round a number |
| `FLOOR()` | Round down |
| `CEIL()` | Round up |
| `MOD()` | Find remainder |
| `IF()` | Conditional logic |



---

# 🔄 MySQL Transactions & AutoCommit

## What is AutoCommit?

By default, MySQL runs in **AutoCommit Mode**.

That means every SQL statement is treated as a separate transaction and is saved automatically.

If you want complete control over transactions, disable AutoCommit.

---

## Disable AutoCommit

```sql
SET autocommit = 0;
```

Now changes are **not permanent** until you execute:

```sql
COMMIT;
```

---

## COMMIT

Saves all changes permanently.

```sql
COMMIT;
```

Example

```sql
SET autocommit = 0;

UPDATE users
SET salary = 80000
WHERE id = 5;

COMMIT;
```

---

## ROLLBACK

Cancels all changes after the last COMMIT.

```sql
ROLLBACK;
```

Example

```sql
SET autocommit = 0;

UPDATE users
SET salary = 80000
WHERE id = 5;

ROLLBACK;
```

The salary returns to its previous value.

---

## Enable AutoCommit Again

```sql
SET autocommit = 1;
```

---

## Best Practices

- Use **COMMIT** only after verifying your changes.
- Use **ROLLBACK** when an error occurs.
- Disable AutoCommit while performing multiple related updates.

---

# 🔑 PRIMARY KEY

A **Primary Key** uniquely identifies every row in a table.

A Primary Key:

- Must be unique
- Cannot contain NULL values
- Identifies each row uniquely
- Can contain one or multiple columns
- Only one Primary Key is allowed per table

---

## Example

```sql
CREATE TABLE users(
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100)
);
```

---

# PRIMARY KEY vs UNIQUE

| Feature | PRIMARY KEY | UNIQUE |
|----------|-------------|---------|
| Unique Values | ✅ | ✅ |
| Allows NULL | ❌ | ✅ |
| Per Table | Only One | Multiple |
| Used as Main Identifier | ✅ | ❌ |

---

## UNIQUE Example

```sql
CREATE TABLE users(
    id INT AUTO_INCREMENT PRIMARY KEY,
    email VARCHAR(100) UNIQUE,
    name VARCHAR(100)
);
```

---

## Drop Primary Key

```sql
ALTER TABLE users
DROP PRIMARY KEY;
```

---

## Drop UNIQUE Constraint

```sql
ALTER TABLE users
DROP INDEX email;
```

---

# AUTO_INCREMENT

Automatically generates sequential values.

```sql
CREATE TABLE users(
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100)
);
```

Change starting value

```sql
ALTER TABLE users
AUTO_INCREMENT = 1000;
```

---

## Key Takeaways

- Primary Key uniquely identifies records.
- UNIQUE prevents duplicate values.
- AUTO_INCREMENT generates IDs automatically.

---

# 🔗 FOREIGN KEY

A Foreign Key creates a relationship between two tables.

It ensures that values exist in the referenced table.

---

## Example

### Users Table

```sql
CREATE TABLE users(
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100)
);
```

### Addresses Table

```sql
CREATE TABLE addresses(
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    street VARCHAR(255),
    city VARCHAR(100),
    state VARCHAR(100),
    pincode VARCHAR(10),

    FOREIGN KEY(user_id)
    REFERENCES users(id)
);
```

---

## Why Use Foreign Keys?

- Maintains data integrity
- Prevents invalid references
- Connects related tables

---

## Add Foreign Key Later

```sql
ALTER TABLE addresses
ADD CONSTRAINT fk_user
FOREIGN KEY(user_id)
REFERENCES users(id);
```

---

## Drop Foreign Key

```sql
ALTER TABLE addresses
DROP FOREIGN KEY fk_user;
```

---

# ON DELETE CASCADE

Automatically deletes child records when the parent record is deleted.

```sql
CREATE TABLE addresses(
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    street VARCHAR(255),

    CONSTRAINT fk_user
    FOREIGN KEY(user_id)
    REFERENCES users(id)
    ON DELETE CASCADE
);
```

---

# Other ON DELETE Options

| Option | Description |
|---------|-------------|
| CASCADE | Delete child records automatically |
| SET NULL | Set Foreign Key to NULL |
| RESTRICT | Prevent deleting parent record |

---

## Summary

- Foreign Keys maintain relationships.
- They improve data integrity.
- Use `ON DELETE CASCADE` when child records should also be deleted automatically.

---

# SQL JOINs in MySQL

## What is a JOIN?

A **JOIN** is used to combine rows from **two or more tables** based on a related column.

Generally, the relationship is created using:

- **Primary Key (PK)** in one table
- **Foreign Key (FK)** in another table

---

# Sample Tables

## users

| id | name |
|----|-------|
| 1 | Aarav |
| 2 | Sneha |
| 3 | Raj |

---

## addresses

| id | user_id | city |
|----|---------|---------|
| 1 | 1 | Mumbai |
| 2 | 2 | Kolkata |
| 3 | 4 | Delhi |

> **Note:** `user_id` is a Foreign Key that references `users.id`.

---

# 1. INNER JOIN

### Definition

Returns **only the matching rows** from both tables.

### Query

```sql
SELECT users.name,
       addresses.city
FROM users
INNER JOIN addresses
ON users.id = addresses.user_id;
```

### Output

| name | city |
|------|---------|
| Aarav | Mumbai |
| Sneha | Kolkata |

### Explanation

- Aarav → user_id = 1 ✅
- Sneha → user_id = 2 ✅
- Raj → No matching address ❌
- Delhi → user_id = 4 doesn't exist in `users` ❌

Only matching records are returned.

### Visual Representation

```
users               addresses

1 ------------- 1
2 ------------- 2
3

Result:
✔ Aarav - Mumbai
✔ Sneha - Kolkata
```

---

# 2. LEFT JOIN

### Definition

Returns:

- **All rows from the LEFT table**
- Matching rows from the RIGHT table
- If no match exists, NULL is returned.

### Query

```sql
SELECT users.name,
       addresses.city
FROM users
LEFT JOIN addresses
ON users.id = addresses.user_id;
```

### Output

| name | city |
|------|---------|
| Aarav | Mumbai |
| Sneha | Kolkata |
| Raj | NULL |

### Explanation

- Aarav → Match found ✅
- Sneha → Match found ✅
- Raj → No address → NULL

Every user appears.

### Visual Representation

```
users               addresses

1 ------------- 1
2 ------------- 2
3

Result:
✔ Aarav - Mumbai
✔ Sneha - Kolkata
✔ Raj - NULL
```

---

# 3. RIGHT JOIN

### Definition

Returns:

- **All rows from the RIGHT table**
- Matching rows from the LEFT table
- If no match exists, NULL is returned.

### Query

```sql
SELECT users.name,
       addresses.city
FROM users
RIGHT JOIN addresses
ON users.id = addresses.user_id;
```

### Output

| name | city |
|------|---------|
| Aarav | Mumbai |
| Sneha | Kolkata |
| NULL | Delhi |

### Explanation

- Mumbai → Match found ✅
- Kolkata → Match found ✅
- Delhi → user_id = 4 doesn't exist → NULL

Every address appears.

### Visual Representation

```
users               addresses

1 ------------- 1
2 ------------- 2
                4

Result:
✔ Aarav - Mumbai
✔ Sneha - Kolkata
✔ NULL - Delhi
```

---

# INNER JOIN vs LEFT JOIN vs RIGHT JOIN

| JOIN | Returns |
|-------|----------|
| INNER JOIN | Only matching rows from both tables |
| LEFT JOIN | All rows from the left table + matching rows from the right table |
| RIGHT JOIN | All rows from the right table + matching rows from the left table |

---

# Quick Interview Revision

### INNER JOIN

✅ Only matching records.

```
users ∩ addresses
```

---

### LEFT JOIN

✅ Everything from the left table.

```
users
+
matched addresses
```

Missing values become **NULL**.

---

### RIGHT JOIN

✅ Everything from the right table.

```
addresses
+
matched users
```

Missing values become **NULL**.

---

# Interview Tip

A simple way to remember:

- **INNER JOIN** → Only common records.
- **LEFT JOIN** → Keep everything from the **left** table.
- **RIGHT JOIN** → Keep everything from the **right** table.

---

# Summary

| JOIN Type | Includes Left Table | Includes Right Table | Unmatched Rows |
|------------|--------------------|----------------------|----------------|
| INNER JOIN | Only matched | Only matched | No |
| LEFT JOIN | All rows | Only matched | NULL on right |
| RIGHT JOIN | Only matched | All rows | NULL on left |

---



# SQL UNION, UNION ALL & SELF JOIN (MySQL)

---

# 1. UNION

## Definition

The `UNION` operator combines the result of **two or more SELECT statements** into a single result set.

✅ **Duplicate rows are removed automatically.**

---

## Syntax

```sql
SELECT column_name
FROM table1

UNION

SELECT column_name
FROM table2;
```

---

# Example Tables

## users

| id | name |
|----|------|
| 1 | Aarav |
| 2 | Sneha |
| 3 | Raj |
| 4 | Pooja |

---

## admin_users

| id | name |
|----|--------------|
| 101 | Anil Kumar |
| 102 | Pooja |
| 103 | Rakesh |
| 104 | Fatima |

---

# Example 1 — UNION

```sql
SELECT name
FROM users

UNION

SELECT name
FROM admin_users;
```

### Output

| name |
|------|
| Aarav |
| Sneha |
| Raj |
| Pooja |
| Anil Kumar |
| Rakesh |
| Fatima |

> If **Pooja** exists in both tables, it appears **only once** because `UNION` removes duplicates.

---

# 2. UNION ALL

## Definition

`UNION ALL` combines results from multiple `SELECT` statements **without removing duplicates**.

It is faster than `UNION` because SQL does not check for duplicate rows.

---

## Syntax

```sql
SELECT column_name
FROM table1

UNION ALL

SELECT column_name
FROM table2;
```

---

## Example

```sql
SELECT name
FROM users

UNION ALL

SELECT name
FROM admin_users;
```

### Output

| name |
|------|
| Aarav |
| Sneha |
| Raj |
| Pooja |
| Anil Kumar |
| Pooja |
| Rakesh |
| Fatima |

> Here **Pooja** appears **twice** because `UNION ALL` keeps duplicates.

---

# UNION with Multiple Columns

Both `SELECT` statements must return:

- Same number of columns
- Same order of columns
- Compatible data types

```sql
SELECT name, salary
FROM users

UNION

SELECT name, salary
FROM admin_users;
```

---

# Adding Custom Values

```sql
SELECT name,
       'User' AS role
FROM users

UNION

SELECT name,
       'Admin' AS role
FROM admin_users;
```

### Output

| name | role |
|------|-------|
| Aarav | User |
| Sneha | User |
| Raj | User |
| Anil Kumar | Admin |
| Pooja | Admin |

---

# ORDER BY with UNION

```sql
SELECT name
FROM users

UNION

SELECT name
FROM admin_users

ORDER BY name;
```

---

# Rules of UNION

- Both queries must return the **same number of columns**.
- Column data types must be compatible.
- `UNION` removes duplicates.
- `UNION ALL` keeps duplicates.
- `ORDER BY` is written only once, at the end of the final query.

---

# UNION vs UNION ALL

| UNION | UNION ALL |
|--------|-----------|
| Removes duplicate rows | Keeps duplicate rows |
| Slower | Faster |
| Performs duplicate checking | No duplicate checking |

---

# When to Use UNION

- Combining data from two similar tables.
- Current and archived records.
- Reports from multiple tables.
- Combining filtered results.

---

# Interview Question

### Difference between UNION and UNION ALL?

**UNION**
- Removes duplicate rows.
- Slower because duplicate checking is performed.

**UNION ALL**
- Keeps duplicate rows.
- Faster because no duplicate checking is performed.

---

# 3. SELF JOIN

## Definition

A **SELF JOIN** joins a table with itself.

It is useful when rows within the same table are related.

Examples:

- Employee → Manager
- Customer → Referrer
- Parent → Child

---

# Example Table

## users

| id | name | referred_by_id |
|----|------|----------------|
| 1 | Aarav | NULL |
| 2 | Sneha | 1 |
| 3 | Raj | 1 |
| 4 | Fatima | 2 |

---

# SELF JOIN Query

```sql
SELECT
    a.id,
    a.name AS user_name,
    b.name AS referred_by
FROM users a
LEFT JOIN users b
ON a.referred_by_id = b.id;
```

---

# Output

| id | user_name | referred_by |
|----|-----------|-------------|
| 1 | Aarav | NULL |
| 2 | Sneha | Aarav |
| 3 | Raj | Aarav |
| 4 | Fatima | Sneha |

---

# Explanation

`a`

- Represents the current user.

`b`

- Represents the person who referred that user.

The table is joined with itself using:

```sql
a.referred_by_id = b.id
```

---

# Why LEFT JOIN?

We use `LEFT JOIN` so users who were **not referred** are also displayed.

Example:

```
Aarav → NULL
```

If `INNER JOIN` were used, Aarav would not appear because `referred_by_id` is `NULL`.

---

# Visual Representation

```
users

id   name      referred_by_id

1    Aarav     NULL
2    Sneha     1
3    Raj       1
4    Fatima    2


SELF JOIN

Sneha  ----------> Aarav

Raj     ----------> Aarav

Fatima ----------> Sneha
```

---

# SELF JOIN vs INNER JOIN

| INNER JOIN | SELF JOIN |
|------------|-----------|
| Joins two different tables | Joins the same table |
| Uses PK–FK between tables | Uses relationship within the same table |
| Example: Employee & Department | Example: Employee & Manager |

---

# Quick Revision

## UNION

- Combines result sets.
- Removes duplicates.

---

## UNION ALL

- Combines result sets.
- Keeps duplicates.
- Faster.

---

## SELF JOIN

- Joins a table with itself.
- Uses aliases (`a`, `b`) to distinguish the two references.
- Commonly used for employee-manager or referral relationships.

---
# MySQL Views, Indexes & Subqueries

---

# MySQL Views

## What is a View?

A **View** is a virtual table created from the result of a `SELECT` query.

Unlike a normal table, a view **does not store data physically**. It always displays the latest data from the underlying table.

### Why Use Views?

- Simplify complex SQL queries.
- Reuse frequently used queries.
- Hide sensitive columns from users.
- Display filtered data.
- Create a live snapshot of data.

---

## Create a View

Suppose we want to display users whose salary is greater than ₹70,000.

```sql
CREATE VIEW high_salary_users AS
SELECT id, name, salary
FROM users
WHERE salary > 70000;
```

---

## Query the View

```sql
SELECT *
FROM high_salary_users;
```

### Example Output

| id | name | salary |
|----|-------|--------|
| 2 | Sneha | 75000 |
| 5 | Fatima | 80000 |

---

## Views Always Show Latest Data

### Before Update

```sql
SELECT * FROM high_salary_users;
```

| id | name | salary |
|----|-------|--------|
| 2 | Sneha | 75000 |
| 5 | Fatima | 80000 |

---

### Update Base Table

```sql
UPDATE users
SET salary = 72000
WHERE name = 'Raj';
```

---

### Query View Again

```sql
SELECT * FROM high_salary_users;
```

### New Output

| id | name | salary |
|----|-------|--------|
| 2 | Sneha | 75000 |
| 3 | Raj | 72000 |
| 5 | Fatima | 80000 |

Raj appears automatically because a **View always reflects the latest data** from the original table.

---

## Drop a View

```sql
DROP VIEW high_salary_users;
```

---

## Advantages of Views

- Acts like a saved `SELECT` query.
- Always shows updated data.
- Improves security by hiding columns.
- Makes queries easier to read.

---

## Interview Question

**Q. What is a View?**

**Answer:**

A View is a virtual table created using a `SELECT` statement. It does not store data physically and always displays the latest data from the underlying table.

---

# MySQL Indexes

## What is an Index?

An **Index** is a database object that improves the speed of retrieving records.

Think of it like the index of a book—it helps MySQL find data quickly.

---

## View Existing Indexes

```sql
SHOW INDEXES FROM users;
```

This displays all indexes created on the `users` table, including the Primary Key index.

---

## Create a Single-Column Index

```sql
CREATE INDEX idx_email
ON users(email);
```

### Example

```sql
SELECT *
FROM users
WHERE email = 'example@example.com';
```

Searching by `email` becomes much faster.

---

## Create a Multi-Column Index

```sql
CREATE INDEX idx_gender_salary
ON users(gender, salary);
```

### Example

```sql
SELECT *
FROM users
WHERE gender = 'Female'
AND salary > 70000;
```

This query can efficiently use the combined index.

---

## Index Order Matters

For an index on:

```sql
(gender, salary)
```

✅ Efficient

```sql
WHERE gender = 'Female'
AND salary > 70000;
```

❌ Less Efficient

```sql
WHERE salary > 70000;
```

Because the first indexed column (`gender`) is not used.

---

## Drop an Index

```sql
DROP INDEX idx_email
ON users;
```

---

## Advantages of Indexes

- Faster searching.
- Faster filtering.
- Faster joins.
- Faster sorting.

---

## Disadvantages of Indexes

- Uses additional disk space.
- Slows down `INSERT`, `UPDATE`, and `DELETE`.
- Should be created only on frequently searched columns.

---

## Interview Question

**Q. What is an Index?**

**Answer:**

An Index is a database object that speeds up data retrieval by creating a lookup structure for one or more columns.

---

# MySQL Subqueries

## What is a Subquery?

A **Subquery** is a query written inside another SQL query.

It helps solve complex problems by breaking them into smaller queries.

---

## Where Can Subqueries Be Used?

- `SELECT`
- `WHERE`
- `FROM`

---

# Scalar Subquery

A scalar subquery returns **only one value**.

### Example

```sql
SELECT id,
       name,
       salary
FROM users
WHERE salary >
(
    SELECT AVG(salary)
    FROM users
);
```

### Explanation

Inner Query:

```sql
SELECT AVG(salary)
FROM users;
```

Returns the average salary.

Outer Query:

Returns employees earning more than the average salary.

---

# Subquery with IN

```sql
SELECT id,
       name,
       referred_by_id
FROM users
WHERE referred_by_id IN
(
    SELECT id
    FROM users
    WHERE salary > 75000
);
```

### Explanation

The inner query returns IDs of users earning more than ₹75,000.

The outer query returns users referred by those users.

---

# Subquery in SELECT

```sql
SELECT name,
       salary,
(
    SELECT AVG(salary)
    FROM users
) AS average_salary
FROM users;
```

### Example Output

| name | salary | average_salary |
|-------|--------|----------------|
| Aarav | 60000 | 65000 |
| Sneha | 75000 | 65000 |
| Raj | 72000 | 65000 |

---

# Subquery in FROM

```sql
SELECT *
FROM
(
    SELECT dept_id,
           AVG(salary) AS avg_salary
    FROM users
    GROUP BY dept_id
) AS department_average;
```

The subquery acts like a temporary table.

---

# Types of Subqueries

| Type | Description |
|------|-------------|
| Scalar Subquery | Returns a single value |
| IN Subquery | Returns multiple values |
| Subquery in SELECT | Returns calculated values |
| Subquery in FROM | Acts as a temporary table |

---

# GROUP BY and HAVING in MySQL

The `GROUP BY` clause is used to group rows that have the same values in one or more columns. It is commonly used with aggregate functions such as `COUNT()`, `SUM()`, `AVG()`, `MIN()`, and `MAX()`.

The `HAVING` clause is used to filter grouped data after aggregation, similar to how `WHERE` filters individual rows before grouping.

---

# Example Table: `users`

| id | name   | gender | salary | referred_by_id |
| -- | ------ | ------ | ------ | -------------- |
| 1  | Aarav  | Male   | 80000  | NULL           |
| 2  | Sneha  | Female | 75000  | 1              |
| 3  | Raj    | Male   | 72000  | 1              |
| 4  | Fatima | Female | 85000  | 2              |
| 5  | Priya  | Female | 70000  | NULL           |

---

# GROUP BY Example – Average Salary by Gender

```sql
SELECT gender, AVG(salary) AS average_salary
FROM users
GROUP BY gender;
```

### Explanation

* Groups users based on the `gender` column.
* Calculates the average salary for each gender.

---

# GROUP BY with COUNT()

Find how many users were referred by each user.

```sql
SELECT referred_by_id, COUNT(*) AS total_referred
FROM users
WHERE referred_by_id IS NOT NULL
GROUP BY referred_by_id;
```

### Output

| referred_by_id | total_referred |
| -------------- | -------------- |
| 1              | 2              |
| 2              | 1              |

---

# HAVING Clause

Suppose we want to display only those genders whose average salary is greater than ₹75,000.

```sql
SELECT gender, AVG(salary) AS avg_salary
FROM users
GROUP BY gender
HAVING AVG(salary) > 75000;
```

### Why HAVING Instead of WHERE?

* `WHERE` filters rows **before** grouping.
* `HAVING` filters groups **after** `GROUP BY`.
* Aggregate functions like `AVG()` and `COUNT()` can be used only in `HAVING`.

---

# Another Example

Show users who referred more than one person.

```sql
SELECT referred_by_id, COUNT(*) AS total_referred
FROM users
WHERE referred_by_id IS NOT NULL
GROUP BY referred_by_id
HAVING COUNT(*) > 1;
```

---

# GROUP BY with ROLLUP

`ROLLUP` is used to generate subtotals and a grand total.

```sql
SELECT gender, COUNT(*) AS total_users
FROM users
GROUP BY gender WITH ROLLUP;
```

### Explanation

This query returns:

* Total users for each gender.
* A final row showing the grand total of all users.

---

# WHERE vs GROUP BY vs HAVING

| Clause   | Purpose                            | Aggregate Functions |
| -------- | ---------------------------------- | ------------------- |
| WHERE    | Filters rows before grouping       | ❌ No                |
| GROUP BY | Groups rows based on column values | N/A                 |
| HAVING   | Filters groups after aggregation   | ✅ Yes               |

---

#
---



# Stored Procedures, Triggers & More in MySQL

---

# Stored Procedures in MySQL

A **Stored Procedure** is a saved SQL program that can be executed whenever needed. It helps you reuse SQL logic such as queries, inserts, updates, deletes, or conditional statements.

---

# Why Change the Delimiter?

By default, MySQL uses `;` to end SQL statements.

Since a stored procedure contains multiple SQL statements ending with `;`, MySQL may think the procedure ends too early.

To avoid this, we temporarily change the delimiter.

Example:

```sql
DELIMITER $$
```

After creating the procedure, change it back.

```sql
DELIMITER ;
```

---

# Basic Syntax

```sql
DELIMITER $$

CREATE PROCEDURE procedure_name()
BEGIN
    -- SQL statements
END $$

DELIMITER ;
```

---

# Stored Procedure with Input Parameters

Suppose we want to insert a new user into the `users` table.

```sql
DELIMITER $$

CREATE PROCEDURE AddUser(
    IN p_name VARCHAR(100),
    IN p_email VARCHAR(100),
    IN p_gender ENUM('Male','Female','Other'),
    IN p_dob DATE,
    IN p_salary INT
)
BEGIN
    INSERT INTO users(name, email, gender, date_of_birth, salary)
    VALUES(p_name, p_email, p_gender, p_dob, p_salary);
END $$

DELIMITER ;
```

---

# Calling the Procedure

```sql
CALL AddUser(
    'Kiran Sharma',
    'kiran@example.com',
    'Female',
    '1994-06-15',
    72000
);
```

The procedure inserts a new record into the `users` table.

---

# Important Notes

* `IN` is used for input parameters.
* Stored procedures are stored inside the database.
* They can be executed multiple times.

---

# View Stored Procedures

```sql
SHOW PROCEDURE STATUS
WHERE Db='startersql';
```

---

# Drop a Stored Procedure

```sql
DROP PROCEDURE IF EXISTS AddUser;
```

---

# Summary

| Command                 | Purpose                                |
| ----------------------- | -------------------------------------- |
| `DELIMITER $$`          | Change statement delimiter temporarily |
| `CREATE PROCEDURE`      | Create a stored procedure              |
| `CALL procedure_name()` | Execute a procedure                    |
| `DROP PROCEDURE`        | Delete a procedure                     |

---

# Interview Questions

### What is a Stored Procedure?

A Stored Procedure is a saved SQL program that can be executed multiple times to perform database operations.

### Why do we use DELIMITER?

Because procedures contain multiple SQL statements ending with `;`. Changing the delimiter prevents MySQL from ending the procedure definition too early.

---

# Triggers in MySQL

A **Trigger** is a special stored program that executes automatically whenever a specified event occurs on a table.

Events include:

* INSERT
* UPDATE
* DELETE

---

# Why Use Triggers?

* Log database changes.
* Enforce business rules.
* Automatically update related tables.
* Maintain audit records.

---

# Basic Trigger Syntax

```sql
CREATE TRIGGER trigger_name

AFTER INSERT
ON table_name

FOR EACH ROW

BEGIN
    -- SQL statements
END;
```

---

# Trigger Types

Triggers can execute:

* BEFORE INSERT
* AFTER INSERT
* BEFORE UPDATE
* AFTER UPDATE
* BEFORE DELETE
* AFTER DELETE

---

# Example Scenario

Suppose we want to log every newly inserted user.

---

# Step 1: Create Log Table

```sql
CREATE TABLE user_log(

    id INT AUTO_INCREMENT PRIMARY KEY,

    user_id INT,

    name VARCHAR(100),

    created_on TIMESTAMP DEFAULT CURRENT_TIMESTAMP

);
```

---

# Step 2: Create Trigger

```sql
DELIMITER $$

CREATE TRIGGER after_user_insert

AFTER INSERT
ON users

FOR EACH ROW

BEGIN

    INSERT INTO user_log(user_id,name)

    VALUES(NEW.id,NEW.name);

END $$

DELIMITER ;
```

---

# Explanation

* `AFTER INSERT` → Trigger runs after inserting a row.
* `NEW` → Refers to the newly inserted row.
* User details are automatically inserted into `user_log`.

---

# Step 3: Test Trigger

```sql
CALL AddUser(
'Ritika Jain',
'ritika@example.com',
'Female',
'1996-03-12',
74000
);
```

Now check:

```sql
SELECT *
FROM user_log;
```

Ritika's information will be logged automatically.

---

# Drop Trigger

```sql
DROP TRIGGER IF EXISTS after_user_insert;
```

---

# Trigger Summary

| Component    | Description                          |
| ------------ | ------------------------------------ |
| BEFORE       | Runs before an event                 |
| AFTER        | Runs after an event                  |
| INSERT       | Fires on insert                      |
| UPDATE       | Fires on update                      |
| DELETE       | Fires on delete                      |
| NEW.column   | Refers to new values                 |
| OLD.column   | Refers to old values                 |
| FOR EACH ROW | Executes once for every affected row |

---

# More on MySQL

---

# 1. Logical Operators

Logical operators combine multiple conditions.

| Operator | Description                         | Example                            |
| -------- | ----------------------------------- | ---------------------------------- |
| AND      | All conditions must be true         | `salary > 50000 AND gender='Male'` |
| OR       | At least one condition must be true | `gender='Male' OR gender='Other'`  |
| NOT      | Reverses a condition                | `NOT gender='Female'`              |

---

# 2. Add a New Column

```sql
ALTER TABLE users

ADD COLUMN city VARCHAR(100);
```

Adds a new column named `city`.

---

# 3. Wildcard Operators

Used with the `LIKE` operator.

| Wildcard | Meaning                  | Example      |
| -------- | ------------------------ | ------------ |
| `%`      | Any number of characters | `LIKE 'A%'`  |
| `_`      | Exactly one character    | `LIKE '_a%'` |

---

# 4. LIMIT and OFFSET

Return selected rows after skipping some records.

```sql
SELECT *

FROM users

ORDER BY id

LIMIT 5 OFFSET 10;
```

Skips the first 10 rows and returns the next 5.

Alternative syntax:

```sql
SELECT *

FROM users

ORDER BY id

LIMIT 10,5;
```

---

# 5. DISTINCT

Returns unique values.

```sql
SELECT DISTINCT gender

FROM users;
```

---

# 6. TRUNCATE

Removes all rows while keeping the table structure.

```sql
TRUNCATE TABLE users;
```

**Advantages**

* Faster than `DELETE`.
* Keeps table structure.
* Resets auto-increment (in most databases).

---

# 7. CHANGE vs MODIFY

### CHANGE

Rename a column and change its datatype.

```sql
ALTER TABLE users

CHANGE COLUMN city location VARCHAR(150);
```

---

### MODIFY

Only changes the datatype.

```sql
ALTER TABLE users

MODIFY COLUMN salary BIGINT;
```

---

# CHANGE vs MODIFY

| CHANGE                        | MODIFY                          |
| ----------------------------- | ------------------------------- |
| Rename + datatype change      | Datatype change only            |
| Column name must be specified | Existing name remains unchanged |

---

# Quick Revision

### Stored Procedure

* Saved SQL block.
* Reusable.
* Executed using `CALL`.

### Trigger

* Executes automatically.
* Fires on INSERT, UPDATE, DELETE.
* Uses `NEW` and `OLD`.

### DISTINCT

Returns unique values.

### TRUNCATE

Deletes all rows but keeps the table.

### LIMIT OFFSET

Used for pagination.

### CHANGE

Rename column and datatype.

### MODIFY

Only changes datatype.

---

