Step 1: Create a Database

CREATE DATABASE startersql;
Right-click it in MySQL Workbench and select “Set as Default Schema”, or
Use this SQL command:
USE startersql



Step 2: Create a Table

Now we’ll create a simple 

CREATE TABLE users (
users table:
id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    gender ENUM('Male', 'Female', 'Other'),
    date_of_birth DATE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP

);


Step 3: Drop the Database
You can delete the entire database (and all its tables) using:
DROP DATABASE startersql;
Be careful — this will delete everything in that database.









