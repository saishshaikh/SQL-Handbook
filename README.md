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
