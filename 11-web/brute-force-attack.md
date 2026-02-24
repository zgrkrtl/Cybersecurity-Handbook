# Brute Forcing Attack (Web Context)

## Overview

Brute forcing is an attack technique where an attacker systematically attempts many possible inputs until the correct one is found.

In web applications, brute force attacks commonly target:

- Authentication systems (username/password)
- Hidden directories and files
- URL parameters
- Open redirection parameters
- Token-based systems

The attack relies on automation and repetition rather than exploiting a specific software vulnerability.

---

## How Brute Forcing Works in Web Applications

Web brute force attacks typically follow this pattern:

1. Identify a target endpoint (e.g., /login).
2. Send repeated HTTP requests with varying input values.
3. Analyze server responses to determine success or failure.
4. Continue until valid credentials or resources are discovered.

Attackers use tools to automate this process, allowing hundreds or thousands of requests per minute.

---

## 1. Authentication Brute Forcing

### Target:
Login forms such as:

```
POST /login
```

### Method:
The attacker submits many password guesses for a known username (or many username/password combinations).

Example pattern in logs:

```
POST /login HTTP/1.1" 200
POST /login HTTP/1.1" 200
POST /login HTTP/1.1" 200
```

Even if the server returns HTTP 200, repeated login attempts from the same IP within seconds indicate automation.

### Variations:
- Password brute force (one user, many passwords)
- Credential stuffing (known leaked credentials)
- Username enumeration

---

## 2. Directory and File Brute Forcing

Also known as directory enumeration.

### Target:
Hidden directories or files that are not publicly linked.

Examples:
```
/admin
/backup
/.git
/config.php
```

### Method:
The attacker uses wordlists to guess possible paths and monitors server responses.

Successful discovery indicators:
- HTTP 200 (exists)
- HTTP 301/302 (redirect)
- Different response size compared to 404

Example suspicious log pattern:
```
GET /admin HTTP/1.1" 404
GET /administrator HTTP/1.1" 404
GET /admin/login HTTP/1.1" 200
```

---

## 3. Open Redirection Brute Forcing

### Target:
Parameters like:

```
/redirect?url=
/login?next=
/go?target=
```

### Method:
The attacker injects different external URLs to test whether the application redirects users to arbitrary domains.

Example:
```
/redirect?url=http://evil.com
```

If the server responds with:
```
302 Found
Location: http://evil.com
```

The application may be vulnerable to open redirection.

Attackers brute force parameter names and behaviors to identify exploitable redirection logic.

---

## 4. Token and ID Brute Forcing

### Target:
- Password reset tokens
- Session identifiers
- Download links
- Numeric object IDs

Example:
```
/download?id=1001
/download?id=1002
/download?id=1003
```

If predictable IDs expose different data, this may lead to unauthorized access.

---

## Indicators of Brute Force in Logs

Common signs include:

- Multiple requests from the same IP
- Requests occurring within the same second
- Repeated access to the same endpoint
- Sequential parameter changes
- High request frequency
- Consistent User-Agent across attempts

Example suspicious pattern:

```
21:42:37 POST /login
21:42:37 POST /login
21:42:37 POST /login
21:42:37 POST /login
```

Humans cannot generate multiple login attempts in a single second. This indicates automation.

---

## Tools Commonly Used

Attackers often use automated tools such as:

- Burp Suite (Intruder)
- wfuzz
- dirsearch
- gobuster
- Hydra
- Custom Python scripts

These tools allow high-speed testing of wordlists and payload combinations.

---

## Impact

Brute force attacks can result in:

- Account compromise
- Administrative access
- Discovery of hidden functionality
- Information disclosure
- Further exploitation of the application

Even if unsuccessful, brute forcing can:

- Cause denial of service (resource exhaustion)
- Generate excessive server load
- Trigger account lockouts

---

## Prevention and Mitigation

Effective defenses include:

- Rate limiting
- Account lockout policies
- CAPTCHA challenges
- Multi-factor authentication (MFA)
- Strong password policies
- Monitoring and alerting on abnormal request patterns
- Web Application Firewall (WAF)

Proper logging and real-time monitoring are essential for detecting automated attack behavior.

