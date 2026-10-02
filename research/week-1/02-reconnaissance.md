# Reconnaissance

## Definition

**Reconnaissance** is the process of gathering information about a target before performing further security assessment.

In cybersecurity, reconnaissance helps security professionals understand the target's externally observable infrastructure, services, technologies, and publicly available information.

Reconnaissance must only be performed against systems that are **owned by the assessor or explicitly authorized for testing**.

---

## Purpose of Reconnaissance

The primary purpose of reconnaissance is to build an accurate profile of the target.

A typical workflow is:

```text
Target
  ↓
Domain / Subdomain Discovery
  ↓
IP Address Identification
  ↓
Port Discovery
  ↓
Service Identification
  ↓
DNS / HTTP Information
  ↓
Technology Identification
  ↓
Target Profile
```

Reconnaissance helps security teams understand what assets exist and which parts of the infrastructure require further security assessment.

---

## Information Collected

Reconnaissance may identify different types of information:

| Information        | Example                          |
| ------------------ | -------------------------------- |
| Domain             | `example.com`                    |
| Subdomain          | `api.example.com`                |
| IP Address         | `203.0.113.10`                   |
| Open Port          | `443/tcp`                        |
| Network Service    | HTTPS                            |
| Service Version    | nginx                            |
| DNS Records        | A, MX, NS                        |
| HTTP Information   | Status codes, headers            |
| Technologies       | Apache, PHP                      |
| Public Information | Organization-related information |

The exact information collected depends on the reconnaissance technique and the scope of the assessment.

---

## Passive Reconnaissance

**Passive reconnaissance** involves collecting information without directly interacting with the target's infrastructure in a way that probes or scans its systems.

Common sources include:

* Search engines
* Public websites
* Certificate Transparency records
* Public DNS information
* Public datasets
* Internet-facing documentation
* Publicly available organization information

Example:

```text
Public Sources
      ↓
Information Collection
      ↓
Domain / Subdomain / DNS Data
      ↓
Target Profile
```

Passive reconnaissance is useful for gathering initial information while minimizing direct interaction with the target.

---

## Active Reconnaissance

**Active reconnaissance** involves directly interacting with the authorized target infrastructure to obtain technical information.

Examples include:

* Port scanning
* Service enumeration
* HTTP requests
* DNS queries
* Banner identification
* Network service discovery

Example:

```text
Authorized Target
      ↓
Network Interaction
      ↓
Port Discovery
      ↓
Service Identification
      ↓
Technical Information
```

Active reconnaissance can generate traffic that may be detected by monitoring and security systems, so it should only be performed within an approved scope.

---

## Passive vs Active Reconnaissance

| Feature                   | Passive                       | Active                |
| ------------------------- | ----------------------------- | --------------------- |
| Direct target interaction | Minimal/none                  | Yes                   |
| Typical sources           | Public sources                | Target infrastructure |
| Network traffic to target | Usually minimal               | Yes                   |
| Example                   | Certificate records           | Port scanning         |
| Detection possibility     | Generally lower               | Generally higher      |
| Use                       | Initial information gathering | Technical discovery   |

---

## Reconnaissance Workflow

A general reconnaissance workflow can be represented as:

```text
                Authorized Target
                       ↓
              Initial Information
                       ↓
             ┌─────────┴─────────┐
             ↓                   ↓
      Passive Recon         Active Recon
             ↓                   ↓
       Public Sources       Network Services
             ↓                   ↓
             └─────────┬─────────┘
                       ↓
                Result Processing
                       ↓
                 Asset Inventory
                       ↓
                    Reports
```

The collected information can then be organized into an asset inventory for further security assessment.

---

## Relevance to RedHawk

Reconnaissance is a core component of **RedHawk — Automated Attack Surface & External Reconnaissance Suite**.

RedHawk is intended to automate and organize multiple reconnaissance activities for authorized security assessments.

The planned workflow is:

```text
User Enters Authorized Target
              ↓
        Reconnaissance
              ↓
     ┌────────┼────────┐
     ↓        ↓        ↓
    DNS     Network    HTTP
     ↓        ↓        ↓
     └────────┼────────┘
              ↓
       Result Processing
              ↓
        Asset Inventory
              ↓
       Attack Surface View
              ↓
            Reports
```

Instead of keeping information from different tools separately, RedHawk will collect and organize the results into a centralized view.

The goal is to make it easier for security professionals to understand:

* What assets were discovered
* Which domains and subdomains exist
* Which IP addresses are associated with the target
* Which services are exposed
* What HTTP information is available
* Which technologies were identified
* How the discovered assets contribute to the external attack surface

---

## Conclusion

Reconnaissance is an important stage of a security assessment because it provides information about the target before deeper analysis is performed.

It can be divided into **passive reconnaissance**, which relies primarily on publicly available information, and **active reconnaissance**, which directly interacts with authorized infrastructure.

For RedHawk, reconnaissance provides the data required to build an organized and useful **external attack-surface inventory**.
