# Chapter 12 – Design Patterns & Co.

## Sections
1. Basics  
2. MVC (Model-View-Controller)  
3. Adapter  
4. Factory  

---

## Summary
This chapter introduces common design patterns in PHP and how they help structure applications in a clean, maintainable way. Design patterns solve recurring problems in software design by providing reusable solutions.

---

## Key Concepts

### 1. Basics
- **Design Patterns**: standardized solutions to common programming problems
- Improve code **readability**, **reusability**, and **maintenance**
- Categories:
  - **Creational**: object creation (Factory, Singleton)
  - **Structural**: class and object composition (Adapter, Decorator)
  - **Behavioral**: communication between objects (Observer, Strategy)

### 2. MVC (Model-View-Controller)
- **Model**: manages data and business logic
- **View**: presentation layer (HTML, templates)
- **Controller**: handles user input, connects Model and View

Example:
```php
class UserController {
    public function showProfile($id) {
        $user = UserModel::find($id);
        View::render('profile', ['user' => $user]);
    }
}
```

* Widely used in frameworks like Laravel and Symfony

### 3. Adapter Pattern

* Allows incompatible interfaces to work together
* Acts as a **translator** between classes

Example:

```php
interface PaymentGateway {
    public function pay($amount);
}

class StripeAdapter implements PaymentGateway {
    private $stripe;

    public function __construct($stripe) {
        $this->stripe = $stripe;
    }

    public function pay($amount) {
        $this->stripe->charge($amount);
    }
}
```

### 4. Factory Pattern

* Provides a **method to create objects** without exposing instantiation logic
* Useful when object creation is complex

Example:

```php
class LoggerFactory {
    public static function create($type) {
        if ($type === 'file') {
            return new FileLogger();
        } elseif ($type === 'db') {
            return new DatabaseLogger();
        }
    }
}

$logger = LoggerFactory::create('file');
```

---

## Notes & Reflections

* Understanding design patterns is crucial for writing **scalable and maintainable code**
* Frameworks like Symfony and Laravel heavily rely on these patterns