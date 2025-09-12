# Chapter 20 – SQLite

## Sections
1. Preparation  
2. Database Access with SQLite  

---

## Summary
This chapter explains how to use **SQLite** databases with PHP.  
SQLite is a **lightweight, file-based database**, ideal for small to medium projects or for testing purposes.

---

## Key Concepts

### 1. Preparation
- Ensure **SQLite extension** is enabled in PHP (`pdo_sqlite` or `sqlite3`).  
- SQLite databases are stored in a **single file**.  
- No separate server installation is required.  

### 2. Database Access with SQLite

#### Using the SQLite3 Class
```php
// Open or create a database file
$db = new SQLite3('testdb.sqlite');

// Create a table
$db->exec("CREATE TABLE IF NOT EXISTS employees (id INTEGER PRIMARY KEY, name TEXT, position TEXT)");

// Insert data
$db->exec("INSERT INTO employees (name, position) VALUES ('Alice', 'Developer')");

// Query data
$result = $db->query("SELECT * FROM employees");
while ($row = $result->fetchArray(SQLITE3_ASSOC)) {
    echo $row['name'] . " - " . $row['position'];
}

// Close the connection
$db->close();
```

#### Using PDO with SQLite

```php
$pdo = new PDO('sqlite:testdb.sqlite');
$pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

// Create table
$pdo->exec("CREATE TABLE IF NOT EXISTS employees (id INTEGER PRIMARY KEY, name TEXT, position TEXT)");

// Insert data using prepared statements
$stmt = $pdo->prepare("INSERT INTO employees (name, position) VALUES (:name, :position)");
$stmt->execute([':name' => 'Bob', ':position' => 'Designer']);

// Query data
foreach ($pdo->query("SELECT * FROM employees") as $row) {
    echo $row['name'] . " - " . $row['position'];
}
```

---

## Advantages & Notes

* **No server required**: Works directly on the database file.
* **Lightweight**: Excellent for testing or small apps.
* **PDO support**: Allows switching between SQLite and other databases easily.
* **Limitations**: Not suitable for very large applications or high-concurrency environments.