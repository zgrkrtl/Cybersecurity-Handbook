# Directory Traversal Attack

## Overview

Directory Traversal (also known as Path Traversal or Dot-Dot-Slash attack) is a web application vulnerability that allows attackers to access files and directories outside of the intended web root directory.

This attack occurs when user input is improperly validated and is directly used to construct file paths on the server.

---

## How Directory Traversal Works

Web applications sometimes use user-supplied input to retrieve files.

Example vulnerable PHP code:

```php
$file = $_GET['file'];
readfile("uploads/" . $file);
```

If an attacker supplies:

```
?file=../../../../etc/passwd
```

The application may resolve the path as:

```
/etc/passwd
```

Instead of restricting access to the `uploads/` directory.

The `../` sequence moves one directory up in the file system hierarchy.

---

## Common Payload Patterns

### Basic Traversal
```
../
..\
```

### URL Encoded Traversal
```
%2e%2e%2f
..%2f
%2e%2e/
```

### Double Encoded Traversal
```
%252e%252e%252f
```

### Sensitive File Targets

Linux systems:
```
/etc/passwd
/etc/shadow
```

Windows systems:
```
C:\Windows\win.ini
C:\boot.ini
```

---

## Log Detection (Blue Team Perspective)

When analyzing web server logs (e.g., nginx or apache access.log), look for:

- `../` patterns
- `%2e%2e%2f` or other encoded variations
- Attempts to access system files
- Multiple similar requests from the same IP
- Many requests occurring within the same second
- Suspicious or automated User-Agent strings (e.g., curl, python-requests)

Example suspicious log entry:

```
GET /index.php?file=../../../../etc/passwd HTTP/1.1
```

Repeated variations like:

```
?page=../etc/passwd
?page=../../etc/passwd
?page=../../../etc/passwd
```

Often indicate automated scanning.

---

## Impact

If successful, Directory Traversal can result in:

- Exposure of sensitive system files
- Disclosure of configuration files
- Leakage of credentials
- Access to application source code
- Information gathering for further exploitation

In some cases, it may lead to more severe attacks if combined with other vulnerabilities.

---

## Directory Traversal vs Local File Inclusion (LFI)

Directory Traversal:
- Manipulates file paths.
- Focuses on accessing unauthorized files.
- Primarily results in information disclosure.

Local File Inclusion (LFI):
- Uses inclusion functions such as `include()` or `require()`.
- Can execute included files within the application.
- May lead to Remote Code Execution (RCE).

Directory Traversal is often used as a technique during LFI exploitation, but they are not the same vulnerability.

---

## Prevention

To prevent Directory Traversal vulnerabilities:

- Validate and sanitize all user input.
- Use allowlists for permitted filenames.
- Normalize file paths before processing.
- Avoid direct string concatenation for file paths.
- Implement proper access controls.
- Run applications with least privilege.
- Use secure frameworks and built-in file handling mechanisms.
