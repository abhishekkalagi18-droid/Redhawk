# Passive Reconnaissance

## Definition

**Passive reconnaissance** is the process of gathering information about a target primarily through publicly available sources without directly probing or scanning the target's infrastructure.

It is generally used as an initial information-gathering phase before performing active security assessment.

> Passive reconnaissance should only be used for legitimate security research and authorized assessments.

---

## Objectives

The main objectives are:

- Identify publicly known assets.
- Discover domains and subdomains.
- Collect publicly available DNS information.
- Identify information contained in public certificates.
- Find publicly available organizational information.
- Build an initial asset inventory.
- Reduce unnecessary direct interaction with the target.
- Provide information that can guide later authorized assessment activities.

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

| Source | Information That May Be Available |
|---|---|
| Search Engines | Publicly indexed pages and documents |
| Certificate Transparency | Domains and subdomains included in certificates |
| WHOIS/RDAP | Domain registration information |
| Public DNS Data | DNS records and related information |
| Public Websites | Organization and infrastructure information |
| GitHub/Public Repositories | Publicly exposed project information |
| Security Databases | Previously observed infrastructure |
| Public Documents | Metadata and organizational information |

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

---

## Passive vs Active Reconnaissance

| Passive Reconnaissance | Active Reconnaissance |
|---|---|
| Primarily uses existing public information | Directly interacts with target infrastructure |
| Usually involves less direct interaction | Generates direct network interaction |
| Search engines | Port scanning |
| Certificate Transparency | Service enumeration |
| Public DNS information | HTTP probing |
| Public repositories | Network scanning |
| Public documents | Banner/service discovery |

---

## Advantages

- Low direct interaction
- Initial asset discovery
- Useful for planning
- Reduced unnecessary scanning
- Broad information sources

---

## Limitations

Passive reconnaissance has several limitations:

- Public information may be outdated.
- Some assets may not appear in public sources.
- Information can be incomplete.
- Different sources may contain conflicting information.
- A discovered domain does not necessarily mean the associated system is currently active.
- Publicly available information may require validation.

Therefore, passive reconnaissance should be treated as an **initial information-gathering stage**, not a complete representation of the target.

---

## Relevance to RedHawk

Passive reconnaissance is an important component of **RedHawk — Automated Attack Surface & External Reconnaissance Suite**.

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

RedHawk can eventually collect results from multiple passive sources, normalize the information, remove duplicates, and organize the discovered assets.

---

## Conclusion

Passive reconnaissance provides a low-interaction method for collecting publicly available information about an authorized target.

For RedHawk, it provides the **initial data layer** needed to build an organized external asset inventory before moving toward active reconnaissance.
