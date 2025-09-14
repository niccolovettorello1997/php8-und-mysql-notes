# Chapter 13 – Forms

## Sections
1. Preparations  
2. Forms with PHP  
3. Form Validation  
4. Prefilling Forms  
5. File Uploads  
6. Settings  

---

## Summary
This chapter covers how to work with HTML forms in PHP: preparing the environment, creating and handling forms, validating input, prefilling data in forms, uploading files securely, and configuring form-related settings. Understanding forms is crucial since they are a primary avenue for user input, data collection, and user interaction in web apps.

---

## Key Concepts

### 1. Preparations
- Ensure `php.ini` settings allow file uploads (e.g. `upload_max_filesize`, `post_max_size`).  
- Enable required PHP extensions (`fileinfo` for MIME detection, `gd` or `imagick` if images are involved).  
- Properly configure form `method` (GET vs POST) and `enctype` for file uploads (`multipart/form-data`).  

### 2. Forms with PHP
- Use HTML `<form>` tags with `action` and `method`.  
- Handling form submission via `$_POST`, `$_GET`.  
- Sanitizing displayed data to prevent XSS (e.g. `htmlspecialchars()`).  

### 3. Form Validation
- Always validate on the server-side; client-side validation is useful only for UX.  
- Use built-in PHP functions like `filter_var()`, `preg_match()` for validating email, URLs, numbers.
- Check required fields (non empty).
- Validate input against allowed values (dropdowns, radio buttons) to avoid unexpected values.  
- Provide meaningful error messages.  

### 4. Prefilling Forms
- When form submission fails, repopulate form fields with previous user input so they don’t have to retype everything.  
- Use session variables or hidden fields to carry state.  
- Use default values if certain data is available (e.g. user data).  

### 5. File Uploads
- Use `$_FILES` superglobal.  
- Validate file size, file type, and MIME type.  
- Use `move_uploaded_file()` to safely transfer files.  
- Rename uploaded files to avoid collisions and security issues (e.g. generate unique names).  
- Store uploads outside web root or restrict access.  

### 6. Settings
- `php.ini` settings relevant for forms: `upload_max_filesize`, `post_max_size`, `max_file_uploads`, `file_uploads`.  
- Max input vars (`max_input_vars`) if form has many fields.  
- Timeout or max execution time if handling large uploads.  

---

## Common Pitfalls
- Relying only on client-side validation → bypassable.  
- Not sanitizing or escaping output in forms leads to XSS.  
- Accepting file uploads without validating type or size → security risk.  
- Forgetting to set `enctype="multipart/form-data"` for file uploads.  
- Showing error messages that reveal system details.  

---

## Notes & Reflections
- Forms are central in almost every web application; knowing how to build them securely and user-friendly is a big plus.  
- File upload functionality often reveals weak spots in security if not done properly.  
- Prefilling forms improves UX and is something interviewers often like to see demonstrated.  
- The “Settings” subsection reminds me that knowing server/PHP configuration is not separate from programming; they interact.