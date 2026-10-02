# Active Reconnaissance

## Definition

**Active reconnaissance** is the process of gathering technical information by directly interacting with an authorized target.

Unlike passive reconnaissance, which primarily relies on existing public information, active reconnaissance generates requests or network traffic to the target to identify current and reachable services.

> Active reconnaissance should only be performed against systems that are owned by the assessor or explicitly authorized for testing.

A basic workflow is:

```text
Authorized Target
       ↓
  Active Recon
       ↓
 ┌─────┼─────┐
 ↓     ↓     ↓
Ports Services HTTP
 ↓     ↓     ↓
     Results
        ↓
   Asset Profile
```

---

## Objectives

The main objectives of active reconnaissance are:

* Identify reachable network services.
* Discover open ports.
* Identify services running on accessible ports.
* Determine service or software versions where possible.
* Examine HTTP responses from authorized web services.
* Verify information discovered through passive reconnaissance.
* Collect current technical information about the target.
* Build a more accurate asset profile.

---

## Techniques

### 1. Port Scanning

Port scanning identifies network ports that are accessible on a target.

Example:

```text
22/tcp  → SSH
80/tcp  → HTTP
443/tcp → HTTPS
```

This provides information about the network services that may be exposed.

---

### 2. Service Detection

After identifying an accessible port, service detection can determine what service is running.

Example:

```text
Port 22
   ↓
SSH Service
```

This provides more useful information than knowing only that a port is open.

---

### 3. Version Detection

Version detection attempts to identify the software or service version.

Example:

```text
80/tcp
   ↓
HTTP
   ↓
Web Server
   ↓
Software / Version Information
```

Version information can help security teams determine what further assessment may be appropriate.

---

### 4. HTTP Probing

HTTP probing examines how an authorized web server responds to requests.

Information may include:

* HTTP status codes
* Response headers
* Content type
* Response size
* Server information
* Redirects

Example:

```text
Web Server
    ↓
HTTP Request
    ↓
HTTP Response
    ↓
Status + Headers + Metadata
```

---

### 5. DNS Queries

DNS queries can be used to retrieve information from an authorized domain's DNS infrastructure.

Examples include:

* A records
* AAAA records
* MX records
* NS records
* TXT records

DNS information can help connect domains with network infrastructure and services.

---

### 6. Network Discovery

Network discovery can identify reachable hosts within an authorized testing scope.

For example:

```text
Authorized Network
       ↓
Host Discovery
       ↓
Reachable Hosts
       ↓
Further Service Discovery
```

---

## Example

Consider an authorized lab system:

```text
Target: 192.0.2.10
```

Active reconnaissance may produce:

```text
192.0.2.10
│
├── 22/tcp  → SSH
├── 80/tcp  → HTTP
└── 443/tcp → HTTPS
```

Further service and HTTP analysis may provide additional information about the exposed services.

This information can then be added to the asset inventory.

---

## Active Recon vs Exploitation

Active reconnaissance and exploitation are separate stages.

```text
Active Reconnaissance
        ↓
Discover Exposed Service
        ↓
Identify Service / Version
        ↓
Security Assessment
        ↓
Potential Vulnerability
        ↓
Authorized Exploitation
```

**Reconnaissance does not automatically mean exploitation.**

The primary purpose of RedHawk is to **discover, collect, normalize, and organize information**, rather than exploit discovered systems.

---

## Advantages

Active reconnaissance provides several benefits:

* Provides current technical information.
* Identifies reachable network services.
* Helps verify information discovered through passive reconnaissance.
* Provides information about exposed ports and services.
* Helps build a more complete technical asset profile.
* Provides useful input for later authorized security assessment.

---

## Limitations

Active reconnaissance also has limitations:

* Generates network traffic toward the target.
* Can be detected by security monitoring systems.
* May produce incomplete results.
* Requires explicit authorization.
* Network conditions can affect results.
* Aggressive scanning may create unnecessary load on systems.

Therefore, active reconnaissance should be carefully scoped and performed using controlled techniques.

---

## Passive and Active Reconnaissance Together

Passive and active reconnaissance provide complementary information.

```text
                  Authorized Target
                         ↓
              ┌──────────┴──────────┐
              ↓                     ↓
       Passive Recon          Active Recon
              ↓                     ↓
       Public Assets           Live Services
              ↓                     ↓
              └──────────┬──────────┘
                         ↓
                  Result Processing
                         ↓
                   Asset Inventory
                         ↓
                  Attack Surface View
                         ↓
                       Report
```

Passive reconnaissance can provide initial information, while active reconnaissance can help verify and expand that information using direct interaction with authorized infrastructure.

---

## Relevance to RedHawk

Active reconnaissance is a core component of **RedHawk — Automated Attack Surface & External Reconnaissance Suite**.

RedHawk can eventually combine passive and active reconnaissance results into a centralized asset inventory.

The planned workflow is:

```text
Authorized Target
       ↓
Passive Recon
       ↓
Initial Asset Inventory
       ↓
Active Recon
       ↓
Ports / Services / HTTP
       ↓
Result Processing
       ↓
Data Normalization
       ↓
Attack Surface View
       ↓
Report
```

RedHawk can use active reconnaissance results to enrich previously discovered assets.

For example:

```text
Passive Recon
      ↓
api.example.com
      ↓
Resolve / Verify
      ↓
IP Address
      ↓
Service Discovery
      ↓
443/tcp → HTTPS
      ↓
HTTP Analysis
      ↓
Updated Asset Profile
```

This allows information from different reconnaissance stages to be combined into a structured representation of the external attack surface.

---

## Conclusion

Active reconnaissance provides technical information by directly interacting with authorized target infrastructure.

It can identify reachable hosts, open ports, services, software versions, HTTP responses, and DNS information.

For RedHawk, active reconnaissance complements passive reconnaissance by providing **current technical information about reachable services**.

Together, both approaches provide the foundation for building an organized external attack-surface inventory for authorized security assessments.
