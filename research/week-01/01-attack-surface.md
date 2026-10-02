# Attack Surface

## Definition

An **attack surface** is the complete collection of systems, services, applications, devices, and other accessible assets that could potentially be targeted by an attacker.

In cybersecurity, understanding the attack surface helps security teams identify what systems and services are exposed and therefore require monitoring and security assessment.

---

## External Attack Surface

The **external attack surface** consists of assets that are accessible or discoverable from outside an organization's internal network, especially through the Internet.

Examples include:

- Domains
- Subdomains
- Public IP addresses
- Open ports
- Network services
- Websites and web applications
- APIs
- DNS records
- Internet-facing technologies
- Publicly exposed organizational information

RedHawk primarily focuses on discovering and organizing these externally visible assets.

---

## Components

| Component | Example |
|---|---|
| Domain | `example.com` |
| Subdomain | `api.example.com` |
| IP Address | `203.0.113.10` |
| Open Port | `443` |
| Network Service | HTTPS |
| Web Application | `example.com/login` |
| Technology | Apache, Nginx, PHP |
| DNS Information | A, MX, NS records |
| Public Information | Organization/contact metadata |

---

## Example

Consider an organization that owns the domain `example.com`.

```text
example.com
│
├── www.example.com
├── mail.example.com
├── api.example.com
│
├── 203.0.113.10
│   ├── 22  → SSH
│   ├── 80  → HTTP
│   └── 443 → HTTPS
│
└── Web Technologies
    ├── Apache
    └── PHP
```

The domain, subdomains, IP address, exposed ports, services, and detected technologies all contribute to the organization's external attack surface.

---

## Attack Surface vs Vulnerability

An **attack surface** and a **vulnerability** are related concepts, but they are not the same.

### Attack Surface

An attack surface describes **what is exposed or accessible**.

```text
Port 22 Open
      ↓
SSH Service Exposed
      ↓
Part of the Attack Surface
```

### Vulnerability

A vulnerability is a **security weakness** in a system, application, configuration, or service that could potentially be exploited.

```text
SSH Service
      ↓
Outdated Software Version
      ↓
Potential Vulnerability
```

Therefore:

> **Attack Surface = What is exposed**

> **Vulnerability = A weakness in what is exposed**

---

## Importance

Attack-surface discovery helps security teams:

- Identify externally visible assets.
- Maintain an inventory of domains, subdomains, IP addresses, and services.
- Detect unexpected or unknown exposed services.
- Understand the organization's Internet presence.
- Identify assets that require further security assessment.
- Reduce risks caused by unmanaged Internet-facing assets.

---

## Relevance to RedHawk

**RedHawk** is an Automated Attack Surface and External Reconnaissance Suite designed to discover, collect, and organize information about Internet-facing assets during authorized security assessments.

The basic workflow is:

```text
Target
  ↓
Asset Discovery
  ↓
Domain / Subdomain / IP Discovery
  ↓
Port & Service Discovery
  ↓
Technology & HTTP Information
  ↓
Result Collection
  ↓
Attack Surface View
```

The initial objective is **attack-surface visibility rather than exploitation**.

---

## Conclusion

Attack-surface discovery is an important first step in understanding an organization's external security exposure.

By identifying domains, subdomains, IP addresses, ports, services, technologies, and other externally visible information, security teams can build an accurate picture of what is exposed to the Internet.
