# Open Redirection

## Definition
Open Redirection occurs when a web application redirects users to a URL controlled by user input without proper validation.

Example:
https://trusted.com/login?redirect=https://evil.com

If the application redirects to `evil.com`, it is vulnerable.

---

## How It Works

Application logic:

redirect(user_input)

If `user_input` is not validated, an attacker can supply an external malicious URL.

---

## Types

### 1. Server-Side (Header-Based)
Uses HTTP 3xx response with `Location` header.

Example response:
HTTP/1.1 302 Found
Location: https://evil.com

---

### 2. JavaScript-Based (DOM-Based)
Redirection handled in client-side JS.

Example:
window.location = userInput;

Usually returns HTTP 200.

---

### 3. Meta Refresh-Based
Uses HTML meta tag.

Example:
<meta http-equiv="refresh" content="0;url=https://evil.com">

---

## Common Parameters

redirect=
url=
next=
return=
continue=
dest=

---

## Impact

- Phishing
- OAuth token theft
- Bypass security filters
- Attack chaining

---

## Log Detection

Indicators:

- 3xx status codes with external `Location`
- Parameters containing `http://` or `https://`
- Encoded URLs: %3A%2F%2F
- Suspicious domains in redirect parameters

Example regex:
(redirect|url|next|return|continue)=https?:\/\/

---

## Prevention

- Allow only relative paths
- Use strict domain whitelist
- Reject full external URLs
- Normalize and validate input