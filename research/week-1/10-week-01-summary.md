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

The research was focused on understanding the problem domain before beginning implementation.

---

## Key Findings

### Attack Surface

An attack surface consists of externally observable or accessible assets that may require security assessment.

Examples include:

```text id="v5m2g8"
Domains
Subdomains
IP Addresses
Ports
Services
Web Applications
Technologies
DNS Information
```

Understanding the attack surface is an important foundation for security assessment.

---

### Reconnaissance

Reconnaissance is the process of gathering information about an authorized target before further security assessment.

A general workflow is:

```text id="m1k8qv"
Target
  ↓
Information Gathering
  ↓
Asset Discovery
  ↓
Technical Information
  ↓
Target Profile
```

---

### Passive Reconnaissance

Passive reconnaissance primarily uses publicly available information without directly probing the target infrastructure.

Examples include:

* Search engines
* Certificate Transparency
* Public DNS information
* WHOIS/RDAP
* Public repositories
* Public documents

Passive reconnaissance can provide an initial asset inventory.

---

### Active Reconnaissance

Active reconnaissance directly interacts with an authorized target to collect technical information.

Examples include:

* Port scanning
* Service detection
* HTTP analysis
* DNS queries
* Network discovery

Active reconnaissance can help verify and expand information discovered through passive methods.

---

### OSINT

**OSINT (Open-Source Intelligence)** involves collecting, processing, and analyzing information from publicly available sources.

OSINT can contribute to passive reconnaissance by providing information about an organization's public digital presence.

---

## Existing Tools Studied

The following tools and technologies were researched:

| Tool             | Primary Purpose                     |
| ---------------- | ----------------------------------- |
| **Nmap**         | Host, port, and service discovery   |
| **theHarvester** | Public OSINT collection             |
| **Amass**        | Domain and attack-surface discovery |
| **dig**          | DNS queries                         |
| **WHOIS/RDAP**   | Domain registration information     |
| **WhatWeb**      | Web technology identification       |
| **cURL**         | HTTP request/response analysis      |

The research showed that each tool specializes in different types of reconnaissance information.

---

## Identified Problems

Using multiple reconnaissance tools independently can create several workflow challenges:

### 1. Scattered Results

Information may be distributed across different terminals, files, and output formats.

### 2. Repetitive Work

Analysts may need to repeatedly execute tools, save results, compare outputs, and prepare summaries.

### 3. Duplicate Information

Different tools may discover the same domains, IP addresses, or other assets.

### 4. Difficult Asset Tracking

Managing a growing number of domains, subdomains, IP addresses, ports, and services manually becomes increasingly difficult.

### 5. Lack of Centralized Visibility

There may be no single interface showing the complete externally discovered attack surface.

### 6. Human Error

Manual workflows can result in missed assets, incorrect copying, duplicate records, or inconsistent organization.

---

## Proposed RedHawk Solution

RedHawk is proposed as a centralized reconnaissance and attack-surface management platform.

The conceptual workflow is:

```text id="n9r3xe"
                 Authorized Target
                        ↓
                 Reconnaissance
                        ↓
                  Asset Discovery
                        ↓
                 Result Collection
                        ↓
              Processing & Normalization
                        ↓
                  Asset Inventory
                        ↓
                     Dashboard
                        ↓
                      Report
```

The objective is to collect information from selected reconnaissance capabilities, process the results, organize discovered assets, and present them through a centralized interface.

RedHawk is intended to **complement specialized reconnaissance tools rather than replace every existing tool**.

---

## Requirements

The research identified the following major system requirements.

### Functional Requirements

RedHawk should support:

* Target management.
* Domain and subdomain discovery.
* DNS information collection.
* Port discovery.
* Service detection.
* HTTP information collection.
* Technology identification.
* Result collection and processing.
* Result normalization.
* Duplicate handling.
* Asset inventory.
* Dashboard visualization.
* Report generation.

### Non-Functional Requirements

The system should provide:

* Usability
* Performance
* Reliability
* Security
* Scalability
* Maintainability
* Data accuracy

---

## Objectives

The main objective of RedHawk is:

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

```text id="n0v0l5"
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

* Automatically exploit vulnerabilities.
* Perform unauthorized scanning.
* Conduct destructive testing.
* Replace every specialized security tool.
* Guarantee that automated results are always accurate.

Active reconnaissance must only be performed against **authorized targets and within an approved scope**.

---

## Week 1 Research Outcome

The Week 1 research established:

```text id="n2zy2k"
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

The research indicates that the main challenge is not simply collecting reconnaissance data, but **organizing, normalizing, correlating, and presenting information from multiple sources in a centralized manner**.

Therefore, the next project phases can focus on translating these research findings into a technical architecture and implementation plan.

**Week 1 Status: Research and Requirements Foundation Completed.**
