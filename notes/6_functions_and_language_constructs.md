# Chapter 6 – Functions and Language Constructs

## Sections
1. Functions  
2. Language Constructs  

---

## Summary
This chapter covers PHP functions and language constructs, which are essential for organizing code, reusing logic, and leveraging built-in capabilities. Functions allow encapsulation of behavior, while language constructs are special syntactic elements with specific purposes.  

---

## Key Concepts

### Functions
- **Definition:** Functions are blocks of reusable code defined with `function`.  
- **Parameters & Arguments:** Functions can accept arguments; they can have default values.  
- **Return Values:** Functions may return a value using `return`.  
- **Variable Scope:** Local vs. global variables; `global` keyword for accessing globals.  
- **Anonymous Functions / Closures:** Functions without a name, assignable to variables.  

Example:

```php
function greet($name = "Guest") {
    return "Hello, $name!";
}

echo greet("Alice"); // Hello, Alice!
echo greet();        // Hello, Guest!

$adder = function($a, $b) {
    return $a + $b;
};
echo $adder(2, 3);   // 5
```

### Language Constructs

- **`echo` / `print`** → output strings.
- **`include` / `require`** → include external PHP files.
- **`isset` / `empty` / `unset`** → variable existence and cleanup.
- **`die` / `exit`** → terminate script execution.
- **`global` / `static` / `const`** → variable scope and constants.

Example:

```php
if (isset($variable)) {
    echo "Variable exists";
}

include 'header.php';

const MAX_USERS = 100;
```

---

## Notes & Reflections

- Use functions to keep code modular and readable.
- Built-in language constructs are faster than equivalent functions, e.g., `isset()` vs. checking with a function.
- Proper handling of scope and constants prevents bugs and improves maintainability.