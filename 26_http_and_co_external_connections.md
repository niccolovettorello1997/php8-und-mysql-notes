# Chapter 26 – HTTP & Co.: External Connections

## Sections
1. Preparation  
2. External Connections with PHP  
3. Fibers  

---

## Summary
This chapter explains how PHP can interact with **external resources over HTTP and other protocols**.  
It covers configuration, functions and libraries for sending requests, and introduces **Fibers**, which enable cooperative multitasking in PHP.

---

## Key Concepts

### 1. Preparation
- To enable external connections, check `php.ini`:
  - `allow_url_fopen = On` → allows functions like `file_get_contents("http://...")`.  
  - `openssl` extension must be enabled for HTTPS requests.  
- Alternatives: using **cURL** (recommended for complex HTTP communication).  
- Security: be cautious when fetching remote data (avoid SSRF, validate inputs).

---

### 2. External Connections with PHP

#### Using `file_get_contents`
```php
$response = file_get_contents("https://example.com/api/data.json");
$data = json_decode($response, true);
```

#### Using `fopen` with Streams

```php
$handle = fopen("http://example.com", "r");
if ($handle) {
    while (!feof($handle)) {
        echo fgets($handle);
    }
    fclose($handle);
}
```

#### Using `cURL`

```php
$ch = curl_init("https://api.example.com");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
$response = curl_exec($ch);
curl_close($ch);

$data = json_decode($response, true);
```

* `cURL` supports:

  * GET/POST/PUT/DELETE requests
  * Custom headers
  * Authentication (Basic, Bearer tokens)
  * Timeouts and error handling

---

### 3. Fibers

* Introduced in **PHP 8.1**.
* Provide **lightweight concurrency** → allow pausing and resuming execution (similar to coroutines).
* Useful for async I/O without blocking.

#### Example: Fiber Basics

```php
$fiber = new Fiber(function(): void {
    $value = Fiber::suspend("Hello from Fiber");
    echo "Resumed with: $value\n";
});

echo $fiber->start();   // Suspends, outputs "Hello from Fiber"
$fiber->resume("Back to Fiber"); // Resumes
```

* Practical usage: often abstracted by async frameworks like **Amp** or **ReactPHP**.
* Improves scalability of PHP apps handling multiple connections (e.g., APIs, chat apps).

---

## Notes

* For simple tasks → `file_get_contents()` is enough.
* For production APIs → prefer `cURL` or libraries like **Guzzle**.
* Fibers represent a modern shift towards **asynchronous PHP**, though adoption is still limited.