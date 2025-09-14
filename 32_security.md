# Chapter 32 – Security

## Sections
1. User input  
2. XSS (Cross-Site Scripting)  
3. SQL Injection  
4. Hidden input fields — risks and usage  
5. Input filtering  
6. CSRF (Cross-Site Request Forgery)  
7. Screen scraping and CAPTCHAs  
8. Password hashing / encryption  

---

## Summary
This chapter gathers practical security best practices for typical PHP web applications. It focuses on handling user input safely, preventing common web attacks (XSS, SQL injection, CSRF), managing hidden form fields correctly, applying input filtering, defending against automated bots (CAPTCHAs), and securely storing passwords. The goal is to provide concise, actionable measures that reduce the most frequent vulnerabilities in PHP projects.

---

## Key Concepts

### 1. User input
- Treat **all** external input as untrusted (HTTP params, cookies, headers, files, third-party APIs).  
- Apply a **validation → canonicalization → sanitization** workflow:
  1. **Validate** that the input matches expected shape/type (regex, types, ranges).  
  2. **Canonicalize** to a standard representation if needed.  
  3. **Sanitize/escape** only at the point of use (output encoding for HTML, parameterization for DB queries, escaping for shell/OS, etc.).  
- Principle of **least privilege**: accept only what you need.

### 2. XSS (Cross-Site Scripting)
- XSS happens when attacker-supplied data is rendered into pages without proper encoding.  
- Main defenses:
  - **Output encoding**: use `htmlspecialchars($str, ENT_QUOTES | ENT_SUBSTITUTE, 'UTF-8')` for HTML contexts.  
  - Context-specific encoding for attributes, URLs, JS, CSS (use libraries or template engines that provide proper escaping).  
  - Use Content Security Policy (CSP) headers to mitigate impact.  
- Never rely on input sanitization alone to prevent XSS — escape on output.

Example:
```php
// Safe output in HTML
echo htmlspecialchars($userInput, ENT_QUOTES | ENT_SUBSTITUTE, 'UTF-8');
```

### 3. SQL Injection

* SQL injection arises when untrusted input is concatenated into SQL statements.
* Defence: **parameterized queries / prepared statements** (PDO or mysqli). Never interpolate values directly.

PDO example:

```php
$stmt = $pdo->prepare("SELECT * FROM users WHERE email = :email");
$stmt->execute([':email' => $email]);
$user = $stmt->fetch(PDO::FETCH_ASSOC);
```

### 4. Hidden input fields — risks and usage

* Hidden fields (`<input type="hidden">`) are **client-controlled** and can be manipulated.
* Do not store trust decisions or sensitive data in hidden fields (IDs can be OK if re-validated server-side).
* Always re-check and authorize any value coming from the client (including hidden fields) before using it for critical operations.

### 5. Input filtering

* Use PHP `filter_var()` and filter extension to validate common types (email, URL, int), but prefer strict validation/whitelisting for business data.
* Example:

```php
$email = filter_var($_POST['email'] ?? '', FILTER_VALIDATE_EMAIL);
$age = filter_var($_POST['age'] ?? '', FILTER_VALIDATE_INT, [
    'options' => ['min_range' => 0, 'max_range' => 120]
]);
```

* For complex input, use custom validators and/or validation libraries (Respect/Validation, Symfony Validator).

### 6. CSRF (Cross-Site Request Forgery)

* CSRF attacks make authenticated users unknowingly submit requests.
* Defenses:

  * Use **per-session or per-form CSRF tokens** inserted into forms and verified server-side.
  * Use `SameSite` cookie attribute to mitigate (Strict/Lax).
  * Require non-idempotent actions (POST/PUT/DELETE) and verify origin header if appropriate.
* Example pattern (simplified):

```php
// Generate token and store in session
if (empty($_SESSION['csrf'])) $_SESSION['csrf'] = bin2hex(random_bytes(32));
$token = $_SESSION['csrf'];

// On form
<input type="hidden" name="csrf" value="<?= htmlspecialchars($token) ?>">

// On submit
if (!hash_equals($_SESSION['csrf'] ?? '', $_POST['csrf'] ?? '')) {
    throw new Exception('Invalid CSRF token');
}
```

### 7. Screen scraping and CAPTCHAs

* Automated bots can abuse forms (spam, account creation). Options:

  * Use CAPTCHAs (reCAPTCHA, hCaptcha) — place on high-risk endpoints.
  * Use behavioral or invisible CAPTCHA techniques, rate limiting, IP reputation checks, and honeypot hidden fields.
  * Validate server-side usage patterns and throttle suspicious activity (rate limiting, login throttling).

### 8. Password hashing / encryption

* **Do NOT** store passwords in plaintext or with unsalted fast hashes (MD5, SHA1).
* Use PHP builtin `password_hash()` / `password_verify()` (bcrypt/argon2) to store passwords safely.

```php
// Hash on registration
$hash = password_hash($password, PASSWORD_DEFAULT);

// Verify on login
if (password_verify($passwordInput, $hash)) { /* ok */ }
```

* Consider `password_needs_rehash()` to migrate parameters (cost) over time.
* Distinguish between **hashing** (passwords) and **encryption** (symmetric/asymmetric for data you must decrypt). Use libs like libsodium or OpenSSL for encryption and manage keys securely (never commit keys).

---

## Code Examples

### Safe output for HTML

```php
// Always escape dynamic content before printing in HTML
function h($s) {
    return htmlspecialchars($s, ENT_QUOTES | ENT_SUBSTITUTE, 'UTF-8');
}
echo '<p>' . h($username) . '</p>';
```

### Prepared statements with PDO (prevents SQL injection)

```php
$stmt = $pdo->prepare('INSERT INTO comments (user_id, text) VALUES (:uid, :text)');
$stmt->execute([':uid' => $userId, ':text' => $commentText]);
```

### CSRF token example (see section 6 above)

### Password hashing (see section 8 above)

---

## Common Pitfalls

* Relying only on client-side validation (JS) — can be bypassed easily.
* Escaping input once and reusing it everywhere — use **contextual escaping** (HTML, JavaScript, URL, CSS) at point of output.
* Using `addslashes()` or naive escaping for SQL — use prepared statements instead.
* Storing sensitive data in cookies without HttpOnly/Secure flags.
* Reusing the same CSRF token for very long periods; rotate/expire tokens where appropriate.
* Rolling your own cryptography instead of using vetted libraries (avoid homemade algorithms).

---

## Notes & Best Practices

* Follow the **principle of least privilege** for DB users, file permissions, and service accounts.
* Keep dependencies updated; monitor for CVEs.
* Use HTTPS everywhere and set HSTS.
* Harden cookie settings: `Secure`, `HttpOnly`, `SameSite`.
* Use security headers: `Content-Security-Policy`, `X-Content-Type-Options: nosniff`, `X-Frame-Options: DENY` (or frame-ancestors CSP), `Referrer-Policy`.
* Add logging and monitoring to detect suspicious activity.
* Use automated security tools where possible (static analyzers, dependency scanners, dynamic scanners).
* Read OWASP Top Ten for a good, up-to-date checklist of common web vulnerabilities.

---

## References / Further Reading

* OWASP Top Ten (in particular: Injection, XSS, CSRF)
* PHP manual pages for `htmlspecialchars()`, `password_hash()`, `filter_var()`, `session_*`
* libsodium / Sodium extension for modern crypto in PHP
* PHP security best practices and framework security docs (Symfony Security, Laravel Auth)