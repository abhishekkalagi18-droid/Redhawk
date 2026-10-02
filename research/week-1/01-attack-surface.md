# Attack Surface

## Definition

An **attack surface** is the complete collection of systems, services, applications, devices, and other assets that are accessible and could potentially be targeted by an attacker.

In cybersecurity, understanding the attack surface helps organizations identify what systems and services they expose and where security assessments should be focused.

---

## External Attack Surface

The **external attack surface** consists of assets that are accessible or discoverable from outside an organization's internal network.

RedHawk primarily focuses on identifying and organizing the external attack surface.

Examples include:

* Domains
* Subdomains
* Public IP addresses
* Open ports
* Network services
* Web applications
* Web technologies
* DNS records
* Publicly exposed organizational information

---

## Components

| Component          | Example                          |
| ------------------ | -------------------------------- |
| Domain             | `example.com`                    |
| Subdomain          | `api.example.com`                |
| IP Address         | `203.0.113.10`                   |
| Open Port          | `443`                            |
| Network Service    | HTTPS                            |
| Web Application    | `example.com/login`              |
| Technology         | Apache, Nginx, PHP               |
| DNS Information    | A, AAAA, MX, NS records          |
| Public Information | Organization or contact metadata |

Each component provides information about systems that are externally visible.

---

## Example

Suppose an organization owns the domain `example.com`.

Its external infrastructure may look like:

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

The domain, subdomains, public IP address, open ports, services, and detected technologies all contribute to the organization's external attack surface.

---

## Attack Surface vs Vulnerability

An **attack surface** and a **vulnerability** are related concepts, but they are not the same.

### Attack Surface

The attack surface describes **what is exposed or accessible**.

Example:

```text
Port 22 Open
      ↓
SSH Service Exposed
      ↓
Part of Attack Surface
```

### Vulnerability

A vulnerability is a **security weakness** that may exist within a system, application, configuration, or service.

Example:

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

An exposed service is not automatically vulnerable.

---

## Importance

Organizations need visibility into the systems and services they expose to the Internet.

Without proper asset discovery, an organization may have forgotten or unmanaged systems that remain publicly accessible.

For example:

```text
Unknown Asset
      ↓
Publicly Accessible
      ↓
Unmonitored Service
      ↓
Potential Security Exposure
```

Attack-surface discovery helps security teams:

* Maintain an inventory of Internet-facing assets.
* Discover unknown or forgotten assets.
* Identify exposed services.
* Understand externally visible infrastructure.
* Prioritize systems for security assessment.
* Reduce unnecessary exposure.

---

## Relevance to RedHawk

**RedHawk** is an Automated Attack Surface and External Reconnaissance Suite.

One of its primary objectives is to automate the discovery and organization of externally visible assets during authorized security assessments.

The basic RedHawk workflow is:

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
Organize and Store Results
   ↓
Attack Surface View
```

RedHawk will combine information gathered through different reconnaissance techniques and present it in an organized format.

The initial focus is **attack-surface visibility and reconnaissance rather than exploitation**.

---

## Conclusion

Understanding the attack surface is the foundation of the RedHawk project.

Before assessing security weaknesses, we first need to understand **what assets exist, which assets are publicly accessible, and what services they expose**.

This concept will guide the later reconnaissance, asset discovery, service discovery, and reporting modules of RedHawk.

---

**Project:** RedHawk — Automated Attack Surface & External Reconnaissance Suite
**Week:** 01
**Task:** 01 — Attack Surface Research
**Purpose:** Educational and authorized security assessment
