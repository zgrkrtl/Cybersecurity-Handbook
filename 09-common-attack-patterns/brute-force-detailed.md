# Brute Force Attacks

Brute force attack is the name given to the activity performed to find any username, password, directory on a web page, or an encryption key by trial and error method.

It can be categorized in two:

## 1.1 Online Brute Force Attacks

Attacker and victim are online at the same time in this brute force attack type.
This can also be categorized as passive and active.

### 1.1.1 Passive Online Brute Force Attacks
In passive online brute force attacks, the attacker and the victim are on the same network but do not have direct contact with each other. The attacker tries to obtain the password in passive ways without establishing a one-to-one connection with the victim machine.

**Examples:** MITM, Sniffing

### 1.1.2 Active Online Brute Force Attacks
In active online brute force attacks, the attacker communicates directly with the victim machine and makes attempts against the relevant service running on it.

**Examples:** User/password attempts made to a web server, email server, SSH service, RDP service, or a database service.

## 1.2 Offline Brute Force Attacks

Offline brute force attacks are used against previously captured encrypted or hashed data. The attacker does not need an active connection to the victim machine. The attacker performs the attack on a password file that was somehow obtained.

**Ways to obtain the password file:**
- Capturing packets on wireless networks
- Capturing packets via a MITM attack
- Dumping hashes from a database via SQLi vulnerability
- SAM or NTDS.dit database on Windows systems

### 1.2.1 Dictionary Attacks
The attacker creates or downloads a wordlist (dictionary) of commonly used passwords. Each word in the dictionary is then tested against the target system as a password. This attack is effective because many users tend to use weak or common passwords.

### 1.2.2 Brute Force Attacks
All possible character combinations within a defined range are tried one by one. For example, if the password is up to 5 characters long, the attacker tries every possible combination of uppercase/lowercase letters, digits, and special characters from 1 to 5 characters. Attack duration depends heavily on hardware performance and password complexity.

### 1.2.3 Rainbow Table Attacks
Rainbow table attacks are a pre-computation method where hash values for all possible passwords within a certain range are calculated in advance. The attacker then compares these pre-calculated hashes against the target hash to find a match.

The main challenge is the significant **processing power and disk space** required to generate these tables. For example, computing a rainbow table for all possible passwords up to 8 characters requires substantial resources.

---
*Documentation structured and formatted with the assistance of generative AI.*