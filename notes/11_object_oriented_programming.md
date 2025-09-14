# Chapter 11 – Object-Oriented Programming (OOP)

## Sections
1. History of Object-Oriented Programming in PHP  
2. Classes and Objects – Basic Concepts  
3. Advanced Concepts  
4. Utilities  
5. Namespaces  

---

## Summary
This chapter covers PHP’s object-oriented programming (OOP) capabilities, from the basics to advanced features. OOP allows structuring code into reusable, modular components using classes and objects.

---

## Key Concepts

### 1. History of OOP in PHP
- PHP added OOP gradually:
  - PHP 4: basic class support
  - PHP 5: full OOP features (interfaces, abstract classes, visibility)
  - PHP 7+: improvements in type hints, return types, and performance

### 2. Classes and Objects – Basic Concepts
- **Class**: blueprint for objects
- **Object**: instance of a class
- **Properties**: variables inside a class
- **Methods**: functions inside a class

Example:
```php
class User {
    public $name;
    private $email;

    public function __construct($name, $email) {
        $this->name = $name;
        $this->email = $email;
    }

    public function getEmail() {
        return $this->email;
    }
}

$user = new User("Alice", "alice@example.com");
echo $user->getEmail();
```

### 3. Advanced Concepts

* **Inheritance**: child classes inherit from parent classes
* **Interfaces**: define methods a class must implement
* **Abstract Classes**: cannot be instantiated, can contain abstract methods
* **Traits**: reusable sets of methods to include in classes
* **Visibility**: public, private, protected
* **Static properties and methods**
* **Magic methods**: `__construct()`, `__destruct()`, `__get()`, `__set()`, `__call()`, `__toString()`

Example of inheritance:

```php
class Admin extends User {
    public function isAdmin() {
        return true;
    }
}
```

### 4. Utilities

* `instanceof` keyword: check object type
* `get_class()` function: get class name
* `method_exists()` and `property_exists()` functions

### 5. Namespaces

* Used to organize code and avoid name collisions
* Declared with `namespace` keyword

Example:

```php
namespace App\Models;

class User {}
```

---

## Notes & Reflections

* OOP allows modular, maintainable, and reusable code.
* Familiarity with OOP is essential for modern PHP frameworks like Symfony and Laravel.