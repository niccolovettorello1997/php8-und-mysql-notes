# Chapter 15 – Sessions

## Sections
1. Preparations  
2. Basic Facts, Concepts, and Configuration  
3. Working with Sessions in PHP  
4. Protected Area  
5. Sessions in Databases  
6. Security Considerations  

---

## Summary
Sessions allow PHP to maintain state across multiple HTTP requests by storing data on the server side and linking it to a client via a session ID (usually stored in a cookie). This chapter covers configuration, usage, database-backed sessions, and best practices for secure session handling.

---

## Key Concepts

### 1. Preparations
- Ensure session support is enabled in `php.ini`.  
- Default settings typically store session data in temporary files.  
- Check that cookies are enabled in the browser, as PHP commonly uses cookies to store session IDs.  

### 2. Basic Facts, Concepts, and Configuration
- Sessions overcome HTTP’s stateless nature by persisting user-specific data.  
- A unique session ID identifies each session (stored in cookie or URL parameter).  
- Configurable in `php.ini` (e.g., `session.save_path`, `session.gc_maxlifetime`, `session.cookie_secure`).  
- By default, session data is stored on the server (filesystem or custom handler).  

### 3. Working with Sessions in PHP
- Start a session with `session_start()`.  
- Store data in `$_SESSION` superglobal.  

Example:
```php
  session_start();
  $_SESSION['username'] = 'Alice';
  echo $_SESSION['username'];
```

* Destroy session with `session_unset()` and `session_destroy()`.
* Regenerate session ID with `session_regenerate_id(true)` for better security.

### 4. Protected Area

* Common use case: restrict access to logged-in users.
* Example flow:

  1. User logs in successfully.
  2. Store user ID or role in `$_SESSION`.
  3. Protect sensitive pages by checking session variables.
* Helps implement authentication and authorization in PHP applications.

### 5. Sessions in Databases

* Instead of storing sessions in files, use a DB backend (e.g., MySQL, PostgreSQL).
* Benefits:

  * Centralized session management (useful in load-balanced environments).
  * Easier to persist and query session data.
* Implement with `session_set_save_handler()` to define custom storage logic.

### 6. Security Considerations

* Use `session.cookie_secure = On` → transmit cookies only via HTTPS.
* Use `session.cookie_httponly = On` → prevent JavaScript from accessing session cookies.
* Prefer `session.use_strict_mode = On` → disallows uninitialized session IDs.
* Regenerate session IDs after login to prevent fixation attacks.
* Always validate user input and sanitize stored session data.
* Store minimal sensitive data; never raw passwords.

---

## Common Pitfalls

* Forgetting to call `session_start()` before using `$_SESSION`.
* Exposing session IDs in URLs → risk of session hijacking.
* Not regenerating session IDs after privilege escalation (login).
* Misconfigured garbage collection (`session.gc_probability` / `session.gc_divisor`) leading to old session persistence.

---

## Notes & Reflections

* Sessions are the backbone of PHP authentication and personalization.
* Understanding how to secure them is crucial for modern web applications.
* Good practice: implement a demo login system with session-based access control.