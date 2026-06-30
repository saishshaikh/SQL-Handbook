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


