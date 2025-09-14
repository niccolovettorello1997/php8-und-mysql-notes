# Chapter 14 – Cookies

## Sections
1. Preparations  
2. Basic Facts and Information  
3. Working with Cookies in PHP  
4. Cookie Test  
5. Final Considerations  

---

## Summary
This chapter explains how cookies work, how PHP can create and manage them, and what to watch out for in terms of usability and security. Cookies are small pieces of data stored on the client’s browser and are essential for session handling, user preferences, and state management across multiple requests.

---

## Key Concepts

### 1. Preparations
- Check browser configuration: cookies must be enabled for testing.  
- Ensure server and client are configured correctly (e.g. no output before `setcookie()`).  
- Understand the difference between session cookies (expire when the browser closes) and persistent cookies (have a set lifetime).  

### 2. Basic Facts and Information
- Cookies are key–value pairs stored on the client.  
- Sent via HTTP headers; must be set before output.  
- Each cookie can contain additional metadata: expiration, path, domain, secure flag, HttpOnly flag, SameSite attribute.  
- Browsers enforce size and number limits for cookies.  

### 3. Working with Cookies in PHP
- Create cookies using `setcookie(name, value, expire, path, domain, secure, httponly, options)`.  
- Read cookies with `$_COOKIE['name']`.  
- Modify cookies by sending a new cookie with the same name and different value.  
- Delete cookies by setting expiration time in the past.  
- Use options like `HttpOnly` (protects from JavaScript access), `Secure` (only send over HTTPS), and `SameSite` (limits cross-site requests).  

### 4. Cookie Test
- A simple test flow:  
  1. Set a cookie with `setcookie()`.  
  2. Reload page and check `$_COOKIE` array.  
  3. Validate that cookie persists across requests.  
- Check browser dev tools → Storage → Cookies to verify.  
- Useful for debugging authentication and user-preference functionality.  

### 5. Final Considerations
- Cookies are essential for authentication (often combined with sessions).  
- Privacy laws (e.g. GDPR) require user consent for non-essential cookies.  
- Avoid storing sensitive data directly in cookies → always use tokens or IDs, not plain passwords or personal data.  
- Keep cookie size minimal to reduce HTTP overhead.  

---

## Common Pitfalls
- Trying to set cookies after HTML output (headers already sent error).  
- Storing sensitive information (e.g. passwords, raw tokens) in cookies.  
- Forgetting to use secure flags → risk of session hijacking.  
- Not testing SameSite → may cause issues with third-party integrations.  

---

## Notes & Reflections
- Cookies are simple but central to web development, especially when combined with sessions.  
- Security practices (HttpOnly, Secure, SameSite) are non-optional in modern development.  
- Good to practice with a small demo project where cookies store theme preferences or login states.  