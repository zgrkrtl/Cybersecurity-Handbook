# SQL Injection

## What is SQL Injection?

SQL Injection is a web attack where an attacker injects malicious SQL code  
into an application's database query.

It happens when:
- User input is not properly validated
- Queries are built using string concatenation

Goal:
- Bypass authentication
- Read sensitive data
- Modify or delete data
- Execute administrative operations

---

# How It Works

Vulnerable code (conceptual):

SELECT * FROM users WHERE username = 'input' AND password = 'input';

If attacker enters:

' OR '1'='1

The query becomes:

SELECT * FROM users WHERE username = '' OR '1'='1' AND password = '';

Since '1'='1' is always true → authentication bypass.

---

# Types of SQL Injection

## 1. Classic (In-Band) SQLi
Attacker receives results directly in the response.

Includes:
- Error-based SQLi
- Union-based SQLi

---

## 2. Blind SQL Injection
No visible error messages or output.

Attacker infers results using:
- True/False responses
- Time delays (Time-based SQLi)

---

## 3. Out-of-Band SQLi
Data is exfiltrated via another channel  
(e.g., DNS or HTTP request).

---

# Common Impact

- Dump entire database
- Extract user credentials
- Privilege escalation
- Delete tables
- Remote code execution (in some configurations)

---

# Root Causes

- Dynamic query building
- No input validation
- No parameterized queries
- Excessive database privileges

---

# Detection Clues (Blue Team)

- SQL keywords in URL parameters (UNION, SELECT, DROP)
- Unusual database errors
- Long response times (time-based SQLi)
- Large data responses unexpectedly
- Repeated login bypass attempts

Example suspicious request pattern:
?id=1 UNION SELECT username,password FROM users

---

# Prevention

## 1. Use Parameterized Queries (Prepared Statements)
Prevents injected input from being executed as SQL code.

## 2. Use ORM Frameworks
Reduces direct query manipulation.

## 3. Input Validation
Whitelist expected formats.

## 4. Least Privilege
Database user should not have admin rights.

## 5. Web Application Firewall (WAF)
Can block common injection patterns.

---

# Real-World Risk

SQL Injection has been responsible for:
- Massive data breaches
- Credential leaks
- Financial loss

It remains one of the most critical web vulnerabilities.
