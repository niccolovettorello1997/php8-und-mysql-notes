# Chapter 8 – Arrays

## Sections
1. Array Basics  
2. Arrays and Loops  
3. Array Analysis  
4. Transformation  
5. Search and Sorting  
6. Superglobal Arrays  

---

## Summary
This chapter covers arrays in PHP. Arrays are ordered maps that can store multiple values in a single variable, indexed numerically or associatively. They are essential for organizing and manipulating collections of data.

---

## Key Concepts

### Array Basics
- Indexed arrays: numeric keys starting from 0.
- Associative arrays: custom keys (strings or integers).
- Multidimensional arrays: arrays containing arrays.

Example:
```php
$indexed = ["apple", "banana", "cherry"];
$associative = ["name" => "John", "age" => 30];
$multi = [
    "fruits" => ["apple", "banana"],
    "vegetables" => ["carrot", "lettuce"]
];
```

### Arrays and Loops

* Use `foreach` to iterate over arrays.
* `for` can iterate numeric arrays using indices.

Example:

```php
foreach ($associative as $key => $value) {
    echo "$key: $value\n";
}
```

### Array Analysis

* `count()` → number of elements.
* `in_array()` → check if a value exists.
* `array_key_exists()` → check if a key exists.

### Transformation

* `array_merge()` → merge arrays.
* `array_slice()` → extract part of an array.
* `array_map()` → apply function to each element.
* `array_filter()` → filter elements based on a callback.

### Search and Sorting

* `array_search()` → return key of a value.
* Sorting functions:

  * `sort()` / `rsort()` → numeric array ascending/descending.
  * `asort()` / `arsort()` → associative array by values.
  * `ksort()` / `krsort()` → associative array by keys.

### Superglobal Arrays

* `$_GET`, `$_POST`, `$_REQUEST` → HTTP input.
* `$_SESSION`, `$_COOKIE` → session and cookie data.
* `$_SERVER`, `$_ENV` → server and environment info.

---

## Notes & Reflections

* Arrays are flexible but can become complex if nested deeply.
* Using built-in array functions is often more efficient than manual loops.
* Understanding superglobals is crucial for web applications handling user input.