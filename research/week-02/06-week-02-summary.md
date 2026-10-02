# Week 2 Progress Summary

## RedHawk – Automated Attack Surface & External Reconnaissance Suite

## 1. Week Objective

The objective of Week 2 was to study the reconnaissance techniques required by RedHawk and evaluate existing security tools that can provide the technical information needed for external attack-surface discovery.

The work focused on understanding how different reconnaissance sources complement one another and how their outputs could eventually be integrated into a centralized system.

## 2. Research Completed

The following reconnaissance areas were studied:

### Domain and Subdomain Discovery
Research focused on identifying domains, hostnames, subdomains, and their relationships to other infrastructure.

### DNS Reconnaissance
The team studied DNS records including A, AAAA, MX, NS, CNAME, and TXT records and examined how these records can provide infrastructure context.

### Host and Network Discovery
The research examined how reachable hosts can be identified within an authorized scope and why network conditions can affect discovery results.

### Port and Service Discovery
The team studied how open ports and services contribute to an external attack-surface inventory.

### HTTP/HTTPS Reconnaissance
The research covered status codes, response headers, content types, redirects, and other web-service metadata.

### Technology Identification
The team examined how web technologies can be fingerprinted and why technology fingerprints should be treated as observations rather than absolute facts.

### OSINT
The team studied how publicly available information can complement technical reconnaissance.

### Result Normalization
The research identified the need for a common data structure because different tools produce different output formats.

## 3. Tools Evaluated

The following tools were studied:

| Tool | Main Purpose | Proposed RedHawk Module |
|---|---|---|
| Nmap | Network and service discovery | Network Recon |
| theHarvester | OSINT collection | OSINT |
| Amass | Domain/subdomain discovery | Subdomain Recon |
| dig | DNS queries | DNS Recon |
| cURL | HTTP response analysis | HTTP Recon |
| WhatWeb | Technology identification | Technology Recon |

## 4. Key Technical Findings

### Finding 1 – No Single Tool Provides Complete Coverage

Different tools specialize in different reconnaissance activities. Therefore, RedHawk should use a modular architecture rather than depend on a single tool.

### Finding 2 – Output Normalization Is Required

Tool output may be provided as text, XML, JSON, or other formats. RedHawk needs parsers that convert these results into a consistent internal representation.

### Finding 3 – Asset Correlation Is Important

A hostname discovered through OSINT may resolve to an IP address through DNS, and that IP may expose services identified by Nmap. These observations should be related.

Example:

```text
api.example.com
      |
      +---- DNS ----> 203.0.113.10
                          |
                          +---- Nmap ----> 443/tcp
                                             |
                                             +---- HTTPS
```

### Finding 4 – Source and Timestamp Should Be Preserved

Reconnaissance results can become outdated. RedHawk should record when and how an observation was collected.

### Finding 5 – Errors Must Be Part of the Design

Reconnaissance tools can fail because of timeouts, invalid input, missing dependencies, filtering, or network conditions. The backend must record failures instead of silently discarding them.

## 5. Proposed RedHawk Reconnaissance Pipeline

```text
                    Authorized Target
                           |
                           v
                  Target Validation
                           |
          +----------------+----------------+
          |                |                |
          v                v                v
        OSINT             DNS           Subdomain
          |                |                |
          +----------------+----------------+
                           |
                           v
                  Network Discovery
                           |
                           v
                 Port / Service Scan
                           |
                           v
                    HTTP Analysis
                           |
                           v
                Technology Detection
                           |
                           v
                  Result Parsers
                           |
                           v
                    Normalization
                           |
                           v
                  Asset Correlation
                           |
                           v
                    Asset Database
                           |
                  +--------+--------+
                  |                 |
                  v                 v
              Dashboard          Reports
```

## 6. Proposed Asset Model

The Week 2 research suggests that RedHawk should eventually represent several types of assets:

```text
Domain
Subdomain
IP Address
Port
Service
Web Application
Technology
DNS Record
HTTP Observation
```

These assets should be connected through relationships instead of being treated as unrelated text records.

## 7. Week 2 Outcome

By the end of Week 2, the technical reconnaissance areas required for RedHawk have been identified and the main candidate tools have been evaluated.

The research provides the foundation for designing:

- Reconnaissance modules
- Backend interfaces
- Tool execution workflow
- Output parsers
- Database entities
- Asset relationships
- Dashboard data
- Reporting structure

## 8. Transition to Week 3

The next stage is system design. Week 3 will convert the research findings into a technical architecture for RedHawk.

The planned Week 3 work will cover:

1. System architecture
2. Frontend and backend responsibilities
3. Reconnaissance engine architecture
4. Database design
5. API design
6. Data flow
7. Module interfaces
8. Project directory structure
9. Security and validation requirements

## 9. Scope and Authorization

RedHawk is designed for authorized security assessment and laboratory environments. Active reconnaissance must only be performed against systems for which appropriate permission has been obtained.
