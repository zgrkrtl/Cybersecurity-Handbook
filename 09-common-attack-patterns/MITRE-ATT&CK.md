# MITRE ATT&CK – Quick Notes

## What is MITRE ATT&CK?

MITRE ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge)  
is a knowledge base of real-world attacker behaviors.

Developed and maintained by MITRE Corporation.

Purpose:
- Understand how attackers operate
- Map detections to attacker behavior
- Improve defensive coverage
- Standardize security language

---

# Core Concepts

## 1. Tactics (The "Why")

Tactics represent the attacker’s goal at a specific stage.

Examples:
- Initial Access
- Execution
- Persistence
- Privilege Escalation
- Defense Evasion
- Credential Access
- Discovery
- Lateral Movement
- Collection
- Command and Control
- Exfiltration
- Impact

Think of tactics as high-level attack objectives.

---

## 2. Techniques (The "How")

Techniques describe how attackers achieve a tactic.

Example:

Tactic: Credential Access  
Technique: Brute Force  

Each technique has a unique ID (e.g., T1110).

---

## 3. Sub-Techniques

More detailed variations of a technique.

Example:

Technique: Brute Force (T1110)  
Sub-technique: Password Spraying (T1110.003)

---

# ATT&CK Matrices

MITRE ATT&CK is divided into different matrices:

- Enterprise (Windows, Linux, macOS, Cloud, Network)
- Mobile
- ICS (Industrial Control Systems)

Enterprise matrix is the most commonly used in blue team roles.

---

# How Blue Teams Use MITRE ATT&CK

1. Map alerts to techniques (e.g., T1059 – Command and Scripting Interpreter)
2. Identify detection gaps
3. Improve SOC visibility
4. Conduct threat hunting
5. Build detection rules

Example:

If you detect:
- Suspicious PowerShell execution  
You might map it to:
T1059.001 (PowerShell)

---

# Difference from Cyber Kill Chain

Cyber Kill Chain:
- Linear model
- Focused on attack stages

MITRE ATT&CK:
- Non-linear
- Behavior-based
- Much more detailed
- Real-world technique catalog
