# Chapter 18 – PDO (PHP Data Objects)

## Sections
1. Preparation  
2. Database Access via PDO  

---

## Summary
PDO (PHP Data Objects) is a **unified database access abstraction layer** in PHP.  
It provides a consistent API for working with different relational databases (MySQL, PostgreSQL, SQLite, etc.), while also supporting advanced features like prepared statements, transactions, and error handling.  

---

## Key Concepts

### 1. Preparation
- PDO must be enabled in the PHP installation (commonly pre-installed with modern PHP distributions).
- To use PDO, you create a **PDO object** by passing a **DSN (Data Source Name)**, username, and password.  
- General syntax:
  ```php
  $pdo = new PDO("driver:host=hostname;dbname=database", "username", "password");
  ```

### 2. Database Access via PDO

#### Establishing a Connection

```php
try {
    $pdo = new PDO("mysql:host=localhost;dbname=testdb;charset=utf8", "user", "password");
    // Set error handling mode
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    echo "Connection successful!";
} catch (PDOException $e) {
    echo "Connection failed: " . $e->getMessage();
}
```

#### Executing Queries

* **Simple query** (not recommended for user input):

  ```php
  $stmt = $pdo->query("SELECT * FROM employees");
  $employees = $stmt->fetchAll(PDO::FETCH_ASSOC);
  ```

#### Prepared Statements (Safe Against SQL Injection)

* **Insert with placeholders**:

  ```php
  $stmt = $pdo->prepare("INSERT INTO employees (name, position, salary) VALUES (?, ?, ?)");
  $stmt->execute(["Alice", "Developer", 55000.00]);
  ```

* **Named parameters**:

  ```php
  $stmt = $pdo->prepare("SELECT * FROM employees WHERE position = :position");
  $stmt->execute([":position" => "Developer"]);
  $rows = $stmt->fetchAll(PDO::FETCH_ASSOC);
  ```

#### Fetching Data

* `PDO::FETCH_ASSOC` → associative array
* `PDO::FETCH_NUM` → numeric array
* `PDO::FETCH_OBJ` → object
* Example:

  ```php
  while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {
      echo $row['name'] . " - " . $row['position'];
  }
  ```

#### Transactions

* Ensures multiple operations are executed atomically:

  ```php
  try {
      $pdo->beginTransaction();
      $pdo->exec("UPDATE accounts SET balance = balance - 100 WHERE id = 1");
      $pdo->exec("UPDATE accounts SET balance = balance + 100 WHERE id = 2");
      $pdo->commit();
  } catch (Exception $e) {
      $pdo->rollBack();
      echo "Transaction failed: " . $e->getMessage();
  }
  ```

---

## Advantages of PDO

* Database independence: same API for multiple RDBMS.
* Prepared statements prevent SQL injection.
* Advanced error handling and exceptions.
* Support for transactions.

---

## Common Pitfalls

* Forgetting to set `PDO::ERRMODE_EXCEPTION` → errors may go unnoticed.
* Mixing user input directly into queries instead of prepared statements.
* Not closing the connection properly (although PDO closes automatically when the object is destroyed).

---

## Notes & Reflections

* PDO is considered the **best practice** way to connect PHP applications to relational databases.
* In real-world frameworks (Laravel, Symfony), PDO is typically wrapped by ORMs like **Doctrine** or **Eloquent**.