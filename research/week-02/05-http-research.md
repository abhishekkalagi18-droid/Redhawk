# HTTP/HTTPS Reconnaissance Research

## RedHawk – Automated Attack Surface & External Reconnaissance Suite

## 1. Introduction

Web applications are a major part of an organization's external attack surface. HTTP and HTTPS reconnaissance can reveal how a web service responds to requests and can provide metadata about the application or server.

The purpose of HTTP reconnaissance is not exploitation. The focus is on collecting and organizing observable response information from authorized targets.

## 2. HTTP Request and Response

A basic HTTP interaction consists of:

```text
Client
  ↓
HTTP Request
  ↓
Web Server
  ↓
HTTP Response
```

The response can contain:

- Status code
- Headers
- Content type
- Response body
- Redirect information

RedHawk can extract useful metadata from the response.

## 3. HTTP Status Codes

Status codes provide a high-level description of the result of a request.

| Code | Category | Meaning |
|---|---|---|
| 200 | 2xx | Successful request |
| 301 | 3xx | Permanent redirect |
| 302 | 3xx | Temporary redirect |
| 400 | 4xx | Bad request |
| 401 | 4xx | Authentication required |
| 403 | 4xx | Forbidden |
| 404 | 4xx | Resource not found |
| 500 | 5xx | Server-side error |

Status codes should be interpreted in context. A 403 response, for example, does not automatically indicate a security vulnerability.

## 4. HTTP Headers

Headers provide metadata about the request and response.

Examples include:

```text
Content-Type
Location
Server
Set-Cookie
Cache-Control
```

Some servers expose technology-related information through headers, although modern systems may deliberately minimize such disclosure.

## 5. cURL for HTTP Reconnaissance

cURL is useful for making HTTP requests from a command line.

For example:

```bash
curl -I https://example.com
```

The `-I` option requests response headers without retrieving the complete response body.

For authorized lab environments, cURL can be used to examine:

- Response status
- Headers
- Redirect behavior
- Content type

## 6. HTTPS

HTTPS is HTTP transported over TLS.

From a reconnaissance perspective, the analyst may observe the HTTPS service and response behavior without attempting to bypass encryption.

HTTPS reconnaissance can include:

- URL
- Response status
- Headers
- Certificate-related information when appropriate
- Redirect behavior

## 7. Proposed HTTP Data Model

```text
HTTPObservation
├── URL
├── scheme
├── status_code
├── content_type
├── server
├── redirect_location
├── response_size
├── source
└── observed_at
```

This structure allows HTTP information to be connected to a particular web asset.

## 8. RedHawk HTTP Workflow

```text
Web Asset
    ↓
Scope Validation
    ↓
HTTP Request
    ↓
Receive Response
    ↓
Extract Metadata
    ↓
Validate / Normalize
    ↓
Store Observation
    ↓
Display in Dashboard
```

## 9. Technology Identification

HTTP responses can sometimes provide indicators about technologies.

For example:

```text
Web Server
Application Framework
CMS
JavaScript Library
```

Tools such as WhatWeb can provide additional technology fingerprinting.

However, fingerprints are not always accurate. RedHawk should label them as detected observations and preserve the source.

## 10. Error Handling

The HTTP module should handle:

- Connection timeout
- DNS resolution failure
- TLS errors
- Connection refusal
- Redirect loops
- Invalid URL
- Unexpected server response

A failure should be recorded clearly rather than causing the complete reconnaissance job to fail.

## 11. Limitations

HTTP reconnaissance has limitations:

- Some services require authentication.
- Servers may hide technology information.
- Responses can change depending on headers or location.
- Web applications may generate dynamic responses.
- A status code alone does not identify a vulnerability.

Therefore, HTTP reconnaissance should be considered a source of application metadata rather than a vulnerability scanner.

## 12. RedHawk Relevance

HTTP reconnaissance allows RedHawk to extend beyond network-level discovery.

For example:

```text
api.example.com
      |
      +---- 443/tcp
              |
             HTTPS
              |
        HTTP Observation
              |
      Status / Headers / Type
```

This produces a richer profile of externally accessible web assets.

## 13. Conclusion

HTTP/HTTPS reconnaissance provides valuable application-level context. By collecting response metadata and connecting it to discovered domains, ports, and technologies, RedHawk can present a more complete view of externally visible web services.
