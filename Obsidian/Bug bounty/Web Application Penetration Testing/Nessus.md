---
tags:
  - Automated-Tool
  - Vulnerability-Assessment
  - Vulnerability-Scanner
---

# Nessus

---

- Nessus is a proprietary vulnerability scanner developed by Tenable.
- We can utilize Nessus to perform a vulnerability scan on a target system, after which, we can import the Nessus results in to MSF for analysis and exploitation.
- Nessus automates the process of identifying vulnerabilities and also provides us with information pertinent to a vulnerability like the CVE code.
- We can use the free version of Nessus (Nessus Essentials), which allows us to scan up to 16 IPs.

## Installation

---

[Tenable Nessus Essentials Vulnerability Scanner](https://www.tenable.com/products/nessus/nessus-essentials)

```bash
chmod +x <Nessus>
```

```bash
sudo dpkg -i <Nessus>
```

```bash
sudo systemctl start nessusd.service
```


