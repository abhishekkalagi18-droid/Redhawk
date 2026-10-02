# Week 2 Summary

## RedHawk – Automated Attack Surface & External Reconnaissance Suite

## Objective
Study reconnaissance techniques and evaluate the tools that can provide the technical data required by RedHawk.

## Work Completed

### 1. Reconnaissance Techniques
Studied:
- Domain and subdomain discovery
- DNS reconnaissance
- Host/network discovery
- Port and service discovery
- HTTP/HTTPS reconnaissance
- Technology identification
- OSINT collection
- Result normalization

### 2. Tool Research
Evaluated:
- Nmap
- theHarvester
- Amass
- dig
- cURL
- WhatWeb

### 3. Tool-to-Module Mapping

```text
Nmap         → Network / Service Recon
theHarvester → OSINT
Amass        → Subdomain Recon
dig          → DNS Recon
cURL         → HTTP Recon
WhatWeb      → Technology Recon
```

## Key Findings
1. Different tools provide different types of reconnaissance data.
2. Tool outputs vary in structure and format.
3. RedHawk needs a normalization layer to convert results into consistent records.
4. Nmap can provide network/service information.
5. DNS tools provide domain infrastructure information.
6. HTTP analysis provides web-service metadata.
7. OSINT and subdomain discovery can expand the initial asset inventory.

## Proposed RedHawk Reconnaissance Pipeline

```text
Target
  ↓
Recon Modules
  ├── OSINT
  ├── DNS
  ├── Subdomain
  ├── Network
  ├── HTTP
  └── Technology
  ↓
Result Parser
  ↓
Normalization
  ↓
Asset Inventory
  ↓
Dashboard / Reports
```

## Week 2 Outcome
The reconnaissance techniques and candidate tools required for the next design phase have been identified. The findings will be used during Week 3 to design RedHawk's architecture, APIs, database structure, and module interfaces.

## Scope Note
All active reconnaissance described in this project is intended for authorized laboratory systems or systems for which explicit permission has been obtained.
