# Chapter 10 – Regular Expressions

## Sections
1. Basics  
2. Regular Expression Functions  

---

## Summary
This chapter introduces regular expressions (regex) in PHP. Regular expressions are patterns used to match, search, and manipulate text. They are extremely useful for validation, parsing, and text processing.

---

## Key Concepts

### Basics
- A regular expression is a string that defines a search pattern.  
- Common elements:
  - `.` : any single character
  - `*` : zero or more repetitions
  - `+` : one or more repetitions
  - `?` : zero or one repetition
  - `[]` : character class
  - `^` : start of string
  - `$` : end of string
  - `|` : alternation (OR)
  - `()` : grouping

Example:
```php
$pattern = "/^a.*b$/";  // string starts with 'a' and ends with 'b'
```

### Regular Expression Functions

* `preg_match()` : check if pattern matches
* `preg_match_all()` : match all occurrences
* `preg_replace()` : search and replace
* `preg_split()` : split string using regex

Examples:

```php
if (preg_match("/[0-9]{3}/", "abc123")) {
    echo "Found a 3-digit number!";
}

$result = preg_replace("/foo/", "bar", "foo baz"); // "bar baz"

$parts = preg_split("/[\s,]+/", "one,two three"); // ["one","two","three"]
```

---

## Notes & Reflections

* Regex is powerful but can be complex; always test patterns carefully.
* Regular expressions are widely used for form validation, input sanitization, and text parsing.