# Reconnaissance Tool Evaluation

## Week 2 – RedHawk

## Objective
Evaluate existing reconnaissance tools and identify their potential role in RedHawk.

| Tool | Primary Use | Recon Type | Expected Output | Proposed RedHawk Module |
|---|---|---|---|---|
| Nmap | Port/service discovery | Active | Ports, services, versions | Network Recon |
| theHarvester | Public information collection | Passive | Hostnames, emails, related data | OSINT |
| Amass | Domain/attack-surface discovery | Passive + Active capabilities | Domains/subdomains | Subdomain Recon |
| dig | DNS queries | Active | DNS records | DNS Recon |
| cURL | HTTP analysis | Active | Status, headers, content metadata | HTTP Recon |
| WhatWeb | Technology identification | Active | Web technologies | Technology Recon |

## Nmap
Useful for discovering reachable ports and services on authorized systems.

## theHarvester
Useful for collecting supported information from public sources.

## Amass
Useful for domain and subdomain discovery and external attack-surface mapping.

## dig
Useful for querying specific DNS records and validating DNS information.

## cURL
Useful for inspecting HTTP/HTTPS responses and collecting response metadata.

## WhatWeb
Useful for identifying technologies associated with web applications.

## Evaluation Criteria
Tools should be evaluated using:
1. Information provided
2. Output format
3. Automation capability
4. Reliability
5. Ease of integration
6. Performance
7. Error handling

## Conclusion
No single tool provides complete reconnaissance coverage. RedHawk should use selected tools as specialized modules and provide a common interface for collecting and organizing their results.
