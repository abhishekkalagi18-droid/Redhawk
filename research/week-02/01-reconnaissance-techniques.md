# Reconnaissance Techniques

## Objective
Study the main reconnaissance techniques required for RedHawk and understand what information each technique can provide.

## 1. Domain and Subdomain Discovery
Domain discovery identifies the target's primary domain and related subdomains. Subdomains can represent applications, APIs, mail systems, development environments, or other externally visible services.

**Typical information:**
- Root domain
- Subdomains
- Hostnames
- Associated IP addresses

## 2. DNS Reconnaissance
DNS reconnaissance examines records associated with a domain.

Common records include:
- A – IPv4 address
- AAAA – IPv6 address
- MX – Mail server
- NS – Name server
- TXT – Text/configuration information
- CNAME – Canonical name

## 3. Host and Network Discovery
This identifies reachable hosts within an authorized scope.

## 4. Port and Service Discovery
Port scanning identifies accessible network ports. Service detection can help determine what service is operating on a port.

Example:
```text
22/tcp  -> SSH
80/tcp  -> HTTP
443/tcp -> HTTPS
```

## 5. HTTP/HTTPS Reconnaissance
HTTP reconnaissance examines web-server responses and can collect:
- Status codes
- Response headers
- Content types
- Redirects
- Response size

## 6. Technology Identification
Technology fingerprinting attempts to identify technologies used by a web application, such as web servers, frameworks, CMS platforms, and libraries.

## 7. OSINT Collection
OSINT collects information from publicly available sources. It can complement technical reconnaissance by providing additional domains, hostnames, and public information.

## 8. Result Normalization
Different tools produce different formats. RedHawk should convert useful results into a consistent internal structure.

## Week 2 Finding
RedHawk should combine multiple reconnaissance techniques rather than depend on one source. Each technique contributes a different part of the external attack-surface picture.
