# Intrusion Detection System (IDS)

## What is an Intrusion Detection System?

IDS is software or hardware that detects possible attacks by monitoring network or host activity.

---

## Types of IDS

### 1. Network IDS (NIDS)
Monitors all network traffic for possible attack patterns using automated tools.

### 2. Host IDS (HIDS)
Monitors all network traffic coming in and out of a specific host.

### 3. Protocol-Based IDS (PIDS)
Examines traffic between a server and client in a protocol-specific way.

### 4. Application Protocol-Based IDS (APIDS)
Monitors application-layer communication to catch protocol breaches.

### 5. Hybrid IDS
Combines two or more intrusion detection systems operating over a single system.

---

## How IDS Works

When a breach is detected, the information is sent to the administrator and then transferred into a **SIEM** product.

IDS detects security violations according to previously established rules. Therefore, it is very important how well the written rule defines the attack.

---

## Popular IDS Products

- Zeek/Bro
- Snort
- Suricata
- Fail2Ban
- OSSEC

---

## IDS Placement

Placement depends on the type of IDS:

- **NIDS** — should be positioned close to the networking device to monitor all passing traffic
- **HIDS** — should be placed closer to the specific host it is intended to monitor