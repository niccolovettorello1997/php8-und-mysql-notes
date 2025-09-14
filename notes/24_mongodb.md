# Chapter 24 – MongoDB

## Sections
1. Preparation  
2. Accessing the Database with MongoDB  
3. Settings  

---

## Summary
This chapter describes how to use **MongoDB** with PHP.  
MongoDB is a **NoSQL document database** that stores data in flexible **BSON/JSON-like documents**, ideal for unstructured or semi-structured data.  
PHP integrates MongoDB via the **MongoDB PHP driver** and the **MongoDB PHP Library**.

---

## Key Concepts

### 1. Preparation
- Install MongoDB server (from [mongodb.com](https://www.mongodb.com) or package manager).  
- Default port: **27017**.  
- Enable and install the PHP extension:
  ```bash
  pecl install mongodb
  ```

and add in `php.ini`:

```ini
extension=mongodb.so
```

* Composer package for higher-level API:

  ```bash
  composer require mongodb/mongodb
  ```

### 2. Accessing the Database with MongoDB

#### Using the native MongoDB driver

```php
require 'vendor/autoload.php';

$client = new MongoDB\Client("mongodb://localhost:27017");

// Select database and collection
$collection = $client->test->users;

// Insert document
$result = $collection->insertOne([
    'name' => 'Alice',
    'age' => 30,
    'email' => 'alice@example.com'
]);
echo "Inserted with ID: " . $result->getInsertedId() . PHP_EOL;

// Find documents
$cursor = $collection->find(['age' => ['$gt' => 20]]);
foreach ($cursor as $doc) {
    echo $doc['name'] . " - " . $doc['age'] . PHP_EOL;
}
```

#### CRUD Operations

* Insert: `insertOne()`, `insertMany()`
* Read: `findOne()`, `find()`
* Update: `updateOne()`, `updateMany()`
* Delete: `deleteOne()`, `deleteMany()`

Example update:

```php
$collection->updateOne(
    ['name' => 'Alice'],
    ['$set' => ['age' => 31]]
);
```

### 3. Settings

* **Authentication**: configure in `mongod.conf` or with `--auth`.
* **Replica sets**: recommended for high availability.
* **Indexing**: create indexes to improve query performance:

  ```php
  $collection->createIndex(['email' => 1], ['unique' => true]);
  ```
* **BSON vs JSON**: data is stored internally as BSON (Binary JSON), allowing for extra data types like dates and binary data.

---

## Notes

* MongoDB is popular for **scalable web apps, analytics, IoT, and microservices**.
* Good complement to relational databases in **polyglot persistence architectures**.
* PHP developers usually use MongoDB via the **MongoDB PHP Library + Composer** for clean code.