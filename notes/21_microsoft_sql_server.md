# Chapter 21 – Microsoft SQL Server

## Sections
1. Preparation  
2. Microsoft SQL Server Driver for PHP  
3. Usage  

---

## Summary
This chapter introduces how to connect PHP applications with **Microsoft SQL Server** using official drivers.  
Unlike MySQL or SQLite, SQL Server requires a specific **PHP extension/driver** and additional configuration.

---

## Key Concepts

### 1. Preparation
- Install Microsoft SQL Server on your machine or access a remote instance.  
- Enable the required PHP extension:  
  - `php_sqlsrv.dll` for Windows.  
  - Linux requires the **ODBC driver** (`msodbcsql`) and the **SQLSRV** / **PDO_SQLSRV** extensions.  
- Check installation with `phpinfo()` to confirm the driver is loaded.  

### 2. Microsoft SQL Server Driver for PHP
- Two main drivers are available:  
  - **SQLSRV**: Procedural and object-oriented API.  
  - **PDO_SQLSRV**: PDO-based API for consistency across databases.  

- Drivers must match:  
  - PHP version  
  - Thread-safety (TS/NTS)  
  - System architecture (x86/x64)  

### 3. Usage

#### Example with SQLSRV
```php
// Connection
$serverName = "localhost";
$connectionOptions = [
    "Database" => "testdb",
    "Uid" => "username",
    "PWD" => "password"
];
$conn = sqlsrv_connect($serverName, $connectionOptions);

// Check connection
if ($conn === false) {
    die(print_r(sqlsrv_errors(), true));
}

// Query
$sql = "SELECT id, name, role FROM employees";
$stmt = sqlsrv_query($conn, $sql);

while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
    echo $row['name'] . " - " . $row['role'];
}

// Close connection
sqlsrv_close($conn);
```

#### Example with PDO\_SQLSRV

```php
try {
    $pdo = new PDO("sqlsrv:Server=localhost;Database=testdb", "username", "password");
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

    // Insert
    $stmt = $pdo->prepare("INSERT INTO employees (name, role) VALUES (:name, :role)");
    $stmt->execute([':name' => 'Alice', ':role' => 'Developer']);

    // Select
    foreach ($pdo->query("SELECT * FROM employees") as $row) {
        echo $row['name'] . " - " . $row['role'];
    }
} catch (PDOException $e) {
    echo "Connection failed: " . $e->getMessage();
}
```

---

## Notes

* SQL Server integration is less common in PHP than MySQL/PostgreSQL, but still relevant in enterprise contexts.
* Prefer **PDO\_SQLSRV** if you want database abstraction and portability.
* Ensure proper **error handling** and **encoding (UTF-8)** setup to avoid issues with special characters.