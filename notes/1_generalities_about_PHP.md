# Chapter 1 – Generalities about PHP

## Sections
1. History of PHP  
2. Consequences and usage  
3. The concept of PHP  
4. The most important new features from PHP 8 up to PHP 8.3  
5. The most important new features in PHP 7.3  
6. The most important new features in PHP 7  
7. The most important new features in PHP 5.4, 5.5 and 5.6  
8. Versions and official site  

---

## Summary
This chapter introduces the PHP language, starting from its history, its main concepts, and its typical use cases. It also presents the major innovations from the recent versions (PHP 5.4 → PHP 8.3), highlighting how PHP has evolved into a mature and powerful language for web development.

---

## Key Concepts
- **Origins of PHP** → Created in 1994 by Rasmus Lerdorf as a set of CGI scripts to make web pages dynamic.  
- **Usage** → One of the most widely used server-side languages for web applications, with large frameworks such as Laravel and Symfony.  
- **Core idea** → Interpreted language, runs on the server, embedded in HTML.  
- **PHP 8–8.3 highlights** → JIT compiler, union types, attributes, match expressions, improved typing and performance.  
- **PHP 7.3 highlights** → Functions `array_key_first`, `array_key_last`, trailing commas in function calls.  
- **PHP 7 highlights** → Scalar type hints, return type declarations, huge performance boost, null coalescing operator `??`.  
- **PHP 5.4–5.6 highlights** → Traits, short array syntax `[]`, variadic functions, generators, `finally` keyword.  
- **Versions and site** → Official website [https://www.php.net](https://www.php.net) contains documentation and changelog.  

---

## Code Examples
```php
// Example: typing introduced in PHP 7+
function sum(int $a, int $b): int {
    return $a + $b;
}
echo sum(2, 3); // 5

// Match expression (PHP 8)
$value = 2;
$result = match($value) {
    1 => "one",
    2 => "two",
    default => "other",
};
echo $result; // "two"
```

---

## Common Pitfalls
- Using old PHP versions (5.x) → no longer supported, insecure, much slower.
- Ignoring modern features → typing, attributes, match expressions are now best practices.
- Thinking of PHP as “just a simple scripting language” → modern PHP is feature-rich and enterprise-ready.

---

## Notes & Reflections
- Interesting to see how PHP moved from a “quick hack” language to an enterprise-grade solution.
- PHP 7 was the real revolution in terms of performance and stability.
- PHP 8+ added strong typing and features that align it more with modern, strongly typed languages.