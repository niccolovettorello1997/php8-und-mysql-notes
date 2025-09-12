# Chapter 4 – PHP Basics

## Sections
1. PHP in HTML  
2. Output with PHP  
3. Variables  
4. Constants  

---

## Summary
This chapter covers the fundamental concepts of PHP programming: embedding PHP within HTML, displaying output, using variables to store data, and defining constants. These basics form the foundation for all PHP development.  

---

## Key Concepts

### PHP in HTML
- PHP code can be embedded directly into HTML files.  
- Standard PHP tags:
```php
<?php
// PHP code here
?>
```

* Short tags `<?` and `<?=` exist but may be disabled on some servers.

Example:

```php
<!DOCTYPE html>
<html>
  <body>
    <h1><?php echo "Hello, world!"; ?></h1>
  </body>
</html>
```

### Output with PHP

- `echo` → outputs one or more strings.
- `print` → outputs a string, returns 1 (can be used in expressions).
- `printf` / `sprintf` → formatted output.

Example:

```php
echo "Hello", " ", "World!";
print "Hello World!";
printf("Number: %d", 42);
```

### Variables

- Start with `$`, followed by a name (letters, numbers, underscores).
- Case-sensitive.
- Dynamic typing: PHP determines type automatically (string, int, float, boolean, array, object, null).

Example:

```php
$age = 30;
$name = "Alice";
$isActive = true;
```

- Variable scope: local, global, static.

### Constants

- Defined using `define()` or `const`.
- Cannot be changed after declaration.

Example:

```php
define("SITE_NAME", "My Website");
const VERSION = "1.0";
```

---

## Code / Command Examples

```php
// Embedding PHP in HTML
<!DOCTYPE html>
<html>
<body>
  <p><?php echo "Welcome!"; ?></p>
</body>
</html>

// Variables and constants
$counter = 10;
define("PI", 3.14159);
echo "Counter: $counter, PI: " . PI;
```

---

## Notes & Reflections

- PHP’s flexibility with types is convenient but requires careful attention to avoid unexpected behavior.
- Always use descriptive variable names and constants for readability.
- Embedding PHP in HTML is useful for templating but modern applications often use template engines for cleaner separation of logic and presentation.