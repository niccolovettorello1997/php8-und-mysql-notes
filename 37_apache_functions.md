# Chapter 37 – Apache Functions

## Sections
1. Preparations  
2. Information about Apache  
3. Reading HTTP Headers  
4. Information about URIs  
5. Connecting Other Server-Side Technologies  
6. Terminating an Apache Process  

---

## Summary
PHP provides **Apache-specific functions** that can be used when running under the Apache web server. These functions are mostly used for interacting with Apache internals, headers, and request handling. They are not portable (i.e., will not work under Nginx, IIS, or CLI), so usage should be carefully considered.

---

## Key Concepts

### 1. Preparations
- These functions are only available when PHP is **running as an Apache module**.  
- Verify the SAPI (Server API) with:
  ```php
  echo php_sapi_name(); // e.g. "apache2handler"
  ```

* Many of these functions are **deprecated or discouraged** in modern environments.

---

### 2. Information about Apache

* `apache_get_version()` → Returns the Apache version string.
* `apache_get_modules()` → Lists all currently loaded Apache modules.
* `apache_note()` → Gets or sets values in Apache request notes (can be shared across modules).

**Example**:

```php
if (function_exists('apache_get_version')) {
    echo "Apache version: " . apache_get_version();
}
```

---

### 3. Reading HTTP Headers

* `getallheaders()` → Returns an array of all HTTP request headers.
* Useful for authentication tokens, API keys, or custom headers.

**Example**:

```php
$headers = getallheaders();
echo "User-Agent: " . $headers['User-Agent'];
```

---

### 4. Information about URIs

* `apache_lookup_uri($filename)` → Performs a partial request for a URI and returns info.

  * Includes status, content type, handler, etc.
* Useful for internal checks or routing logic.

---

### 5. Connecting Other Server-Side Technologies

* Apache can be configured to **work with multiple backends** (PHP, Python, Perl, etc.).
* `apache_setenv()` allows setting environment variables visible to other modules.

**Example**:

```php
apache_setenv("APP_MODE", "development");
```

---

### 6. Terminating an Apache Process

* `apache_child_terminate()` → Ends the current Apache process after the request.
* Historically used to prevent memory leaks with long-lived Apache processes.
* Rarely needed today with PHP-FPM or modern setups.

---

## Common Pitfalls

* These functions are **not portable**; avoid them if you want cross-server compatibility.
* May require specific **Apache configurations** (e.g., mod\_php).
* Many hosting environments no longer run PHP as an Apache module.

---

## Notes & Best Practices

* Prefer **server-agnostic solutions** when possible (e.g., `$_SERVER` variables instead of Apache functions).
* Use Apache functions only when you know the environment will always be Apache.
* For modern projects, it’s often better to rely on **frameworks or reverse proxies** rather than Apache-specific logic.

---

## References / Further Reading

* [PHP Manual: Apache Functions](https://www.php.net/manual/en/ref.apache.php)
* [getallheaders() Documentation](https://www.php.net/manual/en/function.getallheaders.php)
* [Apache HTTP Server Project](https://httpd.apache.org/)