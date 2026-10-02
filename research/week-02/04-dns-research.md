# DNS Reconnaissance Research


## Objective
Understand DNS reconnaissance and identify information useful for RedHawk.

## What is DNS?
The Domain Name System (DNS) maps domain names to network-related information.

## Important DNS Records

| Record | Purpose |
|---|---|
| A | Maps a name to an IPv4 address |
| AAAA | Maps a name to an IPv6 address |
| MX | Identifies mail servers |
| NS | Identifies authoritative name servers |
| CNAME | Provides an alias |
| TXT | Stores text/configuration information |

## Example Lab Query
For an authorized or owned domain:
```bash
dig example.com A
```

Other records can be queried with:
```bash
dig example.com MX
dig example.com NS
dig example.com TXT
```

## Information Useful to RedHawk
- Domain
- Record type
- Record value
- TTL
- Query time
- Source

## Conceptual Workflow
```text
Target Domain
     ↓
DNS Query
     ↓
DNS Response
     ↓
Parser
     ↓
Normalized DNS Records
     ↓
Asset Inventory
```

## Limitations
DNS information can change over time, may contain records unrelated to the security assessment, and does not by itself prove that a discovered host is accessible.

## RedHawk Relevance
A DNS module can provide infrastructure context and support correlation with domains, subdomains, and IP addresses discovered through other modules.
