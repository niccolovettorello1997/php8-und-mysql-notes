# Chapter 34 – Configuration Options in `php.ini`

## Sections
1. Where to configure?  
2. What to configure?  

---

## Summary
`php.ini` is the central configuration file for PHP. It defines global behavior of the PHP runtime, such as error handling, memory usage, and extension management. Understanding its role is crucial for development, deployment, and debugging.

---

## Key Concepts

### 1. Where to configure?
- **`php.ini` locations**:
  - Default installation provides one or more `php.ini` templates (`php.ini-development`, `php.ini-production`).
  - The active file is usually located in:
    - Linux: `/etc/php/{version}/cli/php.ini` or `/etc/php/{version}/apache2/php.ini`.
    - Windows: inside the PHP installation directory.
- **Runtime check**:  
  - Run `php --ini` (CLI) or use `phpinfo()` (web) to find the loaded configuration file.
- **Override options**:
  - `php.ini` → global default.  
  - `.htaccess` (Apache with `mod_php`) → per-directory overrides.  
  - `ini_set()` in PHP → per-script override (limited to modifiable directives).

### 2. What to configure?
Key categories of settings in `php.ini`:

#### General Settings
- `display_errors`, `log_errors` – control error output and logging.
- `error_reporting` – defines which errors are reported.
- `timezone` (`date.timezone`) – ensures consistent date/time handling.

#### Resource Limits
- `memory_limit` – maximum memory per script.
- `max_execution_time` – time limit for script execution.
- `max_input_time` – limit for parsing input (POST, GET).

#### File Uploads
- `file_uploads` (On/Off).
- `upload_max_filesize` – maximum single file size.
- `post_max_size` – maximum total POST request size.

#### Sessions
- `session.save_path` – where session files are stored.
- `session.gc_maxlifetime` – session lifetime.
- `session.cookie_secure`, `session.cookie_httponly` – security flags.

#### Extensions
- `extension=...` – enable PHP extensions (e.g., `pdo_mysql`, `gd`, `mbstring`).

#### Security
- `disable_functions` – disable risky functions (`exec`, `shell_exec`, etc.).
- `allow_url_fopen` – control remote file access.
- `expose_php` – prevent PHP version exposure.

---

## Common Pitfalls
- Misaligned limits: `upload_max_filesize` < `post_max_size` → uploads fail silently.  
- Using development settings (`display_errors = On`) in production.  
- Not setting `date.timezone`, leading to warnings and inconsistent behavior.  
- Forgetting to restart web server/PHP-FPM after changing `php.ini`.

---

## Notes & Best Practices
- Keep separate configurations for **development** and **production**.  
- Log errors instead of displaying them to users.  
- Regularly audit enabled extensions (minimize attack surface).  
- Store customized `php.ini` under version control when using Docker or deployment pipelines.  
- Use `ini_get()` to check current settings inside PHP.

---

## References / Further Reading
- [PHP Manual: Runtime Configuration](https://www.php.net/manual/en/ini.php)  
- [PHP Configuration Directives List](https://www.php.net/manual/en/ini.list.php)  
- [Error Handling in PHP](https://www.php.net/manual/en/errorfunc.configuration.php)