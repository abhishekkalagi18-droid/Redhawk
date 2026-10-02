# RedHawk Data Flow and Module Design

## Week 3 – System Design

## 1. Objective

This document defines how information should move through RedHawk from the moment a user submits an authorized target until the results appear in the dashboard or report.

## 2. End-to-End Data Flow

```text
User
 ↓
Frontend
 ↓
REST API
 ↓
Target Validation
 ↓
Scan Job
 ↓
Reconnaissance Engine
 ↓
Tool Execution
 ↓
Raw Output
 ↓
Parser
 ↓
Validation
 ↓
Normalization
 ↓
Correlation / Deduplication
 ↓
Database
 ↓
API
 ↓
Frontend Dashboard
 ↓
Report
```

## 3. Step 1 – Target Submission

The user enters an authorized target through the frontend.

Example:

```text
Target Type: Domain
Target: example.com
```

The frontend sends the request to the backend.

## 4. Step 2 – Validation

The backend validates:

- Target format
- Target type
- Authorization/scope
- Requested modules
- Scan configuration

Only valid requests should create a scan job.

## 5. Step 3 – Scan Job Creation

The backend creates a ScanJob record.

Example:

```text
Scan ID: 101
Target: example.com
Status: QUEUED
Modules: DNS, HTTP
```

## 6. Step 4 – Module Execution

The Scan Manager selects the requested modules.

Example:

```text
Scan Manager
    |
    +--- DNS Module
    |
    +--- HTTP Module
    |
    +--- Network Module
```

Modules should be isolated so that one failure does not necessarily terminate all other modules.

## 7. Step 5 – Tool Execution

A module may execute an external tool or use a native Python implementation.

For example:

```text
Network Module
      ↓
Nmap
      ↓
XML Output
```

## 8. Step 6 – Parsing

The parser extracts useful information.

Example:

```text
Raw XML
   ↓
Host
   ↓
Port
   ↓
Service
   ↓
Version
```

## 9. Step 7 – Validation

Extracted values should be checked before storage.

Examples:

- Valid IP address format
- Valid port range
- Valid domain/hostname format
- Valid status code
- Supported record type

## 10. Step 8 – Normalization

Different modules should return a consistent structure.

Example:

```json
{
  "asset_type": "ip",
  "asset_value": "203.0.113.10",
  "source": "nmap",
  "observed_at": "timestamp"
}
```

## 11. Step 9 – Correlation

RedHawk should connect related observations.

Example:

```text
api.example.com
      |
      +---- A record ----> 203.0.113.10
                              |
                              +---- 443/tcp
```

This correlation creates a more useful asset model.

## 12. Step 10 – Deduplication

If the same hostname is discovered by multiple modules, RedHawk should maintain one logical asset while recording multiple sources.

```text
Asset: api.example.com

Sources:
- Amass
- DNS
- OSINT
```

## 13. Step 11 – Storage

Normalized information is stored in the database.

The database becomes the source for dashboard and reporting operations.

## 14. Module Interface

Each reconnaissance module should follow a consistent conceptual interface:

```text
ReconModule
├── name
├── validate_target()
├── execute()
├── parse_output()
├── normalize()
└── handle_error()
```

This makes it easier to add modules later.

## 15. Example Module Lifecycle

```text
Initialize
   ↓
Validate
   ↓
Execute
   ↓
Collect Output
   ↓
Parse
   ↓
Normalize
   ↓
Return Result
```

## 16. Error Flow

If a module fails:

```text
Tool Failure
    ↓
Capture Error
    ↓
Update ToolResult
    ↓
Mark Module FAILED
    ↓
Continue Other Modules
    ↓
Update Overall Scan
```

The overall scan can report partial completion when appropriate.

## 17. Dashboard Data Flow

The dashboard should not read tool output directly.

Instead:

```text
Tool
 ↓
Parser
 ↓
Database
 ↓
API
 ↓
Dashboard
```

This separation ensures that frontend code does not depend on the output format of individual security tools.

## 18. Conclusion

The proposed data flow establishes a clear separation between target management, reconnaissance execution, processing, storage, and presentation. This design is important for making RedHawk maintainable and extensible as additional reconnaissance modules are introduced.
