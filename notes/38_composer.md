# Chapter 38 – Composer

## Sections
1. Installing Composer  
2. Installing Packages with Composer  
3. Publishing Your Own Package for Composer  

---

## Summary
**Composer** is the standard dependency manager for PHP.  
It allows you to install, update, and autoload external libraries in a project, and to define your project’s dependencies in a `composer.json` file.  
Mastering Composer is essential for modern PHP development and for working with frameworks such as Symfony and Laravel.  

---

## Key Concepts

### 1. Installing Composer
- Download Composer from the official site: [getcomposer.org](https://getcomposer.org).  
- Two installation modes:
  - **Global** installation → Available system-wide (`composer` command in terminal).  
  - **Local (per project)** → `composer.phar` file inside project directory.  

**Example** (global installation on Linux/MacOS):
```bash
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
```

Verify:

```bash
composer --version
```

---

### 2. Installing Packages with Composer

* Dependencies are defined in `composer.json`.
* To add a package:

  ```bash
  composer require vendor/package-name
  ```
* Composer downloads the package into the `vendor/` directory and updates the `composer.lock` file.
* Autoloading is managed via:

  ```php
  require 'vendor/autoload.php';
  ```
* Update dependencies:

  ```bash
  composer update
  ```
* Common fields in `composer.json`:

  * `require` → Lists required packages.
  * `autoload` → Configures autoloading (PSR-4 recommended).
  * `scripts` → Defines custom commands to run.

**Example `composer.json`**:

```json
{
  "require": {
    "monolog/monolog": "^3.0"
  },
  "autoload": {
    "psr-4": {
      "App\\": "src/"
    }
  }
}
```

---

### 3. Publishing Your Own Package for Composer

* Steps:

  1. Create a **public repository** (e.g., GitHub or GitLab).
  2. Write a valid `composer.json` with metadata:

     * `name` (e.g., `yourname/package-name`)
     * `description`, `type`, `license`
     * `autoload` rules
  3. Tag a release in Git.
  4. Register the package on [Packagist.org](https://packagist.org/).

**Example `composer.json` for publishing**:

```json
{
  "name": "yourname/mypackage",
  "description": "A simple helper package",
  "type": "library",
  "license": "MIT",
  "autoload": {
    "psr-4": {
      "MyPackage\\": "src/"
    }
  },
  "require": {
    "php": ">=8.0"
  }
}
```

* After publishing, your package can be installed by others via:

  ```bash
  composer require yourname/mypackage
  ```

---

## Common Pitfalls

* Forgetting to **commit `composer.json` and `composer.lock`** to version control.
* Running `composer update` instead of `composer install` on production (may cause unexpected version changes).
* Not defining proper **semantic versioning** in `composer.json`.

---

## Notes & Best Practices

* Always use **PSR-4 autoloading** for new projects.
* Use `composer dump-autoload -o` to optimize autoloading in production.
* Keep dependencies up-to-date but follow semantic version constraints (`^`, `~`).
* For libraries, keep the public API stable and use Git tags for versioning.

---

## References / Further Reading

* [Composer Official Documentation](https://getcomposer.org/doc/)
* [Packagist – The PHP Package Repository](https://packagist.org/)
* [Semantic Versioning](https://semver.org/)