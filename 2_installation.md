# Chapter 2 – Installation

## Sections
1. Installing PHP  
2. PEAR (PHP Extension and Application Repository)  

---

## Summary
This chapter covers the installation of PHP on different systems and introduces PEAR, the traditional package manager for PHP. While modern PHP development often relies on **Composer**, PEAR is still relevant for understanding the historical context and certain legacy environments.  

---

## Key Concepts

### Installing PHP
- **Linux/Unix** → PHP can be installed via package managers (e.g., `apt`, `dnf`, `yum`) or by compiling from source.  
  - Example:  
    ```bash
    sudo apt update
    sudo apt install php php-cli php-mysql
    ```
- **Windows** → PHP can be downloaded as a binary package from [php.net](https://www.php.net/downloads). Often used together with XAMPP or WAMP for local development.  
- **macOS** → PHP can be installed with Homebrew (`brew install php`).  

- **PHP configuration** → after installation, `php.ini` defines runtime behavior (extensions, error handling, performance options).  

- **Testing installation** →  
  ```bash
  php -v
  php -m
  ```
  to check version and installed modules.

### PEAR
- **Definition** → PHP Extension and Application Repository, an older framework and distribution system for reusable PHP components.

- **Usage** → used to install libraries and extensions with a central registry (`pear install <package>`).

- **Decline** → modern projects rarely use PEAR; most libraries are distributed via Composer instead.

- **Relevance today** → important for legacy systems that still depend on old PEAR packages.

---

## Code / Command Examples
```bash
# Install PHP and extensions (Debian/Ubuntu example)
sudo apt install php php-cli php-mbstring php-xml php-curl

# Run a simple PHP script
php -r "echo 'Hello, world!';"

# Example of installing a package with PEAR
pear install HTTP_Request2
```

---

## Common Pitfalls
- Installing PHP from system repositories may not always give the latest version.

- Forgetting to configure php.ini can cause missing functionality (e.g., pdo_mysql).

- Depending on PEAR in new projects is discouraged; prefer Composer.

---

## Notes & Reflections
- Installation methods vary across operating systems, but package managers make it simple today.

- PEAR is mostly legacy knowledge, useful to understand historical PHP practices but not for new development.

- Composer has become the *de facto* standard for package management in PHP ecosystems.