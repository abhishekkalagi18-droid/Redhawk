# DNS Reconnaissance Research


## 1. Introduction

DNS is a fundamental part of Internet infrastructure. Domains and hostnames depend on DNS records to identify services and network destinations.

From a reconnaissance perspective, DNS information can help connect domain names with infrastructure. RedHawk can use DNS reconnaissance to enrich the asset inventory and establish relationships between discovered assets.

## 2. DNS Basics

The Domain Name System converts names such as:

```text
api.example.com
```

into information that network systems can use.

DNS is distributed and uses different record types for different purposes.

## 3. Important DNS Records

### A Record

Maps a hostname to an IPv4 address.

```text
api.example.com → 203.0.113.10
```

### AAAA Record

Maps a hostname to an IPv6 address.

### MX Record

Identifies mail-exchange servers associated with a domain.

### NS Record

Identifies authoritative name servers.

### CNAME Record

Creates an alias from one hostname to another.

### TXT Record

Stores text information commonly used for verification and configuration purposes.

## 4. DNS Reconnaissance Objectives

RedHawk can use DNS reconnaissance to:

1. Identify DNS records.
2. Associate hostnames with IP addresses.
3. Identify mail infrastructure.
4. Identify authoritative name servers.
5. Discover relationships between hostnames.
6. Enrich assets discovered through other reconnaissance techniques.

## 5. Using dig

`dig` is a command-line DNS query utility.

Example:

```bash
dig example.com A
```

Other queries include:

```bash
dig example.com AAAA
dig example.com MX
dig example.com NS
dig example.com TXT
```

These commands should be used against domains within an authorized assessment scope.

## 6. Understanding the Result

A DNS response may contain information such as:

```text
QUESTION SECTION
ANSWER SECTION
AUTHORITY SECTION
ADDITIONAL SECTION
```

The answer section contains records relevant to the requested query.

RedHawk should parse the useful fields rather than storing the entire response as an unstructured string.

## 7. Proposed DNS Data Model

```text
DNSRecord
├── domain
├── record_type
├── value
├── ttl
├── source
└── observed_at
```

Example:

```text
domain: api.example.com
record_type: A
value: 203.0.113.10
```

## 8. DNS Workflow in RedHawk

```text
Target Domain
      ↓
Validate Scope
      ↓
DNS Query Module
      ↓
Receive Response
      ↓
Parse Records
      ↓
Validate Data
      ↓
Normalize
      ↓
Store
      ↓
Associate With Assets
```

## 9. Correlation With Other Modules

DNS becomes more useful when correlated with other results.

Example:

```text
api.example.com
       |
       +---- A record ----> 203.0.113.10
                              |
                              +---- Nmap ----> 443/tcp
                                                |
                                                +---- HTTPS
```

This creates a richer asset profile.

## 10. Limitations

DNS information has several limitations:

- Records can change.
- Cached data can become outdated.
- Some infrastructure may not be publicly exposed through DNS.
- DNS records do not prove that a service is reachable.
- A hostname may resolve to shared infrastructure.

Therefore, DNS results should be combined with other reconnaissance observations.

## 11. Security and Privacy Considerations

RedHawk should only query domains within the authorized scope. DNS data can reveal infrastructure relationships, so collected information should be stored securely and access should be controlled.

## 12. Conclusion

DNS reconnaissance provides important infrastructure context. RedHawk can use DNS results to enrich domain and hostname records, associate assets with IP addresses, and create relationships between different discovered resources.
