# Chapter 39 – Extensions for PHP

## Sections
1. Programming  
2. Compiling  
3. Testing  

---

## Summary
PHP can be extended with **native extensions** written in C (or C++).  
Extensions allow developers to add low-level functionality or improve performance by bypassing pure PHP code.  
Although not a daily task for most PHP developers, understanding how extensions work is valuable for performance-critical systems or integrating PHP with external libraries.

---

## Key Concepts

### 1. Programming
- PHP extensions are typically written in **C** and interact with PHP’s Zend Engine.  
- A new extension defines functions, classes, or resources that become available to PHP scripts.  
- The entry point is usually `PHP_FUNCTION()` macros and `zend_module_entry`.  

**Example (simplified)**:
```c
#include "php.h"

PHP_FUNCTION(hello_world) {
    php_printf("Hello from C extension!\n");
}

static zend_function_entry myext_functions[] = {
    PHP_FE(hello_world, NULL)
    PHP_FE_END
};

zend_module_entry myext_module_entry = {
    STANDARD_MODULE_HEADER,
    "myext",
    myext_functions,
    NULL, NULL, NULL, NULL, NULL,
    "0.1",
    STANDARD_MODULE_PROPERTIES
};

ZEND_GET_MODULE(myext)
```

---

### 2. Compiling

* Extensions are compiled against the installed PHP source.

* Steps:

  1. Install PHP source code (matching your PHP version).
  2. Use `phpize` to prepare the build environment:

     ```bash
     phpize
     ./configure
     make
     sudo make install
     ```
  3. Add the extension to `php.ini`:

     ```ini
     extension=myext.so
     ```

* Tools:

  * `phpize` → prepares build system.
  * `./configure` → configures for your system.
  * `make` → compiles.

---

### 3. Testing

* Once compiled and enabled, the extension can be tested with PHP scripts.
* Use `php -m` to verify that the extension is loaded.
* PHPUnit or **phpt tests** can be used for automated testing.

**Example**:

```php
<?php
hello_world(); // Output: Hello from C extension!
```

* PHPT files are the standard way to test extensions. They include:

  * `--TEST--` (description)
  * `--FILE--` (PHP code to run)
  * `--EXPECT--` (expected output)

**Example test file** (`hello_world.phpt`):

```
--TEST--
Test hello_world function
--FILE--
<?php
hello_world();
?>
--EXPECT--
Hello from C extension!
```

---

## Common Pitfalls

* Extensions must be recompiled for each PHP version → maintenance burden.
* Incorrect memory management in C can lead to crashes.
* Poorly written extensions can reduce stability and security.

---

## Notes & Best Practices

* Prefer **pure PHP or existing libraries** unless absolutely necessary.
* Write extensions only for performance-critical features or when binding to a C library.
* Always include automated **PHPT tests** for reliability.
* Document extension usage for developers who will use it.

---

## References / Further Reading

* [PHP Internals Book](http://www.phpinternalsbook.com/)
* [PHP: Writing PHP Extensions](https://www.php.net/internals2.ze1.zendapi)
* [PHPT Tests Documentation](https://qa.php.net/write-test.php)