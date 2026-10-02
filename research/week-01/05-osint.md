# OSINT

## Definition

**OSINT (Open-Source Intelligence)** is the process of collecting, processing, and analyzing information from publicly available sources.

In cybersecurity, OSINT can help security professionals understand an organization's public digital presence and identify information that may contribute to an external asset inventory.

> OSINT should only involve information that is publicly available or otherwise authorized for use. It does not mean accessing private accounts, restricted systems, or unauthorized data.

---

## Cybersecurity OSINT

Cybersecurity OSINT focuses on publicly available information related to domains, infrastructure, technologies, organizations, and digital assets.

```text
Target
  ↓
Public Information Sources
  ↓
Information Collection
  ↓
Data Validation
  ↓
Data Correlation
  ↓
Asset Inventory
```

---

## Common Sources

| Source | Possible Information |
|---|---|
| Search Engines | Public webpages and indexed documents |
| Certificate Transparency | Domains and subdomains |
| WHOIS/RDAP | Domain registration information |
| DNS Records | Domain infrastructure information |
| Public Repositories | Public project and code information |
| Company Websites | Public organization information |
| Social Platforms | Public organizational information |
| Public Documents | Published information and metadata |
| Security Databases | Previously observed technical information |

---

## Example

Suppose an authorized organization uses:

```text
example.com
```

An OSINT investigation may collect:

```text
                  example.com
                       ↓
                Public Sources
                       ↓
        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
       DNS        Certificates    Public Websites
        ↓              ↓              ↓
     Records       Subdomains      Metadata
        └──────────────┼──────────────┘
                       ↓
                Data Processing
                       ↓
                 Asset Inventory
```

---

## OSINT vs Reconnaissance

**Reconnaissance** is the broader process of gathering information about a target.

**OSINT** specifically focuses on information obtained from publicly available sources.

```text
Reconnaissance
│
├── Passive Reconnaissance
│      └── OSINT Sources
│
└── Active Reconnaissance
       ├── Port Scanning
       ├── Service Detection
       └── HTTP Probing
```

---

## Relevant Tools

### theHarvester

Can collect information from supported public sources, such as domains, subdomains, and related public information.

### Amass

Used for attack-surface discovery and domain enumeration.

### Nmap

Primarily an active reconnaissance tool for network discovery, port scanning, and service detection.

### WHOIS / RDAP

Can provide domain registration information, depending on the registry and information available.

### Certificate Transparency Services

Can help identify domain names and subdomains appearing in publicly logged TLS certificates.

> RedHawk will initially research these tools and their capabilities. Actual tool integration will be considered during the development phase.

---

## Limitations

OSINT data can be:

- Outdated
- Incomplete
- Incorrect
- Duplicated
- Difficult to verify

Therefore, RedHawk should **normalize, validate, and organize collected information rather than blindly trusting every result**.

---

## Relevance to RedHawk

```text
                 Target Domain
                        ↓
                   OSINT Sources
                        ↓
        ┌───────────────┼───────────────┐
        ↓               ↓               ↓
    Subdomains         DNS           Metadata
        └───────────────┼───────────────┘
                        ↓
                  Data Processing
                        ↓
                   Asset Inventory
```

OSINT can become an important information source for RedHawk's asset-discovery pipeline.
