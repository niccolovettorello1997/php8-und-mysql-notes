# Chapter 7 – Strings

## Sections
1. Concatenation  
2. Splitting and Appending  
3. Lowercase and Uppercase Characters  
4. Trimming Strings  
5. Search and Replace  
6. Special Characters, HTML, etc.  
7. Comparison  
8. Utilities  

---

## Summary
This chapter covers string manipulation in PHP. Strings are sequences of characters and are fundamental for almost every PHP application, from user input to generating dynamic content.

---

## Key Concepts

### Concatenation
- Use the `.` operator to join strings.
- `.= ` operator appends to an existing string.

Example:
```php
$first = "Hello";
$second = "World";
echo $first . " " . $second; // Hello World

$first .= " Everyone";
echo $first; // Hello Everyone
```

### Splitting and Appending

* `explode()` splits a string into an array based on a delimiter.
* `implode()` joins array elements into a string.
* `substr()` can extract portions of strings.

Example:

```php
$str = "one,two,three";
$arr = explode(",", $str); // ['one', 'two', 'three']
$newStr = implode("-", $arr); // "one-two-three"
```

### Lowercase and Uppercase Characters

* `strtolower()` → convert to lowercase.
* `strtoupper()` → convert to uppercase.
* `ucfirst()` → capitalize first character.
* `ucwords()` → capitalize first letter of each word.

### Trimming Strings

* `trim()` → removes whitespace from both ends.
* `ltrim()` / `rtrim()` → left/right only.

### Search and Replace

* `strpos()` → find the position of a substring.
* `str_replace()` → replace occurrences in a string.
* `str_ireplace()` → case-insensitive replacement.

### Special Characters, HTML, etc.

* Escape characters with `\` (newline `\n`, tab `\t`).
* `htmlspecialchars()` → convert special HTML characters to entities.
* `htmlentities()` → convert all applicable characters to HTML entities.

### Comparison

* `strcmp()` / `strcasecmp()` → compare strings.
* `===` → strict comparison including type.

### Utilities

* `strlen()` → length of string.
* `str_repeat()` → repeat string.
* `str_pad()` → pad string to a certain length.

---

## Notes & Reflections

* Strings are immutable in PHP; operations create new strings.
* Always use proper escaping when handling HTML output to prevent XSS.
* Efficient string handling is crucial for performance in text-heavy applications.