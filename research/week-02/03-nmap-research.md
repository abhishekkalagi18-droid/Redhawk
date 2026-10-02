# Nmap Research

## Week 2 – RedHawk

## Objective
Understand how Nmap can support authorized network and service reconnaissance in RedHawk.

## What is Nmap?
Nmap (Network Mapper) is a network discovery and security auditing tool. It can identify reachable hosts, open ports, services, and, depending on the scan and target, additional service or operating-system information.

## Information Relevant to RedHawk
- Target host
- Port number
- Protocol
- Port state
- Detected service
- Service version when available

Example:
```text
PORT    STATE  SERVICE
22/tcp  open   ssh
80/tcp  open   http
443/tcp open   https
```

## Basic Authorized Lab Example
```bash
nmap <authorized-lab-ip>
```

Service detection can be performed in an authorized lab with:
```bash
nmap -sV <authorized-lab-ip>
```

## Output Handling
RedHawk should not depend only on human-readable terminal output. For automation, structured Nmap output such as XML can be parsed by the backend.

Conceptual flow:
```text
Target
  ↓
Nmap
  ↓
Structured Output
  ↓
Parser
  ↓
Normalized Asset/Service Records
  ↓
Database
```

## Proposed Data Fields
- target
- host
- port
- protocol
- state
- service
- version
- scan_time

## Limitations
Nmap results depend on network conditions, scan options, firewall rules, and target configuration. Results should therefore be treated as observations that may require validation.

## RedHawk Relevance
Nmap can become the primary network/service reconnaissance module of RedHawk.
