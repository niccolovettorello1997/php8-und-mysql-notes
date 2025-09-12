# Chapter 16 – E-mail

## Sections
1. Preparations  
2. Sending E-mails with PHP  

---

## Summary
PHP provides built-in functionality for sending e-mails through the `mail()` function. This chapter covers prerequisites, configuration, and best practices for reliable e-mail delivery, as well as alternatives for production environments.

---

## Key Concepts

### 1. Preparations
- PHP requires an underlying mail transfer agent (MTA) such as **Sendmail** (Linux/Unix) or SMTP server (Windows).  
- Configuration is done in `php.ini`:  
  - On Linux: `sendmail_path` must be set.  
  - On Windows: `SMTP` and `smtp_port` must be specified.  
- For reliable usage in production, external SMTP servers (e.g., Gmail, Postfix, or third-party providers like SendGrid) are recommended.  

### 2. Sending E-mails with PHP
- **Basic syntax**:
  ```php
  $to = "user@example.com";
  $subject = "Test E-mail";
  $message = "Hello, this is a test e-mail sent from PHP!";
  $headers = "From: webmaster@example.com\r\n";
  
  mail($to, $subject, $message, $headers);
  ```

* **Headers** can include:

  * `From`, `Reply-To`, `Cc`, `Bcc`, `Content-Type`.

* **Limitations of `mail()`**:

  * No native support for authentication (SMTP AUTH).
  * Deliverability issues (often flagged as spam).
  * Lacks advanced features like attachments or HTML formatting.

* **Better alternatives**:

  * Use libraries like **PHPMailer** or **Symfony Mailer**:

    * Provide SMTP authentication.
    * Allow attachments and HTML body.
    * Support modern standards (TLS, DKIM, SPF).
  * Example with PHPMailer:

    ```php
    use PHPMailer\PHPMailer\PHPMailer;

    $mail = new PHPMailer(true);
    $mail->isSMTP();
    $mail->Host = 'smtp.example.com';
    $mail->SMTPAuth = true;
    $mail->Username = 'user@example.com';
    $mail->Password = 'password';
    $mail->SMTPSecure = 'tls';
    $mail->Port = 587;

    $mail->setFrom('user@example.com', 'Mailer');
    $mail->addAddress('recipient@example.com');
    $mail->Subject = 'Hello';
    $mail->Body    = 'This is a test message with PHPMailer.';

    $mail->send();
    ```

---

## Common Pitfalls

* Using `mail()` in production → unreliable deliverability.
* Missing `From` header → messages flagged as spam.
* Incorrect SMTP configuration in `php.ini`.
* Not handling exceptions when using external libraries.

---

## Notes & Reflections

* For learning: using `mail()` is fine to understand the basics.
* For real-world applications: always rely on PHPMailer, Symfony Mailer, or external services (SendGrid, Postmark, etc.).
* Security: never hardcode SMTP credentials directly in code; use environment variables or secret managers.