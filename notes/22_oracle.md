# Chapter 22 – Oracle

## Sections
1. Preparation  
2. Accessing the Database with Oracle  

---

## Summary
This chapter covers how to connect PHP with **Oracle Database** using the **OCI8 extension** or **PDO_OCI**.  
Oracle is a robust and widely used RDBMS, especially in large enterprises. Integrating PHP with Oracle requires additional client libraries and configuration.

---

## Key Concepts

### 1. Preparation
- Install **Oracle Database** locally or access a remote instance.  
- Install the **Oracle Instant Client** for your operating system.  
- Enable the **OCI8 extension** in PHP (`php_oci8.dll` on Windows or `oci8.so` on Linux).  
- Alternatively, enable **PDO_OCI** for a PDO-compatible interface.  
- Confirm installation with `phpinfo()` → look for `OCI8 Support`.  

### 2. Accessing the Database with Oracle

#### Using OCI8
```php
// Connection
$conn = oci_connect("username", "password", "localhost/XE");
if (!$conn) {
    $e = oci_error();
    die("Connection failed: " . $e['message']);
}

// Query
$sql = "SELECT employee_id, first_name, last_name FROM employees";
$stid = oci_parse($conn, $sql);
oci_execute($stid);

while ($row = oci_fetch_assoc($stid)) {
    echo $row['EMPLOYEE_ID'] . ": " . $row['FIRST_NAME'] . " " . $row['LAST_NAME'] . PHP_EOL;
}

// Free resources and close connection
oci_free_statement($stid);
oci_close($conn);
```

#### Using PDO\_OCI

```php
try {
    $pdo = new PDO("oci:dbname=//localhost:1521/XE", "username", "password");
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

    // Insert example
    $stmt = $pdo->prepare("INSERT INTO employees (employee_id, first_name, last_name) VALUES (:id, :first, :last)");
    $stmt->execute([
        ':id' => 101,
        ':first' => 'Alice',
        ':last' => 'Smith'
    ]);

    // Select example
    foreach ($pdo->query("SELECT * FROM employees") as $row) {
        echo $row['FIRST_NAME'] . " " . $row['LAST_NAME'] . PHP_EOL;
    }
} catch (PDOException $e) {
    echo "Connection failed: " . $e->getMessage();
}
```

---

## Notes

* Oracle integration is common in **finance, telco, and enterprise environments**.
* **OCI8** provides the most features (advanced Oracle-specific functionality).
* **PDO\_OCI** is simpler but less feature-rich.
* Always configure proper **character sets** (e.g., UTF-8) to avoid encoding problems.
* Requires more setup than MySQL or PostgreSQL, so often seen only where Oracle is already in use.