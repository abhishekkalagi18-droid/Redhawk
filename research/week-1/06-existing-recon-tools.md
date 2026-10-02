# Existing Reconnaissance Tools

## Introduction

Security professionals use a variety of tools to perform reconnaissance and attack-surface discovery. Each tool generally focuses on a specific type of information, such as network services, DNS records, public information, web technologies, or HTTP responses.

Understanding these tools is important for RedHawk because it helps identify existing capabilities, avoid unnecessary duplication, and determine where a centralized workflow can provide additional value.

RedHawk is intended for **authorized security assessments and controlled lab environments**.

---

## Nmap

**Nmap (Network Mapper)** is a network discovery and security auditing tool.

It can be used to identify:

* Live hosts
* Open ports
* Network services
* Service versions
* Operating-system information under suitable conditions

Basic workflow:

```text
Target
  ↓
Nmap
  ↓
Open Ports
  ↓
Services
  ↓
Service Information
```

### RedHawk Relevance

Nmap can provide the **network and service discovery** component of RedHawk.

---

## theHarvester

**theHarvester** is an OSINT tool that gathers information from supported public sources.

Depending on the available sources, it can help identify:

* Email addresses
* Hostnames
* Subdomains
* IP-related information
* Publicly indexed information

Basic workflow:

```text
Target Domain
      ↓
theHarvester
      ↓
Public Sources
      ↓
Collected Information
```

### RedHawk Relevance

theHarvester can contribute to the **passive reconnaissance and OSINT** portion of RedHawk.

---

## Amass

**Amass** is designed for attack-surface discovery and network mapping, particularly around domains and subdomains.

It can help security professionals discover relationships between:

* Domains
* Subdomains
* IP addresses
* DNS information
* Other related infrastructure

Basic workflow:

```text
Target Domain
      ↓
Amass
      ↓
Domain Discovery
      ↓
Subdomains / Infrastructure
```

### RedHawk Relevance

Amass can provide capabilities related to **domain discovery and external attack-surface mapping**.

---

## DNS Tools

Tools such as **dig** are used to query DNS infrastructure.

Common DNS record types include:

| Record | Purpose                    |
| ------ | -------------------------- |
| A      | IPv4 address               |
| AAAA   | IPv6 address               |
| MX     | Mail server information    |
| NS     | Authoritative name servers |
| TXT    | Text-based DNS information |
| CNAME  | Canonical name / alias     |

Example workflow:

```text
Domain
  ↓
DNS Query
  ↓
DNS Server
  ↓
DNS Record
  ↓
Infrastructure Information
```

### RedHawk Relevance

DNS queries can provide the **DNS reconnaissance** component of RedHawk.

---

## WhatWeb

**WhatWeb** is a web technology identification tool.

It can help identify technologies associated with websites, such as:

* Web servers
* Frameworks
* Content Management Systems
* Programming technologies
* JavaScript libraries

Example:

```text
Website
   ↓
WhatWeb
   ↓
Technology Detection
   ↓
Web Technology Profile
```

### RedHawk Relevance

WhatWeb can contribute to **web technology fingerprinting**.

---

## cURL

**cURL** is a command-line tool capable of making HTTP requests and interacting with web servers.

It can be useful for examining:

* HTTP status codes
* Response headers
* Content types
* Redirects
* Response sizes
* Other HTTP response information

Example:

```text
Web Server
     ↓
   cURL
     ↓
HTTP Response
     ↓
Status + Headers + Metadata
```

### RedHawk Relevance

cURL can support **HTTP reconnaissance and response analysis**.

---

## Tool Comparison

| Tool             | Primary Purpose                     | Recon Type       | RedHawk Component         |
| ---------------- | ----------------------------------- | ---------------- | ------------------------- |
| **Nmap**         | Host, port, and service discovery   | Active           | Network discovery         |
| **theHarvester** | Public information collection       | Passive          | OSINT                     |
| **Amass**        | Domain and attack-surface discovery | Passive + Active | Domain discovery          |
| **dig**          | DNS queries                         | Active           | DNS reconnaissance        |
| **WHOIS/RDAP**   | Domain registration information     | Passive          | Domain information        |
| **WhatWeb**      | Web technology identification       | Active           | Technology fingerprinting |
| **cURL**         | HTTP request/response analysis      | Active           | HTTP analysis             |

---

## Limitations of Using Multiple Tools

Using multiple specialized tools provides broad reconnaissance capabilities, but it can also create practical problems.

### 1. Different Output Formats

Different tools may produce results in different formats.

```text
Nmap        → XML / text
theHarvester → Tool-specific output
Amass       → Text / structured output
cURL        → HTTP response data
```

Manually combining these results can be time-consuming.

### 2. Duplicate Information

Multiple tools may discover the same asset.

```text
Nmap        → 192.0.2.10
Amass       → 192.0.2.10
DNS Query   → 192.0.2.10
```

Without normalization, the final inventory may contain duplicates.

### 3. Manual Correlation

An analyst may need to manually determine that:

```text
api.example.com
       ↓
192.0.2.10
       ↓
443/tcp
       ↓
HTTPS
       ↓
Web Server
```

A centralized system can help maintain these relationships.

### 4. Repetitive Workflow

Running several tools separately can require repeated configuration, execution, and result collection.

### 5. Difficult Reporting

Producing a single report from several independent tools can require additional manual work.

---

## Relevance to RedHawk

The main observation from this research is:

```text
Nmap          → Network information
theHarvester  → OSINT
Amass         → Domain discovery
dig           → DNS
WhatWeb       → Technologies
cURL          → HTTP information
```

Each tool provides valuable information, but the results may remain separated.

RedHawk can address this workflow problem by acting as a **centralized reconnaissance orchestration and analysis layer**.

A conceptual workflow is:

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

RedHawk does **not necessarily need to replace specialized tools**.

Instead, it can provide a common workflow for selected reconnaissance capabilities, collect their outputs, normalize the results, correlate related assets, and present the information in a centralized interface.

---

## Conclusion

Existing reconnaissance tools provide specialized capabilities for network discovery, OSINT, DNS analysis, domain discovery, web technology identification, and HTTP analysis.

Tools such as Nmap, theHarvester, Amass, dig, WhatWeb, and cURL can therefore serve as references when designing RedHawk.

The key research finding is that the challenge is not simply collecting information, but **combining, normalizing, correlating, and presenting reconnaissance results in a useful attack-surface view**.

This concept will guide the next stages of RedHawk architecture and development.
