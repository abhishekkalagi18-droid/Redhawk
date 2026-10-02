# Week 1 Research Summary


Organizations can have many externally visible assets, including domains, subdomains, IP addresses, network services, and web applications.

Manually discovering and organizing these assets using multiple reconnaissance tools can become time-consuming and may result in scattered, duplicated, or difficult-to-correlate information.

**RedHawk** is proposed as a centralized platform for authorized external reconnaissance and attack-surface discovery.

---

## Research Areas

During Week 1, the following areas were studied:

1. Attack Surface
2. Reconnaissance
3. Passive Reconnaissance
4. Active Reconnaissance
5. OSINT
6. Existing Reconnaissance Tools
7. Problems with Manual Reconnaissance
8. RedHawk Requirements
9. RedHawk Objectives

The research focused on understanding the problem domain before beginning implementation.

---

## Key Findings

### Attack Surface

An attack surface consists of externally observable or accessible assets that may require security assessment.

### Reconnaissance

Reconnaissance is the process of gathering information about an authorized target before further security assessment.

### Passive Reconnaissance

Passive reconnaissance primarily uses publicly available information.

Examples:

- Search engines
- Certificate Transparency
- Public DNS information
- WHOIS/RDAP
- Public repositories

### Active Reconnaissance

Active reconnaissance directly interacts with an authorized target.

Examples:

- Port scanning
- Service detection
- HTTP analysis
- DNS queries

### OSINT

OSINT involves collecting, processing, and analyzing information from publicly available sources.

---

## Existing Tools Studied

| Tool | Primary Purpose |
|---|---|
| **Nmap** | Host, port, and service discovery |
| **theHarvester** | Public OSINT collection |
| **Amass** | Domain and attack-surface discovery |
| **dig** | DNS queries |
| **WHOIS/RDAP** | Domain registration information |
| **WhatWeb** | Web technology identification |
| **cURL** | HTTP request/response analysis |

Each tool provides different types of reconnaissance information.

---

## Identified Problems

Using multiple tools independently can result in:

- Scattered results
- Repetitive work
- Duplicate information
- Difficult asset tracking
- Lack of centralized visibility
- Human errors

---

## Proposed RedHawk Solution

RedHawk will provide a centralized workflow:

```text
Authorized Target
      ↓
Reconnaissance
      ↓
Asset Discovery
      ↓
Result Collection
      ↓
Result Processing
      ↓
Asset Inventory
      ↓
Dashboard
      ↓
Report
```

The objective is to collect information from selected reconnaissance capabilities, process the results, organize discovered assets, and present them through a centralized interface.

---

## Requirements

Major requirements identified during Week 1 include:

- Target management.
- Domain and subdomain discovery.
- DNS information collection.
- Port discovery.
- Service detection.
- HTTP information collection.
- Technology identification.
- Result collection and processing.
- Result normalization.
- Duplicate handling.
- Asset inventory.
- Dashboard visualization.
- Report generation.

Non-functional requirements include usability, performance, reliability, security, scalability, maintainability, and data accuracy.

---

## Objectives

The main objective is:

> **To develop a centralized platform that automates authorized external reconnaissance and organizes discovered attack-surface information for easier security analysis.**

Specific objectives include:

1. Automate selected reconnaissance activities.
2. Discover externally observable assets.
3. Integrate multiple reconnaissance capabilities.
4. Centralize reconnaissance results.
5. Provide attack-surface visibility.
6. Reduce duplicate information.
7. Generate structured reports.
8. Provide an extensible architecture for future modules.

---

## Project Scope

### In Scope

```text
External Reconnaissance
Attack-Surface Discovery
OSINT
DNS Reconnaissance
Domain/Subdomain Discovery
Port & Service Discovery
HTTP Analysis
Technology Identification
Result Processing
Asset Inventory
Dashboard
Reporting
```

### Out of Scope

The initial project does not aim to:

- Automatically exploit vulnerabilities.
- Perform unauthorized scanning.
- Conduct destructive testing.
- Replace every specialized security tool.
- Guarantee that automated results are always accurate.

Active reconnaissance must only be performed against **authorized targets and within an approved scope**.

---

## Week 1 Outcome

```text
Problem Domain
      ↓
Attack Surface Concepts
      ↓
Reconnaissance Concepts
      ↓
OSINT & Recon Techniques
      ↓
Existing Tools
      ↓
Manual Workflow Problems
      ↓
System Requirements
      ↓
Project Objectives
```

This research provides the foundation for designing the RedHawk architecture and planning the implementation stages.

---

## Week 1 Conclusion

Week 1 established the **problem domain, key cybersecurity concepts, existing reconnaissance tools, workflow limitations, system requirements, project scope, and objectives** for RedHawk.

The main research finding is that the challenge is not simply collecting reconnaissance data, but **organizing, normalizing, correlating, and presenting information from multiple sources in a centralized manner**.

**Week 1 Status: Research and Requirements Foundation Completed.**
