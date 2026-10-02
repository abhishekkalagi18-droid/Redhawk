# Reconnaissance

## Definition

**Reconnaissance** is the process of gathering information about a target before performing further security assessment.

In cybersecurity, reconnaissance helps security professionals understand the target's externally observable infrastructure, services, technologies, and publicly available information.

Reconnaissance must only be performed against systems that are **owned by the assessor or explicitly authorized for testing**.

---

## Purpose of Reconnaissance

The primary purpose of reconnaissance is to build an accurate profile of the target.

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

---

## Information Collected

| Information | Example |
|---|---|
| Domain | `example.com` |
| Subdomain | `api.example.com` |
| IP Address | `203.0.113.10` |
| Open Port | `443/tcp` |
| Network Service | HTTPS |
| Service Version | nginx |
| DNS Records | A, MX, NS |
| HTTP Information | Status codes, headers |
| Technologies | Apache, PHP |
| Public Information | Organization-related information |

---

## Passive Reconnaissance

**Passive reconnaissance** involves collecting information without directly interacting with the target's infrastructure in a way that probes or scans its systems.

Common sources include:

- Search engines
- Public websites
- Certificate Transparency records
- Public DNS information
- Public datasets
- Internet-facing documentation
- Publicly available organization information

---

## Active Reconnaissance

**Active reconnaissance** involves directly interacting with the authorized target infrastructure to obtain technical information.

Examples include:

- Port scanning
- Service enumeration
- HTTP requests
- DNS queries
- Banner identification
- Network service discovery

Active reconnaissance should only be performed within an approved scope.

---

## Passive vs Active Reconnaissance

| Passive Reconnaissance | Active Reconnaissance |
|---|---|
| Primarily uses existing public information | Directly interacts with target infrastructure |
| Usually involves less direct interaction | Generates direct network interaction |
| Search engines | Port scanning |
| Certificate Transparency | Service enumeration |
| Public DNS information | HTTP probing |
| Public repositories | Network scanning |
| Public documents | Banner/service discovery |

---

## Reconnaissance Workflow

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

---

## Conclusion

Reconnaissance is an important stage of a security assessment because it provides information about the target before deeper analysis is performed.

For RedHawk, reconnaissance provides the data required to build an organized and useful **external asset inventory**.
