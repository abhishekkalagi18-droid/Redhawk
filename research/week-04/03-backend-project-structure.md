# RedHawk Backend Project Structure

## 1. Purpose

The RedHawk backend is responsible for API operations, target validation, scan management, reconnaissance execution, result processing, database operations, and report generation.

FastAPI is selected as the planned backend framework.

## 2. Proposed Structure

```text
backend/
├── app/
│   ├── main.py
│   ├── api/
│   │   ├── targets.py
│   │   ├── scans.py
│   │   ├── assets.py
│   │   └── reports.py
│   ├── models/
│   ├── schemas/
│   ├── services/
│   │   ├── target_service.py
│   │   ├── scan_service.py
│   │   └── report_service.py
│   ├── recon/
│   │   ├── dns/
│   │   ├── subdomain/
│   │   ├── network/
│   │   ├── http/
│   │   └── technology/
│   ├── parsers/
│   ├── database/
│   ├── core/
│   └── utils/
├── tests/
├── requirements.txt
├── .env.example
└── README.md
```

## 3. Layer Responsibilities

### API Layer

Receives HTTP requests and returns HTTP responses.

It should not contain large amounts of reconnaissance logic.

### Service Layer

Contains application-level operations such as:

- Target management
- Scan creation
- Scan status updates
- Result processing
- Report generation

### Reconnaissance Layer

Contains independent modules for authorized reconnaissance activities.

Each module should have a clear input and output contract.

### Parser Layer

Converts raw tool output into structured application data.

Example:

```text
Raw Nmap XML
     ↓
Nmap Parser
     ↓
Host/Port/Service records
```

### Database Layer

Responsible for storing:

- Targets
- Scan jobs
- Assets
- Services
- DNS records
- HTTP observations
- Technologies
- Tool results

## 4. Configuration

Configuration should be separated from source code.

Potential environment variables:

```text
DATABASE_URL
API_HOST
API_PORT
SECRET_KEY
```

Sensitive values should not be committed to Git.

## 5. Error Handling

Backend errors should be handled consistently.

Examples:

- Invalid target → validation error
- Unknown target ID → not found
- Tool failure → scan/module failure status
- Parser failure → processing error
- Database failure → controlled server error

Raw stack traces should not be returned to normal users.

## 6. Recon Module Contract

A reconnaissance module should conceptually support:

```text
validate_target()
execute()
parse_output()
normalize()
handle_error()
```

This allows modules to be developed and tested independently.

## 7. Secure Command Execution

If external tools are invoked, the backend must:

- Validate targets.
- Avoid shell string concatenation.
- Prefer argument lists over shell commands.
- Restrict execution to authorized scope.
- Apply timeouts.
- Capture output safely.
- Record execution status.
- Prevent arbitrary command execution through API input.

## 8. Backend Goal

The backend architecture should provide a stable foundation for implementing reconnaissance modules from Week 5 onward.
