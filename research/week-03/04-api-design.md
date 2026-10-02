# RedHawk REST API Design

## Week 3 – System Design

## 1. API Objective

The RedHawk frontend needs a reliable interface for communicating with the backend. A REST API will provide operations for target management, scan execution, asset retrieval, and reporting.

FastAPI will be used as the backend framework.

## 2. API Architecture

```text
React / Web Frontend
        |
        | HTTP Requests
        v
FastAPI REST API
        |
        +---- Target Service
        |
        +---- Scan Service
        |
        +---- Asset Service
        |
        +---- Report Service
        |
        v
Database / Recon Engine
```

## 3. Target Endpoints

### Create Target

```http
POST /api/targets
```

Purpose: Add an authorized target.

Example request:

```json
{
  "target_type": "domain",
  "target_value": "example.com"
}
```

### List Targets

```http
GET /api/targets
```

Purpose: Retrieve saved targets.

### Get Target

```http
GET /api/targets/{target_id}
```

Purpose: Retrieve information about one target.

### Delete Target

```http
DELETE /api/targets/{target_id}
```

Purpose: Remove a target from the project.

## 4. Scan Endpoints

### Create Scan

```http
POST /api/scans
```

Example conceptual request:

```json
{
  "target_id": 1,
  "modules": [
    "dns",
    "network",
    "http"
  ]
}
```

### Get Scan Status

```http
GET /api/scans/{scan_id}
```

Possible response state:

```json
{
  "id": 10,
  "status": "RUNNING"
}
```

### List Scans

```http
GET /api/scans
```

Purpose: Display previous and current reconnaissance jobs.

## 5. Asset Endpoints

### List Assets

```http
GET /api/assets
```

Optional filtering can later support:

```text
asset_type
target_id
source
```

### Get Asset

```http
GET /api/assets/{asset_id}
```

This endpoint can return the asset and related observations.

## 6. DNS Endpoints

A dedicated endpoint may later expose DNS observations:

```http
GET /api/assets/{asset_id}/dns
```

## 7. HTTP Observation Endpoints

HTTP observations can be retrieved through:

```http
GET /api/assets/{asset_id}/http
```

## 8. Report Endpoints

### Generate Report

```http
POST /api/reports
```

### Get Report

```http
GET /api/reports/{report_id}
```

The exact report format will be finalized during implementation.

## 9. API Response Structure

Responses should use predictable structures.

Example:

```json
{
  "success": true,
  "data": {},
  "error": null
}
```

For errors:

```json
{
  "success": false,
  "data": null,
  "error": {
    "code": "INVALID_TARGET",
    "message": "Target validation failed"
  }
}
```

## 10. HTTP Status Codes

The API should use meaningful HTTP status codes.

| Code | Purpose |
|---|---|
| 200 | Successful request |
| 201 | Resource created |
| 400 | Invalid request |
| 401 | Authentication required |
| 403 | Access denied |
| 404 | Resource not found |
| 409 | Conflict |
| 500 | Internal server error |

## 11. Target Validation

Target validation is a critical security requirement.

Before a reconnaissance job begins, the backend should verify that:

- The target value has an accepted format.
- The requested module is supported.
- The target belongs to the authorized project scope.
- Command arguments cannot be manipulated through untrusted input.

## 12. Scan Execution Model

Long-running scans should not block the API request indefinitely.

Conceptual flow:

```text
POST /api/scans
       ↓
Create ScanJob
       ↓
Return scan ID
       ↓
Background Worker
       ↓
Execute Recon Module
       ↓
Store Results
       ↓
Update Scan Status
```

## 13. API Security

The API should eventually include:

- Authentication
- Authorization
- Input validation
- Rate limiting where appropriate
- Secure error handling
- Audit logging
- Safe command execution

Sensitive internal errors should not be exposed directly to users.

## 14. Conclusion

The API design establishes a clean interface between the frontend, backend, reconnaissance engine, and database. The endpoints can evolve during implementation, but this design provides the initial contract needed to begin development.
