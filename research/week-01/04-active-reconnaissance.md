# Active Reconnaissance

## Definition

**Active reconnaissance** is the process of gathering technical information by directly interacting with an authorized target.

Unlike passive reconnaissance, active reconnaissance generates requests or network traffic to the target to identify current and reachable services.

> Active reconnaissance should only be performed against systems that are owned by the assessor or explicitly authorized for testing.

---

## Objectives

The main objectives are:

- Identify reachable network services.
- Discover open ports.
- Identify services running on accessible ports.
- Determine service or software versions where possible.
- Examine HTTP responses from authorized web services.
- Verify information discovered through passive reconnaissance.
- Collect current technical information.
- Build a more accurate asset profile.

---

## Techniques

### Port Scanning

Port scanning identifies network ports that are accessible on a target.

```text
22/tcp  → SSH
80/tcp  → HTTP
443/tcp → HTTPS
```

### Service Detection

Service detection can determine what service is running on an accessible port.

```text
Port 22
   ↓
SSH Service
```

### Version Detection

Version detection attempts to identify the software or service version.

### HTTP Probing

HTTP probing examines authorized web-server responses, including:

- HTTP status codes
- Response headers
- Content type
- Response size
- Server information
- Redirects

### DNS Queries

DNS queries can retrieve information such as:

- A records
- AAAA records
- MX records
- NS records
- TXT records

### Network Discovery

Network discovery can identify reachable hosts within an authorized testing scope.

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

Further service and HTTP analysis can provide additional information about exposed services.

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

Reconnaissance does not automatically mean exploitation.

The primary purpose of RedHawk is to **discover, collect, normalize, and organize information**, rather than exploit discovered systems.

---

## Advantages

- Provides current technical information.
- Identifies reachable network services.
- Helps verify passive findings.
- Provides information about exposed ports and services.
- Helps build a technical asset profile.

---

## Limitations

- Generates network traffic toward the target.
- Can be detected by security monitoring systems.
- May produce incomplete results.
- Requires explicit authorization.
- Network conditions can affect results.
- Aggressive scanning may create unnecessary load.

---

## Relevance to RedHawk

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

Active reconnaissance complements passive reconnaissance by providing current technical information about reachable services.
