# Chapter 35 – Debugging with XDebug

## Sections
1. Manual Debugging  
2. Debugging with XDebug  

---

## Summary
Debugging is the process of identifying and fixing errors in a program. In PHP, this can be done manually (via `var_dump`, `print_r`, logs) or with advanced tools like **XDebug**, which offer breakpoints, stack traces, and performance profiling.  

---

## Key Concepts

### 1. Manual Debugging
- **Echo-based debugging**:
  - Using `echo`, `print_r()`, or `var_dump()` to display variable values.
  - Often quick but messy and not scalable for complex systems.
- **Error logs**:
  - Configure `log_errors = On` in `php.ini` and check error logs for runtime problems.
- **Limitations**:
  - No real-time insight into code flow.
  - Cannot easily track nested function calls or memory usage.

### 2. Debugging with XDebug
XDebug is a powerful PHP extension that provides in-depth debugging and profiling.

#### Main Features
- **Stack traces**: Detailed information when an error occurs (file, line, function calls).  
- **Breakpoints & step debugging**: Pause code execution and inspect variables at any point.  
- **Variable inspection**: Explore variables, objects, and arrays in real time.  
- **Code coverage**: Measure which parts of code are executed during tests.  
- **Profiling**: Performance analysis to detect bottlenecks.

#### Setup
- Install XDebug via PECL or package manager.  
- Enable in `php.ini`:  
  ```ini
  zend_extension=xdebug.so
  xdebug.mode=debug
  xdebug.start_with_request=yes
  xdebug.client_host=127.0.0.1
  xdebug.client_port=9003
  ```

* Restart the web server or PHP-FPM after enabling.
* Configure IDE (e.g., PHPStorm, VSCode) to listen for XDebug connections.

#### Usage

* Set breakpoints inside the IDE.
* Run the script; XDebug pauses execution where breakpoints are set.
* Inspect variables, step into/out of functions, or continue execution.
* Use XDebug with PHPUnit for test debugging and code coverage.

---

## Common Pitfalls

* Forgetting to enable the correct **XDebug mode** (`debug`, `develop`, `coverage`, etc.).
* Port conflicts: default changed from `9000` to `9003` in recent versions.
* Performance overhead: disable XDebug in production environments.

---

## Notes & Best Practices

* Use manual debugging only for quick checks; switch to XDebug for complex issues.
* Combine XDebug with **PHPUnit** for comprehensive test coverage analysis.
* Separate configs for development (XDebug enabled) and production (XDebug disabled).
* Use profiling sparingly to optimize performance-critical sections.

---

## References / Further Reading

* [XDebug Documentation](https://xdebug.org/docs/)
* [Debugging PHP with VSCode](https://code.visualstudio.com/docs/php/debugging)
* [Debugging PHP with PhpStorm](https://www.jetbrains.com/help/phpstorm/configuring-xdebug.html)