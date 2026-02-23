# Cross-Site Scripting (XSS)

## What is XSS?

Cross-Site Scripting (XSS) is a web vulnerability  
where an attacker injects malicious JavaScript  
into a web page viewed by other users.

Goal:
- Steal session cookies
- Hijack accounts
- Redirect users
- Execute actions on behalf of victim

XSS targets users, not the server directly.

---

# How It Works (Basic Idea)

1. Application displays user input without proper validation.
2. Attacker injects JavaScript code.
3. Victim loads the page.
4. Malicious script runs in victim’s browser.

Example payload:

<script>alert('XSS')</script>

If not filtered, the browser executes it.

---

# Types of XSS

## 1. Reflected XSS

- Malicious script is reflected in HTTP response.
- Usually delivered via link.
- Requires victim to click crafted URL.

Example:
search?q=<script>...</script>

---

## 2. Stored XSS

- Malicious script stored in database.
- Executes whenever users view affected page.
- More dangerous than reflected.

Example:
Comment section injection.

---

## 3. DOM-Based XSS

- Vulnerability exists in client-side JavaScript.
- Script executed due to unsafe DOM manipulation.
- No server-side reflection needed.

---

# Impact

- Session hijacking
- Credential theft
- Keylogging
- Fake login forms
- Browser-based crypto mining
- Redirect to malicious sites

If session cookies are not protected:
Attacker can impersonate user.

---

# Root Causes

- No input validation
- No output encoding
- Unsafe DOM manipulation
- Inline JavaScript handling user input

---

# Detection Clues (Blue Team)

- Suspicious <script> tags in logs
- Encoded payloads in URL (%3Cscript%3E)
- Unexpected JavaScript execution
- Alerts from Content Security Policy (CSP)
- Abnormal session activity

---

# Prevention

## 1. Output Encoding
Encode user data before rendering in HTML.

## 2. Input Validation
Restrict allowed characters where possible.

## 3. Content Security Policy (CSP)
Limit what scripts can execute.

## 4. HTTPOnly Cookies
Prevent JavaScript from accessing session cookies.

## 5. Use Modern Frameworks
Many frameworks auto-escape output by default.