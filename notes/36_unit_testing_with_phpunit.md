# Chapter 36 – Unit Testing with PHPUnit

## Sections
1. Unit Tests  
2. Installing PHPUnit  
3. Testing with PHPUnit  

---

## Summary
**Unit testing** ensures that individual parts of a program (functions, classes, methods) work as expected. In PHP, the most widely used framework for unit testing is **PHPUnit**, which provides a structured way to automate testing and integrate it into the development workflow.

---

## Key Concepts

### 1. Unit Tests
- **Definition**: Automated tests that check the correctness of small, isolated pieces of code.  
- **Goals**:
  - Verify correctness of logic.  
  - Detect regressions when code changes.  
  - Facilitate refactoring with confidence.  
- **Characteristics**:
  - Should be small, isolated, and deterministic.  
  - Follow the **AAA pattern**: Arrange, Act, Assert.  

**Example**:
```php
public function testAddition(): void {
    $this->assertEquals(4, 2 + 2);
}
```

---

### 2. Installing PHPUnit

* **Composer installation (recommended)**:

  ```bash
  composer require --dev phpunit/phpunit
  ```
* **Global installation**:

  ```bash
  wget https://phar.phpunit.de/phpunit.phar
  chmod +x phpunit.phar
  sudo mv phpunit.phar /usr/local/bin/phpunit
  ```
* **Configuration**:

  * Create a `phpunit.xml` file in project root to configure test suite and settings.

Example `phpunit.xml`:

```xml
<phpunit bootstrap="vendor/autoload.php">
    <testsuites>
        <testsuite name="Project Test Suite">
            <directory>tests</directory>
        </testsuite>
    </testsuites>
</phpunit>
```

---

### 3. Testing with PHPUnit

* **Writing tests**:

  * Tests are classes that extend `PHPUnit\Framework\TestCase`.
  * Each test method should start with `test...`.
* **Assertions**:

  * `assertEquals($expected, $actual)`
  * `assertTrue($condition)`
  * `assertFalse($condition)`
  * `assertNull($value)`
  * `assertInstanceOf(ClassName::class, $object)`

**Example**:

```php
use PHPUnit\Framework\TestCase;

class MathTest extends TestCase {
    public function testMultiplication(): void {
        $this->assertEquals(9, 3 * 3);
    }
}
```

* **Running tests**:

  ```bash
  ./vendor/bin/phpunit
  ```

  or if installed globally:

  ```bash
  phpunit
  ```

* **Code Coverage** (with XDebug enabled):

  ```bash
  ./vendor/bin/phpunit --coverage-html coverage/
  ```

  Generates an HTML report showing which parts of the code are tested.

---

## Common Pitfalls

* Not isolating unit tests (mixing DB, external APIs → should be mocked).
* Writing tests only after code (instead of *test-driven development*).
* Ignoring failing tests instead of fixing the underlying issue.

---

## Notes & Best Practices

* Keep tests small and focused on a single behavior.
* Use **mocks/stubs** for dependencies (databases, APIs).
* Run tests automatically in CI/CD pipelines.
* Aim for **high coverage**, but prioritize meaningful tests over quantity.
* Combine with **integration tests** to cover the bigger picture.

---

## References / Further Reading

* [PHPUnit Documentation](https://phpunit.de/documentation.html)
* [Test Doubles in PHPUnit](https://phpunit.readthedocs.io/en/stable/test-doubles.html)
* [Martin Fowler – Unit Testing](https://martinfowler.com/bliki/UnitTest.html)