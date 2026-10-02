# Existing Reconnaissance Tools

## Introduction

Security professionals use a variety of tools to perform reconnaissance and attack-surface discovery. Each tool generally focuses on a specific type of information, such as network services, DNS records, public information, web technologies, or HTTP responses.

Understanding these tools is important for RedHawk because it helps identify existing capabilities and determine where a centralized workflow can provide additional value.

RedHawk is intended for **authorized security assessments and controlled lab environments**.

---

## Nmap

**Nmap (Network Mapper)** is a network discovery and security auditing tool.

It can identify:

- Live hosts
- Open ports
- Network services
- Service versions
- Operating-system information under suitable conditions

### RedHawk Relevance

Network and service discovery.

---

## theHarvester

**theHarvester** is an OSINT tool that gathers information from supported public sources.

It can help identify:

- Email addresses
- Hostnames
- Subdomains
- IP-related information
- Publicly indexed information

### RedHawk Relevance

Passive reconnaissance and OSINT.

---

## Amass

**Amass** is designed for attack-surface discovery and network mapping, particularly around domains and subdomains.

### RedHawk Relevance

Domain and subdomain discovery.

---

## DNS Tools

Tools such as **dig** are used to query DNS infrastructure.

| Record | Purpose |
|---|---|
| A | IPv4 address |
| AAAA | IPv6 address |
| MX | Mail server information |
| NS | Authoritative name servers |
| TXT | Text-based DNS information |
| CNAME | Canonical name / alias |

### RedHawk Relevance

DNS reconnaissance.

---

## WhatWeb

**WhatWeb** is a web technology identification tool.

It can help identify:

- Web servers
- Frameworks
- Content Management Systems
- Programming technologies
- JavaScript libraries

### RedHawk Relevance

Web technology fingerprinting.

---

## cURL

**cURL** is a command-line tool capable of making HTTP requests and interacting with web servers.

It can be useful for examining:

- HTTP status codes
- Response headers
- Content types
- Redirects
- Response sizes

### RedHawk Relevance

HTTP reconnaissance and response analysis.

---

## Tool Comparison

| Tool | Primary Purpose | Recon Type | RedHawk Component |
|---|---|---|---|
| **Nmap** | Host, port, and service discovery | Active | Network discovery |
| **theHarvester** | Public information collection | Passive | OSINT |
| **Amass** | Domain and attack-surface discovery | Passive + Active | Domain discovery |
| **dig** | DNS queries | Active | DNS reconnaissance |
| **WHOIS/RDAP** | Domain registration information | Passive | Domain information |
| **WhatWeb** | Web technology identification | Active | Technology fingerprinting |
| **cURL** | HTTP request/response analysis | Active | HTTP analysis |

---

## Limitations of Using Multiple Tools

### Different Output Formats

Different tools may produce results in different formats.

### Duplicate Information

Multiple tools may discover the same asset.

### Manual Correlation

An analyst may need to manually determine relationships between domains, IPs, ports, services, and technologies.

### Repetitive Workflow

Running several tools separately can require repeated configuration and result collection.

### Difficult Reporting

Producing a single report from several independent tools can require additional manual work.

---

## Relevance to RedHawk

```text
Nmap          → Network information
theHarvester  → OSINT
Amass         → Domain discovery
dig           → DNS
WhatWeb       → Technologies
cURL          → HTTP information
```

RedHawk can act as a **centralized reconnaissance orchestration and analysis layer**.

```text
                    Target
                      ↓
             RedHawk Controller
                      ↓
       ┌──────────────┼──────────────┐
       ↓              ↓              ↓
     OSINT           DNS          Network
       ↓              ↓              ↓
theHarvester         dig          Nmap
       ↓              ↓              ↓
       └──────────────┼──────────────┘
                      ↓
              Result Processing
                      ↓
                Normalization
                      ↓
               Asset Inventory
                      ↓
              Attack Surface View
                      ↓
                   Report
```

RedHawk does not necessarily need to replace specialized tools. It can provide a common workflow for selected reconnaissance capabilities, collect their outputs, normalize results, correlate assets, and present the information centrally.

---

## Conclusion

Existing reconnaissance tools provide specialized capabilities for network discovery, OSINT, DNS analysis, domain discovery, web technology identification, and HTTP analysis.

The key research finding is that the challenge is not simply collecting information, but **combining, normalizing, correlating, and presenting reconnaissance results in a useful attack-surface view**.
