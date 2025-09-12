# Chapter 5 – Programming

## Sections
1. Operators  
2. Conditional Structures  
3. Loops  
4. Jumps  

---

## Summary
This chapter introduces the core programming constructs in PHP: operators for computation, conditional statements for decision-making, loops for iteration, and jump statements for controlling the flow of execution.  

---

## Key Concepts

### Operators
- **Arithmetic:** `+`, `-`, `*`, `/`, `%`  
- **Assignment:** `=`, `+=`, `-=`, `*=`, `/=`, `%=`  
- **Comparison:** `==`, `===`, `!=`, `!==`, `<`, `>`, `<=`, `>=`  
- **Logical:** `&&`, `||`, `!`, `and`, `or`, `xor`  
- **Increment/Decrement:** `++`, `--`  

Example:

```php
$a = 5;
$b = 2;
$c = $a + $b; // 7
$d = $a === $b; // false
```

### Conditional Structures

* `if` / `else if` / `else` → standard conditional branching.
* `switch` → multi-case selection.

Example:

```php
if ($score >= 90) {
    echo "Excellent";
} elseif ($score >= 75) {
    echo "Good";
} else {
    echo "Needs Improvement";
}

switch ($day) {
    case "Mon":
        echo "Monday";
        break;
    case "Tue":
        echo "Tuesday";
        break;
    default:
        echo "Other day";
}
```

### Loops

- **`for`** → known number of iterations.
- **`while`** → condition-checked before execution.
- **`do...while`** → condition-checked after execution.
- **`foreach`** → iterate arrays or objects.

Example:

```php
for ($i = 0; $i < 5; $i++) {
    echo $i;
}

while ($counter > 0) {
    echo $counter--;
}

foreach ($array as $item) {
    echo $item;
}
```

### Jumps

- **`break`** → exit loops or switch.
- **`continue`** → skip current iteration of loop.
- **`return`** → exit function and optionally return value.
- **`goto`** → jump to a label (rarely used).

Example:

```php
for ($i = 0; $i < 10; $i++) {
    if ($i % 2 == 0) continue; // skip even numbers
    if ($i > 7) break;          // exit loop if i > 7
    echo $i;
}
```

---

## Notes & Reflections

- Proper use of operators and conditions is key to implementing correct logic.
- Avoid `goto` in most cases, structured loops and functions are safer and more readable.
- `foreach` is especially useful for working with arrays and objects in modern PHP.