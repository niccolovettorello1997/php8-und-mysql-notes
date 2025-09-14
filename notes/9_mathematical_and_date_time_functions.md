# Chapter 9 – Mathematical and Date/Time Functions

## Sections
1. Mathematical Functions  
2. Date and Time Functions  

---

## Summary
This chapter introduces built-in PHP functions for performing mathematical calculations and handling dates and times. These functions are useful for numeric operations, statistical calculations, and managing temporal data.

---

## Key Concepts

### Mathematical Functions
- Basic arithmetic functions: `abs()`, `round()`, `ceil()`, `floor()`.
- Power and roots: `pow()`, `sqrt()`.
- Trigonometry: `sin()`, `cos()`, `tan()`.
- Random numbers: `rand()`, `mt_rand()`.
- Minimum and maximum: `min()`, `max()`.

Example:
```php
echo abs(-5);      // 5
echo sqrt(16);     // 4
echo round(3.7);   // 4
echo rand(1, 10);  // random number between 1 and 10
```

### Date and Time Functions

* Current date/time: `date()`, `time()`.
* Timestamps: `strtotime()`, `mktime()`.
* Formatting dates: `date("Y-m-d H:i:s")`.
* Differences between dates: subtract timestamps.
* Time zones: `date_default_timezone_set()`.

Example:

```php
echo date("Y-m-d H:i:s");           // current date and time
$timestamp = strtotime("2025-09-12");
echo date("l, d F Y", $timestamp);  // formatted date
```

---

## Notes & Reflections

* Mathematical functions are foundational for numeric and statistical operations.
* Date/time functions are crucial for web applications dealing with scheduling, logging, or any time-sensitive logic.
* Always handle time zones carefully to avoid errors in global applications.