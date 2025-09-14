# Chapter 33 – Authentication

## Sections
1. Authentication with Apache  
2. Authentication with IIS  
3. Manual HTTP Authentication  
4. Standards-based Authentication  

---

## Summary
Authentication is the process of verifying the identity of users accessing a web application. PHP applications can rely on server-level authentication mechanisms (Apache, IIS), custom implementations of HTTP authentication, or modern standards (OAuth2, OpenID Connect, JWT). This chapter reviews each approach, its configuration, and when it may be appropriate.

---

## Key Concepts

### 1. Authentication with Apache
- Apache can provide **Basic** and **Digest** authentication directly, without custom PHP code.  
- Typically configured via `.htaccess` or server configuration:  
  - `AuthType Basic`  
  - `AuthName "Restricted Area"`  
  - `AuthUserFile /path/to/.htpasswd`  
  - `Require valid-user`  
- PHP receives authenticated user info through server variables (`$_SERVER['PHP_AUTH_USER']`).  
- Pros: simple, centralized; Cons: not flexible, poor user experience, insecure without HTTPS.

### 2. Authentication with IIS
- Internet Information Services (Windows) supports:  
  - **Windows Authentication** (Kerberos/NTLM, integrates with Active Directory).  
  - **Basic Authentication**.  
- PHP receives authentication results through `$_SERVER` variables (e.g., `LOGON_USER`).  
- Good for intranet applications tightly coupled with Windows domains.

### 3. Manual HTTP Authentication
- PHP can implement **Basic HTTP Auth** by sending/reading HTTP headers.  
- Example:
```php
if (!isset($_SERVER['PHP_AUTH_USER'])) {
    header('WWW-Authenticate: Basic realm="MyApp"');
    header('HTTP/1.0 401 Unauthorized');
    echo 'Authentication required';
    exit;
} else {
    $user = $_SERVER['PHP_AUTH_USER'];
    $pass = $_SERVER['PHP_AUTH_PW'];
    // validate against DB or other store
}
```

* Not secure unless used over HTTPS. Credentials are sent with every request.
* Usually replaced by token-based methods or form-based login.

### 4. Standards-based Authentication

* Modern applications use protocols/libraries instead of raw HTTP authentication:

  * **Form-based login** (session-based, most common in web apps).
  * **OAuth 2.0** — delegated authorization, used by APIs and third-party integrations.
  * **OpenID Connect (OIDC)** — authentication layer on top of OAuth 2.0.
  * **JWT (JSON Web Token)** — compact tokens often used for stateless APIs.
* Frameworks (Symfony, Laravel) provide robust authentication/authorization components implementing these standards.
* Advantages: security, single sign-on (SSO), scalability, easier integration with third-party services.

---

## Common Pitfalls

* Using Basic authentication over HTTP (credentials exposed).
* Storing passwords insecurely (plaintext or weak hashes).
* Rolling out custom authentication without proven standards or libraries.
* Not invalidating sessions/tokens on logout.
* Forgetting multi-factor authentication (MFA) for high-value systems.

---

## Notes & Best Practices

* Always use HTTPS when handling credentials.
* For custom login systems: use `password_hash()` and `password_verify()`.
* Adopt frameworks’ built-in authentication systems where possible.
* Use OAuth2/OIDC for modern integrations (social login, enterprise SSO).
* Keep authentication separate from authorization (identity vs. access control).
* Rotate and expire tokens or session IDs regularly.

---

## References / Further Reading

* PHP manual: [HTTP authentication with PHP](https://www.php.net/manual/en/features.http-auth.php)
* Apache HTTP authentication docs
* Microsoft IIS authentication overview
* OAuth 2.0 RFC 6749
* OpenID Connect specifications
* Symfony Security component / Laravel Authentication system