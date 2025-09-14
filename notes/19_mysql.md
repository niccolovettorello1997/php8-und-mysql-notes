# Chapter 19 – MySQL

## Sections
1. Preparation  
2. Database Access with MySQL  
3. Settings  

---

## Summary
This chapter covers how to connect and interact with **MySQL** databases using PHP.  
It focuses on the **procedural MySQLi extension** and touches on configuration aspects.

---

## Key Concepts

### 1. Preparation
- Ensure **MySQL server** is installed and running.  
- PHP must have **MySQLi extension** enabled.  
- Typical connection credentials: host, username, password, database name.

### 2. Database Access with MySQL

#### Connecting to MySQL
- Procedural style:
  ```php
  $conn = mysqli_connect("localhost", "user", "password", "testdb");

  if (!$conn) {
      die("Connection failed: " . mysqli_connect_error());
  }
  echo "Connected successfully!";
  ```

* Object-oriented style:

  ```php
  $conn = new mysqli("localhost", "user", "password", "testdb");

  if ($conn->connect_error) {
      die("Connection failed: " . $conn->connect_error);
  }
  echo "Connected successfully!";
  ```

#### Executing Queries

* **Simple query**:

  ```php
  $result = mysqli_query($conn, "SELECT * FROM employees");

  while ($row = mysqli_fetch_assoc($result)) {
      echo $row['name'] . " - " . $row['position'];
  }
  ```
* **Prepared statements** (recommended for user input):

  ```php
  $stmt = $conn->prepare("INSERT INTO employees (name, position, salary) VALUES (?, ?, ?)");
  $stmt->bind_param("ssd", $name, $position, $salary);
  $name = "Alice";
  $position = "Developer";
  $salary = 55000.00;
  $stmt->execute();
  $stmt->close();
  ```

#### Closing the Connection

```php
mysqli_close($conn);
```

or for OOP:

```php
$conn->close();
```

### 3. Settings

* **Charset**: Set proper charset to avoid encoding issues:

  ```php
  mysqli_set_charset($conn, "utf8mb4");
  ```
* **Error reporting**: Check for errors after query execution:

  ```php
  if (mysqli_error($conn)) {
      echo "Error: " . mysqli_error($conn);
  }
  ```

---

## Advantages & Notes

* MySQLi provides both **procedural** and **object-oriented** interfaces.
* Prepared statements help prevent **SQL injection**.
* Most PHP applications today use **PDO** for database abstraction, but MySQLi remains widely used.