# Chapter 17 – SQL

## Sections
1. Creating Databases and Tables  
2. Inserting Data  
3. Querying Data  
4. Updating Data  
5. Deleting Data  
6. Special Considerations  

---

## Summary
SQL (Structured Query Language) is the standard language for interacting with relational databases. PHP typically communicates with databases through extensions such as **PDO** or **MySQLi**. This chapter covers the basic CRUD (Create, Read, Update, Delete) operations and highlights peculiarities relevant when using SQL from PHP.

---

## Key Concepts

### 1. Creating Databases and Tables
- **Create a database**:
  ```sql
  CREATE DATABASE company_db;
  ```

* **Create a table**:

  ```sql
  CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    position VARCHAR(50),
    salary DECIMAL(10,2),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
  );
  ```

### 2. Inserting Data

* **Basic insertion**:

  ```sql
  INSERT INTO employees (name, position, salary)
  VALUES ('Alice', 'Developer', 55000.00);
  ```
* Multiple rows can be inserted in one statement.
* Always use **prepared statements** in PHP to avoid SQL injection.

### 3. Querying Data

* **Select all rows**:

  ```sql
  SELECT * FROM employees;
  ```
* **Filter with WHERE**:

  ```sql
  SELECT name, salary FROM employees WHERE position = 'Developer';
  ```
* **Sorting and limiting**:

  ```sql
  SELECT * FROM employees ORDER BY salary DESC LIMIT 5;
  ```

### 4. Updating Data

* **Update specific fields**:

  ```sql
  UPDATE employees
  SET salary = 60000.00
  WHERE name = 'Alice';
  ```
* Be careful: without a `WHERE` clause, all rows will be updated.

### 5. Deleting Data

* **Delete with condition**:

  ```sql
  DELETE FROM employees WHERE id = 5;
  ```
* **Delete all rows (use caution)**:

  ```sql
  DELETE FROM employees;
  ```

### 6. Special Considerations

* **NULL values**: represent missing or undefined data.
* **Indexes**: improve query performance but slow down inserts/updates.
* **Constraints**: enforce rules (e.g., `PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`).
* **Transactions**: group multiple queries into one atomic unit:

  ```sql
  START TRANSACTION;
  UPDATE accounts SET balance = balance - 100 WHERE id = 1;
  UPDATE accounts SET balance = balance + 100 WHERE id = 2;
  COMMIT;
  ```
* **SQL Injection risks**: never interpolate user input directly; always use prepared statements.

---

## Common Pitfalls

* Forgetting `WHERE` in `UPDATE` or `DELETE`.
* Not defining indexes → poor performance on large tables.
* Using unescaped user input → SQL injection vulnerabilities.
* Relying on database defaults instead of explicit schema definitions.

---

## Notes & Reflections

* Mastering CRUD operations is the foundation of backend programming.
* In real-world PHP projects, PDO is the recommended abstraction for working with databases.
* For better maintainability, use **migrations** (e.g., via Symfony, Laravel, or Doctrine) instead of manual SQL scripts.