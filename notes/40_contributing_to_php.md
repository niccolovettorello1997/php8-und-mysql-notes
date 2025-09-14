# Chapter 40 – Contributing to PHP

## Sections
1. Patches for PHP  
2. Further Opportunities  

---

## Summary
Contributing to PHP means becoming part of the **open-source community** that maintains the language.  
Developers can help by fixing bugs, improving documentation, writing tests, or even proposing new features.  
While not mandatory for a PHP career, contributing shows initiative, technical depth, and collaboration skills—qualities that are highly valued by employers.

---

## Key Concepts

### 1. Patches for PHP
- **What is a patch?**  
  A patch is a small change submitted to the PHP source code (bugfix, improvement, or feature).  
- **Workflow**:  
  1. Identify a bug (from [bugs.php.net](https://bugs.php.net/)) or a missing feature.  
  2. Fork or download PHP source code.  
  3. Create a patch using `git diff`.  
  4. Submit the patch to the PHP project for review.  

**Example command**:  
```bash
git clone https://github.com/php/php-src.git
cd php-src
# make changes
git diff > myfix.patch
```

* Patches are reviewed by the **internals mailing list** or GitHub discussions.
* High-quality patches include:

  * Clear description of the issue.
  * Minimal, focused code changes.
  * Corresponding **phpt tests** proving the fix.

---

### 2. Further Opportunities

* **Documentation**: Improve or translate docs on [php.net](https://www.php.net/docs.php).
* **Tests**: Write or improve PHPT tests to ensure language stability.
* **RFCs (Request for Comments)**: Propose new language features. Requires strong expertise and community discussion.
* **Extension Development**: Contribute to existing extensions (GD, PDO, etc.) or create new ones.
* **Community Support**: Help in mailing lists, StackOverflow, GitHub, or Slack groups.

---

## Common Pitfalls

* Submitting large, unfocused patches → hard to review and often rejected.
* Not following the project’s coding standards.
* Ignoring community discussions or feedback.

---

## Notes & Best Practices

* Start small: fix a typo, improve docs, or write a new test.
* Engage with the PHP Internals community before attempting big changes.
* Always add automated tests for any change.
* Document why your patch is needed, not just how it works.

---

## References / Further Reading

* [PHP Source Repository](https://github.com/php/php-src)
* [PHP Internals Book](http://www.phpinternalsbook.com/)
* [How to contribute to PHP](https://www.php.net/git.php)
* [PHP RFC Process](https://wiki.php.net/rfc)