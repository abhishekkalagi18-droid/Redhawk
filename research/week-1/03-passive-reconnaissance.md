# Passive Reconnaissance

## Definition

**Passive reconnaissance** is the process of gathering information about a target primarily through publicly available sources without directly probing or scanning the target's infrastructure.

It is generally used as an initial information-gathering phase before performing active security assessment.

Passive reconnaissance can help identify domains, subdomains, certificates, DNS information, public documents, and other externally available information.

> Passive reconnaissance should only be used for legitimate security research and authorized assessments.

---

## Objectives

The main objectives of passive reconnaissance are:

* Identify publicly known assets.
* Discover domains and subdomains.
* Collect publicly available DNS information.
* Identify information contained in public certificates.
* Find publicly available organizational information.
* Build an initial asset inventory.
* Reduce unnecessary direct interaction with the target.
* Provide information that can guide later authorized assessment activities.

A basic workflow is:

```text
Target Domain
      ↓
Public Sources
      ↓
Information Collection
      ↓
Data Validation
      ↓
Initial Asset Inventory
```

---

## Sources of Information

Passive reconnaissance can use several publicly available sources.

| Source                     | Information That May Be Available               |
| -------------------------- | ----------------------------------------------- |
| Search Engines             | Publicly indexed pages and documents            |
| Certificate Transparency   | Domains and subdomains included in certificates |
| WHOIS/RDAP                 | Domain registration information                 |
| Public DNS Data            | DNS records and related information             |
| Public Websites            | Organization and infrastructure information     |
| GitHub/Public Repositories | Publicly exposed project information            |
| Security Databases         | Previously observed infrastructure              |
| Public Documents           | Metadata and organizational information         |

The availability and accuracy of information depend on the target and the source.

---

## Examples

Suppose an authorized assessment is being performed for:

```text
example.com
```

Public sources may reveal:

```text
example.com
├── www.example.com
├── mail.example.com
├── api.example.com
└── dev.example.com
```

These discovered domains can become part of the initial asset inventory.

No port scan is required if the information is already available through public sources.

Another example is Certificate Transparency:

```text
Certificate Transparency
          ↓
Certificate Records
          ↓
Domain Names
          ↓
Potential Subdomains
          ↓
Asset Inventory
```

The discovered information should be validated because public records can contain outdated or inactive assets.

---

## Passive vs Active Reconnaissance

| Passive Reconnaissance                     | Active Reconnaissance                         |
| ------------------------------------------ | --------------------------------------------- |
| Primarily uses existing public information | Directly interacts with target infrastructure |
| Usually involves less direct interaction   | Generates direct network interaction          |
| Search engines                             | Port scanning                                 |
| Certificate Transparency                   | Service enumeration                           |
| Public DNS information                     | HTTP probing                                  |
| Public repositories                        | Network scanning                              |
| Public documents                           | Banner/service discovery                      |

Passive reconnaissance generally comes before active reconnaissance when building an initial target profile.

---

## Advantages

Passive reconnaissance provides several benefits:

### 1. Low Direct Interaction

Information can often be collected without directly probing the target's systems.

### 2. Initial Asset Discovery

It can reveal domains, subdomains, certificates, and other publicly observable assets.

### 3. Useful for Planning

The collected information can help determine which assets require further authorized assessment.

### 4. Reduced Unnecessary Scanning

Security teams can use existing information before performing active discovery.

### 5. Broad Information Sources

Information can be collected from multiple independent public sources.

---

## Limitations

Passive reconnaissance also has limitations:

* Public information may be outdated.
* Some assets may not appear in public sources.
* Information can be incomplete.
* Different sources may contain conflicting information.
* A discovered domain does not necessarily mean the associated system is currently active.
* Publicly available information may require validation before being used for further assessment.

Therefore, passive reconnaissance should be treated as an **initial information-gathering stage**, not a complete representation of the target.

---

## Relevance to RedHawk

Passive reconnaissance is an important component of **RedHawk — Automated Attack Surface & External Reconnaissance Suite**.

RedHawk can use passive techniques to build an initial inventory before performing active discovery.

The planned workflow is:

```text
Authorized Target Domain
          ↓
    Passive Recon
          ↓
 ┌────────┼─────────┐
 ↓        ↓         ↓
Domains  DNS     Public Data
 ↓        ↓         ↓
 └────────┼─────────┘
          ↓
    Data Normalization
          ↓
    Asset Inventory
          ↓
 Optional Active Recon
```

The RedHawk system can eventually collect results from multiple passive sources, normalize the information, remove duplicates, and organize the discovered assets.

For example:

```text
Source 1 → api.example.com
Source 2 → api.example.com
Source 3 → mail.example.com
Source 4 → dev.example.com
```

After normalization:

```text
Asset Inventory
├── api.example.com
├── mail.example.com
└── dev.example.com
```

This organized inventory can then become an input for later active reconnaissance and attack-surface analysis.

---

## Conclusion

Passive reconnaissance provides a low-interaction method for collecting publicly available information about an authorized target.

It can help identify domains, subdomains, certificates, DNS information, public documents, and other externally observable data.

For RedHawk, passive reconnaissance provides the **initial data layer** needed to build an organized external asset inventory before moving toward active reconnaissance and deeper security assessment.
