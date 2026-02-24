# XML External Entity (XXE) Attack

## Overview

XML External Entity (XXE) is a web security vulnerability that occurs when an application processes XML input containing external entity references.

If XML parsers are configured insecurely, attackers can define external entities that access local files, internal services, or remote resources.

XXE exploits improper handling of XML input.

---

## How XML Works

XML (Extensible Markup Language) allows structured data representation.

XML supports entities, which are placeholders that can be defined inside a DOCTYPE declaration.

Example:

```xml
<!DOCTYPE note [
  <!ENTITY example "Hello World">
]>
<note>
  <message>&example;</message>
</note>
```

Entities can also reference external resources.

---

## What Causes XXE?

XXE occurs when:

- The application accepts XML input.
- The XML parser allows external entity resolution.
- User-controlled input is processed without disabling dangerous XML features.

---

## Basic XXE Payload Example

```xml
<!DOCTYPE foo [
  <!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<user>
  <name>&xxe;</name>
</user>
```

If vulnerable, the server may return the contents of:

```
/etc/passwd
```

---

## Common XXE Impacts

XXE can allow attackers to:

- Read local files (e.g., /etc/passwd)
- Access internal network services (SSRF)
- Perform denial of service (Billion Laughs attack)
- Extract application source code
- Bypass access controls

---

## Types of XXE Attacks

### 1. In-Band XXE
The server returns the extracted data directly in the response.

### 2. Blind XXE
The response does not contain file contents, but external interaction confirms exploitation.

### 3. Out-of-Band (OOB) XXE
The server sends data to an attacker-controlled external system.

---

## Example Vulnerable Scenario

HTTP request:

```
POST /api
Content-Type: application/xml

<stockCheck>
  <productId>1</productId>
</stockCheck>
```

If the attacker injects malicious XML inside `productId` and the server processes it insecurely, that parameter is vulnerable to XXE.

---

## Indicators of XXE Risk

Applications are more likely vulnerable if they:

- Accept XML input
- Use older XML libraries
- Do not disable DTD processing
- Allow external entity resolution

---

## Prevention

To prevent XXE:

- Disable DTD processing in XML parsers.
- Disable external entity resolution.
- Use secure XML parser configurations.
- Validate and sanitize user input.
- Prefer JSON instead of XML when possible.

Modern XML libraries provide secure configuration options to prevent XXE if properly configured.

