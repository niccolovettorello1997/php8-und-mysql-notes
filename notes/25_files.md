# Chapter 25 – Files

## Sections
1. Preparation  
2. File Management with PHP  
3. Settings  

---

## Summary
This chapter explains how to handle **file operations in PHP**.  
File access is essential for reading, writing, and processing external resources such as logs, configuration files, and user-uploaded content.

---

## Key Concepts

### 1. Preparation
- PHP must have permission to read/write files in the filesystem.  
- File permissions (on Linux via `chmod`) and ownership must be correctly set for the webserver user.  
- `php.ini` settings:
  - `file_uploads` → enable/disable HTTP file uploads.  
  - `upload_max_filesize` and `post_max_size` → control max upload size.  
  - `open_basedir` → restrict PHP file access to a specific directory.  

---

### 2. File Management with PHP

#### Opening and Closing
```php
$file = fopen("example.txt", "r"); // r = read, w = write, a = append
if ($file) {
    // work with file
    fclose($file);
}
```

#### Reading

```php
$content = file_get_contents("example.txt");
$line = fgets($file);  // read line
$char = fgetc($file);  // read char
```

#### Writing

```php
file_put_contents("example.txt", "Hello World", FILE_APPEND);

$file = fopen("example.txt", "w");
fwrite($file, "New content\n");
fclose($file);
```

#### File Metadata

```php
if (file_exists("example.txt")) {
    echo filesize("example.txt");
    echo filemtime("example.txt"); // last modified timestamp
}
```

#### File Deletion & Renaming

```php
rename("old.txt", "new.txt");
unlink("delete.txt");
```

#### Directory Functions

```php
mkdir("newdir");
rmdir("newdir");
$files = scandir(".");
```

---

### 3. Settings

* **Memory limits**: avoid reading huge files into memory all at once → prefer streaming (`fgets()`, `fread()` in chunks).
* **Uploads**:

  * Always validate file type and size.
  * Use `move_uploaded_file()` to store uploaded files securely.
* **Security considerations**:

  * Never trust user-provided file names directly.
  * Disable `allow_url_fopen` if remote file access is not needed.

---

## Notes

* File management is **low-level but essential** for handling uploads, logs, reports, and caching.
* In modern PHP applications, file I/O is often abstracted via **framework components** or **cloud storage SDKs** (e.g., AWS S3, Google Cloud Storage).