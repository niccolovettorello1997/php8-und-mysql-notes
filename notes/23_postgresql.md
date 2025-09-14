# Chapter 23 – PostgreSQL

## Sections
1. Preparation  
2. Accessing the Database with PostgreSQL  
3. Settings  

---

## Summary
This chapter describes how to use **PostgreSQL** with PHP.  
PostgreSQL is a powerful open-source relational database with advanced features such as transactions, window functions, and JSON support.  
PHP provides support through **pgSQL functions** and **PDO_PGSQL**.

---

## Key Concepts

### 1. Preparation
- Install PostgreSQL (e.g., via package manager or official installer).  
- Ensure `pgsql` and/or `pdo_pgsql` extensions are enabled in `php.ini`.  
- Verify with `phpinfo()` → look for **PostgreSQL support**.  
- Start the PostgreSQL server (`systemctl start postgresql` on Linux, or pgAdmin).  

### 2. Accessing the Database with PostgreSQL

#### Using pg_connect (procedural API)
```php
// Connection
$conn = pg_connect("host=localhost dbname=test user=postgres password=secret");
if (!$conn) {
    die("Connection failed");
}

// Query
$result = pg_query($conn, "SELECT id, name FROM users");
while ($row = pg_fetch_assoc($result)) {
    echo $row['id'] . " - " . $row['name'] . PHP_EOL;
}

// Close
pg_close($conn);
```

#### Using PDO\_PGSQL

```php
try {
    $pdo = new PDO("pgsql:host=localhost;port=5432;dbname=test;user=postgres;password=secret");
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

    // Insert example
    $stmt = $pdo->prepare("INSERT INTO users (id, name) VALUES (:id, :name)");
    $stmt->execute([
        ':id' => 1,
        ':name' => 'Alice'
    ]);

    // Select example
    foreach ($pdo->query("SELECT * FROM users") as $row) {
        echo $row['id'] . " - " . $row['name'] . PHP_EOL;
    }
} catch (PDOException $e) {
    echo "Connection failed: " . $e->getMessage();
}
```

### 3. Settings

* Default port: **5432**.
* Authentication via `pg_hba.conf` (choose between `md5`, `peer`, `trust`, etc.).
* Character encoding should be set to **UTF-8** for modern applications.
* Use transactions for consistency:

```php
$pdo->beginTransaction();
$pdo->exec("UPDATE accounts SET balance = balance - 100 WHERE id = 1");
$pdo->exec("UPDATE accounts SET balance = balance + 100 WHERE id = 2");
$pdo->commit();
```

---

## Notes

* PostgreSQL is widely used in **startups, SaaS platforms, and data-heavy applications**.
* Offers **better standards compliance** and advanced features compared to MySQL.
* PDO\_PGSQL is recommended for modern applications due to cleaner API and exception handling.