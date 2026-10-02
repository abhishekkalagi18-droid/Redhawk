# RedHawk Frontend–Backend Integration Plan

## 1. Purpose

The frontend and backend must communicate through a defined REST API. This integration plan establishes how user actions become backend requests and how reconnaissance results return to the dashboard.

## 2. Basic Communication Flow

```text
User
  ↓
Frontend UI
  ↓
API Service
  ↓
FastAPI Backend
  ↓
Validation
  ↓
Scan Manager
  ↓
Recon Module
  ↓
Parser/Normalizer
  ↓
Database
  ↓
FastAPI Response
  ↓
Frontend
  ↓
Dashboard
```

## 3. Target Creation Flow

```text
User enters target
        ↓
Frontend validation
        ↓
POST /api/targets
        ↓
Backend validation
        ↓
Target stored in database
        ↓
JSON response
        ↓
Target displayed in UI
```

The backend must remain the authoritative validation layer.

## 4. Scan Creation Flow

```text
User selects target
        ↓
Selects reconnaissance modules
        ↓
POST /api/scans
        ↓
Backend creates scan job
        ↓
Job enters queue/running state
        ↓
Recon modules execute
        ↓
Results parsed
        ↓
Results stored
        ↓
Scan marked completed/failed
```

## 5. Scan Status

The frontend should be able to retrieve scan status through an endpoint such as:

```text
GET /api/scans/{scan_id}
```

A scan record may contain:

```json
{
  "id": 1,
  "target_id": 10,
  "status": "running",
  "started_at": "...",
  "completed_at": null
}
```

The exact response model will be finalized during implementation.

## 6. Result Retrieval

Example logical endpoints:

```text
GET /api/assets
GET /api/assets/{id}
GET /api/scans/{id}
GET /api/reports
```

The frontend should request structured data rather than raw tool output whenever possible.

## 7. Error Handling

Expected errors include:

- Invalid target
- Missing required field
- Unauthorized request
- Target not found
- Scan not found
- Tool execution failure
- Timeout
- Parser failure
- Database failure

The API should return consistent JSON error responses.

## 8. CORS and Environment Configuration

During local development, the frontend and backend may run on different local ports.

The backend should configure CORS for the approved development origin rather than allowing unrestricted origins.

Production configuration should use the actual deployment domain.

## 9. Integration Testing

Before full integration, test:

1. Backend health endpoint.
2. Target creation.
3. Target retrieval.
4. Scan creation.
5. Scan status.
6. Result retrieval.
7. Error responses.
8. Frontend display of returned data.

## 10. Integration Goal

The goal is to create a predictable contract between frontend and backend so that UI development and reconnaissance development can proceed independently.
