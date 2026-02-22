# Cyber Kill Chain – Quick Notes

## What is Cyber Kill Chain?

The Cyber Kill Chain is a framework developed by Lockheed Martin  
to describe the stages of a cyber attack from start to finish.

Purpose:
- Understand attacker behavior
- Detect attacks early
- Break the attack at any stage

---

# 7 Steps of the Cyber Kill Chain

## 1. Reconnaissance
Attacker gathers information about the target.

Examples:
- OSINT (LinkedIn, company website)
- Port scanning
- Email harvesting
- DNS enumeration

Goal → Identify vulnerabilities and entry points.

---

## 2. Weaponization
Attacker prepares a malicious payload.

Examples:
- Malware + exploit
- Malicious macro document
- Backdoored executable

Goal → Create attack package.

---

## 3. Delivery
Payload is delivered to the victim.

Common methods:
- Phishing email
- Malicious attachment
- USB device
- Drive-by download

Goal → Get malware to target system.

---

## 4. Exploitation
Vulnerability is triggered.

Examples:
- User clicks malicious link
- Exploit outdated software
- Macro execution

Goal → Execute malicious code.

---

## 5. Installation
Malware is installed on the system.

Examples:
- Backdoor
- Trojan
- Persistence via registry or scheduled task

Goal → Maintain access.

---

## 6. Command and Control (C2)
Compromised system connects to attacker server.

Examples:
- Reverse shell
- Beaconing traffic
- DNS tunneling

Goal → Remote control of system.

---

## 7. Actions on Objectives
Attacker completes final objective.

Examples:
- Data exfiltration
- Ransomware encryption
- Privilege escalation
- Lateral movement

Goal → Achieve mission.

---

# Defensive Insight

Breaking the chain at any stage can stop the attack.

Examples:
- Recon → Threat intelligence
- Delivery → Email filtering
- Exploitation → Patch management
- C2 → Network monitoring / SIEM

---

# Blue Team Key Takeaway

Early detection = less damage.

Most common detection points:
- Delivery
- Exploitation
- C2

Focus on:
- Logs
- Network traffic analysis
- Endpoint monitoring
- User awareness training