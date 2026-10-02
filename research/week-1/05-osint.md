# OSINT

## Definition

**OSINT (Open-Source Intelligence)** is the process of collecting, processing, and analyzing information from publicly available sources.

In cybersecurity, OSINT can help security professionals understand an organization's public digital presence and identify information that may contribute to an external asset inventory.

> OSINT should only involve information that is publicly available or otherwise authorized for use. It does not mean accessing private accounts, restricted systems, or unauthorized data.

---

## Cybersecurity OSINT

Cybersecurity OSINT focuses on publicly available information related to domains, infrastructure, technologies, organizations, and digital assets.

A basic OSINT workflow is:

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

For example, publicly available information may reveal:

```text
Organization
     ↓
Domain
     ↓
Subdomains
     ↓
Certificates
     ↓
DNS Information
     ↓
Public Technology Information
```

This information can help security teams understand the organization's externally visible digital presence.

---

## Common Sources

| Source                   | Possible Information                      |
| ------------------------ | ----------------------------------------- |
| Search Engines           | Public webpages and indexed documents     |
| Certificate Transparency | Domains and subdomains                    |
| WHOIS/RDAP               | Domain registration information           |
| DNS Records              | Domain infrastructure information         |
| Public Repositories      | Public project and code information       |
| Company Websites         | Public organization information           |
| Social Platforms         | Public organizational information         |
| Public Documents         | Published information and metadata        |
| Security Databases       | Previously observed technical information |

The availability, accuracy, and freshness of information vary between sources.

---

## Example

Suppose an authorized organization uses:

```text
example.com
```

An OSINT investigation may collect information from several public sources:

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

The collected information can provide an initial understanding of the organization's publicly observable assets.

---

## OSINT vs Reconnaissance

OSINT and reconnaissance are related, but they are not exactly the same.

**Reconnaissance** is the broader process of gathering information about a target before further security assessment.

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

Therefore, OSINT can be considered an important source of information within passive reconnaissance, while reconnaissance also includes active techniques.

---

## Relevant Tools

Several tools and services can support cybersecurity OSINT and reconnaissance.

### theHarvester

**theHarvester** can collect information from supported public sources, such as domains, subdomains, and related publicly available information.

### Amass

**Amass** is commonly used for attack-surface discovery and domain enumeration. It can help discover relationships between domains, subdomains, and other infrastructure.

### Nmap

**Nmap** is primarily an active reconnaissance tool used for network discovery, port scanning, and service detection.

It is therefore different from purely passive OSINT tools.

### WHOIS / RDAP Tools

WHOIS and RDAP services can provide domain registration information, depending on the registry and information available.

### Certificate Transparency Services

Certificate Transparency data can help identify domain names and subdomains that appear in publicly logged TLS certificates.

> RedHawk will initially research these tools and their capabilities. Actual tool integration will be considered during the development phase.

---

## Limitations

OSINT has several limitations:

* Public information may be outdated.
* Information may be incomplete.
* Some information may be incorrect.
* Multiple sources may contain duplicate information.
* Different sources may provide conflicting information.
* Public information does not necessarily prove that an asset is currently active.
* Some sources may have access limitations or incomplete coverage.

Therefore, collected OSINT data should be **validated, normalized, and correlated** before being treated as reliable asset information.

---

## Relevance to RedHawk

OSINT can become an important input to the RedHawk asset-discovery pipeline.

The planned workflow is:

```text
                 Authorized Target
                        ↓
                   OSINT Sources
                        ↓
        ┌───────────────┼───────────────┐
        ↓               ↓               ↓
    Subdomains         DNS           Metadata
        ↓               ↓               ↓
        └───────────────┼───────────────┘
                        ↓
                  Data Processing
                        ↓
                   Normalization
                        ↓
                  Asset Inventory
                        ↓
                Attack Surface View
```

RedHawk can eventually collect information from multiple sources and combine related results.

For example:

```text
Source 1 → api.example.com
Source 2 → api.example.com
Source 3 → dev.example.com
Source 4 → example.com
```

After processing:

```text
Asset Inventory
├── example.com
├── api.example.com
└── dev.example.com
```

This reduces duplicate information and provides a cleaner representation of the discovered attack surface.

---

## Conclusion

OSINT provides a structured approach to collecting and analyzing publicly available information about an organization's digital presence.

It can help identify domains, subdomains, DNS information, certificates, public websites, repositories, documents, and other publicly observable information.

For RedHawk, OSINT will provide an important **information source for the asset-discovery pipeline**. The collected data can later be normalized, correlated, and combined with active reconnaissance results to create a more organized external attack-surface inventory.
