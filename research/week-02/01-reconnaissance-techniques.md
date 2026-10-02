# Reconnaissance Techniques


## 1. Introduction

Reconnaissance is one of the earliest and most important stages of a security assessment. The purpose of reconnaissance is to understand what assets are exposed, how those assets are connected, and what technical services are visible from an authorized external perspective.

For RedHawk, reconnaissance is not treated as a single scan. It is considered a collection of complementary techniques. Domain discovery, DNS analysis, network discovery, port scanning, HTTP analysis, technology identification, and OSINT can each reveal different parts of an organization's external attack surface.

A major objective of this research is to understand what information each technique produces and how the information can later be combined into one structured attack-surface inventory.

## 2. Domain and Subdomain Discovery

A domain represents an organization's Internet namespace, while subdomains are hostnames created beneath that domain. Organizations commonly use different subdomains for websites, APIs, mail services, development systems, authentication systems, and other applications.

For example:

```text
example.com
├── www.example.com
├── api.example.com
├── mail.example.com
├── portal.example.com
└── dev.example.com
```

A security team may not initially have a complete list of externally visible hostnames. Discovering these names can therefore help establish an initial asset inventory.

Subdomain discovery may use public information sources, certificate records, DNS information, wordlists, or other authorized discovery techniques.

### Information obtained

- Root domain
- Subdomain
- Hostname
- Associated IP address
- DNS relationship
- Discovery source

### RedHawk relevance

RedHawk can represent each discovered domain or hostname as an asset. Multiple discovery sources can then be correlated so that the same hostname is not unnecessarily stored as multiple independent assets.

## 3. DNS Reconnaissance

The Domain Name System translates human-readable domain names into information used by network systems. DNS reconnaissance examines records associated with a domain and can provide useful infrastructure context.

Important DNS records include:

| Record | Purpose |
|---|---|
| A | Maps a hostname to an IPv4 address |
| AAAA | Maps a hostname to an IPv6 address |
| MX | Identifies mail-exchange servers |
| NS | Identifies authoritative name servers |
| CNAME | Provides an alias for another hostname |
| TXT | Stores text-based configuration or verification information |

For example, an A record may associate:

```text
api.example.com → 203.0.113.10
```

This creates a relationship between a hostname and an IP address.

### RedHawk relevance

DNS information can be stored as relationships between assets. This allows the system to understand that several hostnames may point to the same infrastructure or that one hostname may be associated with another through a CNAME record.

## 4. Host and Network Discovery

Host discovery determines whether systems are reachable within an authorized scope. In an external reconnaissance context, this helps distinguish potentially active systems from addresses that do not currently respond.

Host discovery can be affected by firewalls, routing, filtering, and network configuration. Therefore, a host that does not respond to a particular discovery method should not automatically be considered nonexistent.

### RedHawk relevance

Host discovery can provide the initial set of network assets for later service discovery.

## 5. Port and Service Discovery

A network service normally listens on a specific port. Port scanning identifies accessible ports and can provide an initial view of the services exposed by a host.

Example:

```text
22/tcp   → SSH
80/tcp   → HTTP
443/tcp  → HTTPS
```

A port being open does not mean the associated service is vulnerable. It only indicates that a service appears to be accessible through that port.

Service detection can provide additional information such as the service name and, when detectable, its version.

### RedHawk relevance

Port and service information can become part of the asset inventory:

```text
Host
 └── Port
      └── Service
           └── Version
```

This structure will later support reporting and security analysis.

## 6. HTTP and HTTPS Reconnaissance

Web applications expose information through HTTP or HTTPS responses. HTTP reconnaissance examines these responses to understand how a web service behaves.

Useful information can include:

- HTTP status code
- Content type
- Response headers
- Redirect destination
- Response size
- Server information when exposed

Common response codes include:

| Status | General meaning |
|---|---|
| 200 | Successful response |
| 301 | Permanent redirect |
| 302 | Temporary redirect |
| 403 | Access forbidden |
| 404 | Resource not found |
| 500 | Server-side error |

HTTP reconnaissance can help identify accessible web services and distinguish different application behaviors.

## 7. Technology Identification

Technology identification attempts to determine technologies used by a web application or server.

Examples may include:

- Web server software
- CMS platforms
- Programming technologies
- Frameworks
- JavaScript libraries

Technology identification should be considered an observation rather than absolute proof. Fingerprinting methods can produce false positives or incomplete results.

### RedHawk relevance

Technology information can be linked to a web asset:

```text
api.example.com
 ├── HTTPS
 ├── Web Server
 ├── Framework
 └── Detected Technologies
```

## 8. OSINT Collection

Open-Source Intelligence involves collecting information from publicly available sources. In cybersecurity reconnaissance, OSINT can supplement technical discovery.

Potential sources include:

- Public search engines
- Certificate transparency data
- Public DNS information
- Public repositories
- Public documentation
- Domain registration information

OSINT is valuable because some information may be discoverable without directly interacting with the target infrastructure.

## 9. Result Normalization

Different reconnaissance tools produce different output structures. One tool may produce plain text, another XML, JSON, or tabular output.

For RedHawk, the results should be converted into a common internal structure.

Conceptual example:

```text
Raw Tool Output
       ↓
Parser
       ↓
Validation
       ↓
Normalization
       ↓
Asset Record
```

A normalized asset could contain:

```text
Asset
 ├── type
 ├── value
 ├── source
 ├── discovery_time
 └── relationships
```

## 10. Reconnaissance Workflow for RedHawk

The research suggests the following workflow:

```text
Authorized Target
       ↓
Domain / Target Validation
       ↓
Passive Discovery
       ↓
DNS Discovery
       ↓
Host Discovery
       ↓
Port & Service Discovery
       ↓
HTTP Reconnaissance
       ↓
Technology Identification
       ↓
Result Normalization
       ↓
Asset Inventory
```

The actual execution order can later be changed depending on the target type and module dependencies.

## 11. Limitations

Reconnaissance results are observations and may not represent the complete attack surface.

Reasons include:

- Firewalls may block probes.
- DNS records may change.
- Public sources may contain outdated information.
- Services may behave differently depending on the scan.
- Technology fingerprinting may be inaccurate.
- Different tools may produce conflicting results.

RedHawk should therefore preserve the source and timestamp of important observations.

## 12. Conclusion

The research shows that no single reconnaissance technique provides a complete view of an external attack surface. Domain discovery identifies naming relationships, DNS provides infrastructure information, network discovery identifies reachable systems, port scanning identifies exposed services, HTTP reconnaissance characterizes web services, and OSINT provides publicly available context.

RedHawk can combine these techniques into a centralized workflow and convert their outputs into a structured asset inventory.
