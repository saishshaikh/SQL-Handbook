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

