# Firewall

## What Is a Firewall?

A firewall is software or hardware that monitors in and out traffic with rules. It decides whether network packets passage.

---

## Types of Firewalls

### Application-Level Gateways (Proxy Firewalls)
Type of firewall that monitors network packets at the Application layer based on the OSI Model. It acts as a gateway between the client and the server, inspecting application-layer protocols such as HTTP, FTP, and DNS for malicious content.

### Circuit-Level Gateways
Circuit-Level Gateways are a type of firewall that can be easily configured, has low resource consumption, and has a simplified structure. These types of firewalls verify TCP connections and sessions and operate in the session layer of the OSI model.

### Cloud Firewalls
Cloud Firewalls are the type of firewall used when the institution receives firewall service over the cloud as a service. Advantage of this is there is no physical settlement for the firewall — it is obtained from a cloud server as a service.

### Endpoint Firewalls
Endpoint Firewalls are a type of host-based firewall installed on devices.
**Windows Defender Firewall** is an example of this type of firewall.

### Network Address Translation (NAT) Firewalls
Network Address Translation (NAT) Firewalls are a type of firewall designed to access internet traffic and block unwanted connections. Such firewalls are used to hide the IP addresses in the internal network from the external network. In other words, it is the firewall where NAT is applied.

### Next-Generation Firewalls (NGFW)
NGFW is a combination of different firewalls. These firewalls have a deep-packet inspection (DPI) feature. This type of firewall is designed to block external threats, malware attacks, and advanced attack methods.

### Packet-Filtering Firewalls
Packet-filtering firewalls are designed to filter and block incoming packets based on predefined rules. It is more basic compared to other firewalls and easy to implement. This ease of use comes with a disadvantage: it is inefficient at blocking web-attacks.

### Stateful Multi-Layer Inspection (SMLI) Firewalls
Stateful Multi-Layer Inspection Firewall is a type of firewall capable of both packet inspection and TCP handshake verification. With these features, it stands out from other firewalls. It also has the feature of tracking the status of established connections.

### Threat-Focused NGFW
Threat-Focused NGFW builds on standard NGFW capabilities by adding advanced threat detection and remediation. It uses indicators of compromise (IOC) to identify and react to suspicious activity, provides retrospective security to track suspicious files over time, and helps reduce time between detection and cleanup of an attack.

### Unified Threat Management (UTM) Firewalls
UTM Firewalls combine multiple security functions into a single device. They typically include a stateful firewall, VPN, antivirus, intrusion detection/prevention, content filtering, and anti-spam capabilities. They are commonly used in small to medium-sized businesses due to their all-in-one nature and ease of management.

---

## Popular Firewall Products

| Product | Notes |
|---------|-------|
| **Fortinet** | Enterprise-grade NGFW |
| **Palo Alto Networks** | Industry leading NGFW |
| **SonicWall** | SMB and enterprise firewall |
| **Checkpoint** | One of the oldest firewall vendors |
| **Juniper** | Network and security platform |
| **pfSense** | Open-source firewall/router |
| **Sophos** | Unified threat management |

---

## What Log Data Does a Firewall Have?

Firewall products have logs about network flow because they do network-based filtering. Below is some information from firewall logs:

| Field | Description |
|-------|-------------|
| Date/Time | When the event occurred |
| Source IP Address | Where the traffic originated |
| Destination IP Address | Where the traffic was going |
| Source Port | Port used by the sender |
| Destination Port | Port used by the receiver |
| Action | What the firewall did (allow/block/drop) |
| Packets Sent | Number of packets sent |
| Packets Received | Number of packets received |