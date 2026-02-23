# Command Injection

## What is Command Injection?

Command Injection is a vulnerability where an attacker  
executes arbitrary system commands on the host server.

It occurs when:
- User input is passed to a system shell
- Input is not properly validated or sanitized

Target:
The underlying operating system.

---

# How It Works (Basic Concept)

Vulnerable code (conceptual):

system("ping " + user_input);

If attacker inputs:

8.8.8.8; whoami

The server executes:

ping 8.8.8.8
whoami

The second command is attacker-controlled.

---

# Why It Is Dangerous

Command injection can lead to:

- Remote Code Execution (RCE)
- Reading system files
- Creating new users
- Reverse shell access
- Full server compromise

Impact severity: Critical

---

# Common Injection Operators

Attackers may use:

;   → Command separator  
&&  → Execute if previous succeeds  
||  → Execute if previous fails  
|   → Pipe output  
` ` → Command substitution  
$() → Command substitution  

Example payload:

127.0.0.1 && cat /etc/passwd

---

# Real-World Scenarios

Common vulnerable features:

- Ping/traceroute tools
- File conversion utilities
- Backup scripts
- Image processing tools
- Admin panels

---

# Root Causes

- Direct use of system() / exec() functions
- No input validation
- Concatenating user input into shell commands
- Running applications with excessive privileges

---

# Detection Clues (Blue Team)

- Unexpected system commands in logs
- Outbound connections from web server
- Suspicious child processes (bash, sh, cmd.exe)
- Access to sensitive files (/etc/passwd, SAM)
- High CPU usage after suspicious request

---

# Prevention

## 1. Avoid Shell Execution
Do not call system commands when not necessary.

## 2. Use Safe APIs
Use language-native functions instead of shell calls.

Example:
Use file libraries instead of "cat" command.

## 3. Input Validation
Whitelist allowed values only.

## 4. Escape User Input
If shell use is unavoidable, properly escape arguments.

## 5. Least Privilege
Run services with minimal OS permissions.

---

# Command Injection vs Code Injection

Command Injection:
- Executes OS-level commands

Code Injection:
- Executes code within application context
