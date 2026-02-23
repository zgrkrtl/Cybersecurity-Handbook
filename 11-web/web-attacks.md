# Web Attacks – Quick Notes

## What Are Web Attacks?

Web attacks target web applications, APIs, or users through browsers.

They usually exploit:
- Input validation flaws
- Authentication weaknesses
- Session management issues
- Server misconfigurations

Most modern breaches involve web components.

---

# Common Web Attacks

## 1. SQL Injection (SQLi)

Attacker injects malicious SQL queries into input fields.

Example:
- Login form
- Search box
- URL parameter

Impact:
- Bypass authentication
- Dump database
- Modify or delete data

---

## 2. Cross-Site Scripting (XSS)

Attacker injects malicious JavaScript into a web page.

Types:
- Reflected XSS
- Stored XSS
- DOM-based XSS

Impact:
- Steal cookies
- Session hijacking
- Redirect users
- Deface page

---

## 3. Cross-Site Request Forgery (CSRF)

Victim is tricked into making an unwanted request  
while authenticated to a website.

Impact:
- Change password
- Transfer money
- Modify account settings

---

## 4. Server-Side Request Forgery (SSRF)

Attacker forces the server to make internal requests.

Impact:
- Access internal services
- Cloud metadata exposure
- Internal network scanning

---

## 5. Directory Traversal

Attacker accesses files outside intended directory.

Example:
Impact:
- Read sensitive files
- Access configuration data

---

## 6. File Upload Vulnerabilities

Improper validation of uploaded files.

Impact:
- Upload web shell
- Remote code execution
- Server compromise

---

## 7. Authentication Attacks

Examples:
- Brute force
- Credential stuffing
- Session fixation
- Broken access control

Impact:
- Account takeover
- Privilege escalation

---

# Common Root Causes

- Lack of input validation
- No output encoding
- Weak authentication logic
- Misconfigured server
- Missing security headers

---

# Detection Clues (Blue Team)

- Suspicious SQL patterns in logs
- Unexpected special characters in requests
- Repeated login failures
- Large number of POST requests
- Requests to unusual endpoints
- Access to hidden or admin paths

---

# Prevention Measures

- Input validation & sanitization
- Parameterized queries
- Output encoding
- CSRF tokens
- Content Security Policy (CSP)
- Web Application Firewall (WAF)
- Proper authentication & authorization controls