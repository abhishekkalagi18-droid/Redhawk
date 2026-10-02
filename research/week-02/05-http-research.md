# HTTP/HTTPS Reconnaissance Research

## Week 2 – RedHawk

## Objective
Understand how HTTP responses can provide useful information about externally accessible web services.

## HTTP Reconnaissance
HTTP reconnaissance examines how an authorized web server responds to requests.

Useful information includes:
- HTTP status code
- Content type
- Response headers
- Redirect location
- Response size
- Server information when exposed

## Common Status Codes

| Code | Meaning |
|---|---|
| 200 | Successful response |
| 301/302 | Redirect |
| 403 | Forbidden |
| 404 | Not found |
| 500 | Server-side error |

## cURL
cURL can be used to inspect HTTP responses in an authorized environment.

Example:
```bash
curl -I https://example.com
```

A response may contain:
```text
HTTP/1.1 200 OK
Content-Type: text/html
Server: ...
```

## RedHawk Processing
The backend can extract useful metadata from HTTP responses and store it in a normalized format.

Conceptual workflow:
```text
URL
 ↓
HTTP Request
 ↓
Response
 ↓
Extract Metadata
 ↓
Normalize
 ↓
Store
```

## Proposed Data Fields
- URL
- scheme
- status_code
- content_type
- server_header
- redirect_location
- response_size
- scan_time

## Limitations
Headers may be hidden or modified by the server, and an HTTP response alone does not establish that a vulnerability exists.

## RedHawk Relevance
HTTP reconnaissance can help RedHawk identify and characterize externally accessible web services.
