# Reconnaissance Tool Evaluation

## RedHawk – Automated Attack Surface & External Reconnaissance Suite

## 1. Introduction

RedHawk is intended to combine several reconnaissance capabilities into one platform. Existing security tools already perform many of these individual functions, so the purpose of this research is not to recreate every tool from scratch. Instead, RedHawk should understand the strengths, outputs, limitations, and automation possibilities of established tools.

The evaluation focuses on how each tool can contribute to a larger reconnaissance pipeline.

## 2. Evaluation Criteria

Each candidate tool is considered using the following criteria:

### Information Coverage
What type of reconnaissance information can the tool provide?

### Output Format
Can the output be consumed programmatically? Structured formats such as XML or JSON are generally easier to process than terminal-only output.

### Automation
Can RedHawk execute the tool as part of a backend workflow?

### Reliability
Does the tool provide useful results consistently under normal authorized lab conditions?

### Integration
Can its results be mapped to RedHawk's internal asset model?

### Performance
Can the tool be executed without unnecessary resource consumption or excessive delays?

### Error Handling
Can RedHawk detect and report failures instead of treating missing output as successful reconnaissance?

## 3. Nmap

Nmap is primarily used for network discovery and service enumeration.

It can provide:

- Host availability information
- Open ports
- Port states
- Service names
- Service versions when detectable
- Additional information depending on scan configuration

Nmap is particularly relevant to RedHawk because network and service information forms an important part of an external attack-surface inventory.

For automation, RedHawk should prefer structured output where practical.

## 4. theHarvester

theHarvester is an OSINT-oriented reconnaissance tool. It can collect information from supported public sources.

Depending on the source and configuration, results can include:

- Hostnames
- Email addresses
- Domain-related information
- Publicly indexed information

Its value to RedHawk is primarily in the passive reconnaissance stage.

Because external data sources can change their behavior, RedHawk should treat OSINT results as source-attributed observations rather than guaranteed facts.

## 5. Amass

Amass is focused on attack-surface discovery, particularly domain and subdomain enumeration. It can use multiple discovery techniques and data sources.

Its potential RedHawk role is:

```text
Target Domain
      ↓
Domain Discovery
      ↓
Subdomains / Related Assets
      ↓
Asset Inventory
```

Amass can therefore contribute to the early discovery phase before active service enumeration.

## 6. dig

`dig` is a DNS query utility. It provides a direct way to retrieve DNS information for a specified domain or hostname.

Example authorized query:

```bash
dig example.com A
```

Other record types can be requested:

```bash
dig example.com MX
dig example.com NS
dig example.com TXT
```

Its strength is precision and simplicity. RedHawk can use DNS queries to validate or enrich information discovered by other modules.

## 7. cURL

cURL is a general-purpose command-line tool for communicating with web servers and other network services.

For HTTP reconnaissance, it can provide information such as:

- Status code
- Response headers
- Redirect behavior
- Content type
- Response metadata

Example:

```bash
curl -I https://example.com
```

cURL is useful for a lightweight HTTP reconnaissance module because it can be controlled programmatically and its output can be processed by the backend.

## 8. WhatWeb

WhatWeb is designed to identify technologies used by websites.

Potentially detectable information can include:

- Web server software
- Frameworks
- CMS platforms
- Libraries
- Other technology indicators

Technology detection can help analysts understand the composition of a web asset. However, fingerprints can be incomplete or inaccurate, so RedHawk should store the source and avoid presenting fingerprints as guaranteed facts.

## 9. Tool Comparison

| Tool | Main Function | Input | Main Output | RedHawk Role |
|---|---|---|---|---|
| Nmap | Network/service discovery | Host/IP | Ports/services | Network Recon |
| theHarvester | OSINT | Domain | Public information | OSINT |
| Amass | Domain discovery | Domain | Subdomains/assets | Subdomain Recon |
| dig | DNS queries | Domain/host | DNS records | DNS Recon |
| cURL | HTTP analysis | URL | HTTP metadata | HTTP Recon |
| WhatWeb | Technology detection | URL | Technology fingerprints | Technology Recon |

## 10. Why Multiple Tools Are Necessary

No single tool covers all required reconnaissance areas.

For example:

```text
Amass
  ↓
Subdomains

dig
  ↓
DNS records

Nmap
  ↓
Ports and services

cURL
  ↓
HTTP response information

WhatWeb
  ↓
Technology information

theHarvester
  ↓
Public information
```

RedHawk can combine these specialized outputs into one asset model.

## 11. Proposed Integration Architecture

```text
                    RedHawk Backend
                          |
       +------------------+------------------+
       |         |        |        |         |
     Nmap    Amass      dig      cURL    WhatWeb
       |         |        |        |         |
       +---------+--------+--------+---------+
                          |
                    Result Parsers
                          |
                     Normalization
                          |
                     Asset Database
```

## 12. Tool Integration Considerations

The backend should not assume that every command succeeds. Each module should handle:

- Invalid target
- Tool not installed
- Timeout
- Permission error
- Empty result
- Unexpected output
- Process failure

A module should return a structured result such as:

```text
status
target
tool
start_time
end_time
raw_output
parsed_results
error
```

This makes failures visible and easier to debug.

## 13. Conclusion

The evaluation indicates that RedHawk should act as an orchestration, normalization, visualization, and reporting layer around selected reconnaissance capabilities. Specialized tools can perform discovery while RedHawk provides a common workflow and centralized representation of the results.
