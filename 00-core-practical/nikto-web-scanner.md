# Nikto Web Server Scanner

## Overview

Nikto is an open-source web server scanner used to identify common vulnerabilities and misconfigurations in web servers. It checks for:

- Dangerous files and programs
- Outdated server software
- Version-specific vulnerabilities
- Default files and configurations
- SSL issues
- Misconfigured headers

Official documentation:
https://cirt.net/Nikto2

GitHub repository:
https://github.com/sullo/nikto


## Basic Usage

```bash
nikto -h <target>
```

If running manually:

```bash
perl nikto.pl -h <target>
```

Example:

```bash
nikto -h example.com
```

---

## Practical Examples

Scan an IP:

```bash
nikto -h 192.168.1.10
```

Scan HTTPS:

```bash
nikto -h example.com -ssl
```

Scan specific port:

```bash
nikto -h example.com -p 8080
```

Save output:

```bash
nikto -h example.com -output scan.txt
```

Save as HTML:

```bash
nikto -h example.com -Format html -output report.html
```

Run specific plugins:

```bash
nikto -h example.com -Plugins "apache_users,ssl"
```

Use tuning option:

```bash
nikto -h example.com -Tuning 2
```

---

## Notes

- Nikto is not stealthy and will generate many log entries.
- It reports vulnerabilities but does not exploit them.
- Only scan systems you are authorized to test.
- Useful during reconnaissance and initial web assessment phase.

---

## Quick Cheat Sheet

```bash
nikto -h target.com
nikto -h target.com -ssl
nikto -h target.com -p 8080
nikto -h target.com -output results.txt
nikto -h target.com -Format html -output report.html
```