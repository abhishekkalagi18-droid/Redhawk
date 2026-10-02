# RedHawk System Architecture

## 1. Architecture Objective

RedHawk requires an architecture that separates the user interface, backend services, reconnaissance execution, result processing, and data storage.

The architecture should make it possible to add new reconnaissance modules without rewriting the entire application.

## 2. High-Level Architecture

```text
+------------------------------------------------------+
|                    RedHawk Frontend                  |
|        Dashboard | Targets | Scans | Reports        |
+---------------------------+--------------------------+
                            |
                            | HTTP/REST API
                            v
+------------------------------------------------------+
|                    FastAPI Backend                   |
| Authentication | Target Management | Scan Manager  |
+---------------------------+--------------------------+
                            |
                            v
+------------------------------------------------------+
|               Reconnaissance Engine                 |
|                                                      |
| DNS | Subdomain | Network | HTTP | Technology | OSINT|
+---------------------------+--------------------------+
                            |
                            v
+------------------------------------------------------+
|              Result Processing Layer                 |
| Parser | Validator | Normalizer | Correlator        |
+---------------------------+--------------------------+
                            |
                            v
+------------------------------------------------------+
|                    Database                          |
| Targets | Jobs | Assets | Services | Observations   |
+------------------------------------------------------+
```

## 3. Frontend Layer

The frontend is responsible for user interaction.

Major screens can include:

### Dashboard
Provides an overview of the current attack-surface inventory and recent scan jobs.

### Targets
Allows users to add and manage authorized targets.

### Scan Interface
Allows users to select a target and reconnaissance modules.

### Assets
Displays discovered domains, hosts, IP addresses, services, and technologies.

### Findings/Observations
Displays important observations generated during reconnaissance.

### Reports
Provides access to structured reconnaissance reports.

## 4. Backend Layer

The backend acts as the central control layer.

Responsibilities include:

- Authentication
- Input validation
- Target management
- Scan job creation
- Reconnaissance orchestration
- Result processing
- Database interaction
- Reporting

FastAPI is suitable because it provides a lightweight Python REST API framework and works well with asynchronous application patterns.

## 5. Reconnaissance Engine

The reconnaissance engine is responsible for executing individual modules.

A conceptual module structure is:

```text
ReconEngine
├── DNSRecon
├── SubdomainRecon
├── NetworkRecon
├── HTTPRecon
├── TechnologyRecon
└── OSINTRecon
```

Each module should have a consistent interface.

Example conceptual interface:

```text
Module
├── validate()
├── execute()
├── parse()
└── normalize()
```

## 6. Result Processing Layer

The result processor separates raw tool output from the application's internal data model.

```text
Raw Output
    ↓
Parser
    ↓
Validation
    ↓
Normalization
    ↓
Correlation
    ↓
Database
```

This prevents frontend components from depending directly on individual tool output formats.

## 7. Database Layer

The database stores persistent project information.

Potential entities include:

```text
Users
Targets
ScanJobs
Assets
Services
DNSRecords
HTTPObservations
Technologies
ToolResults
```

Relationships will be defined in the database design.

## 8. Reporting Layer

The reporting component collects stored observations and converts them into a readable report.

The report should identify:

- Target
- Scan time
- Modules executed
- Assets discovered
- Services identified
- HTTP observations
- Technologies detected
- Errors

## 9. Why Modular Architecture?

Reconnaissance tools change over time. A modular architecture means RedHawk can replace or upgrade one module without redesigning the entire system.

For example:

```text
NetworkRecon
     |
   Nmap
```

could later be changed internally without changing the dashboard's asset model.

## 10. Error Isolation

Suppose DNS reconnaissance succeeds but HTTP reconnaissance fails:

```text
DNS        → COMPLETED
Nmap       → COMPLETED
HTTP       → FAILED
WhatWeb    → COMPLETED
```

The scan should still retain the successful results while clearly reporting the failed module.

## 11. Conclusion

The proposed architecture separates presentation, API control, reconnaissance execution, result processing, and persistence. This separation improves maintainability and provides a foundation for integrating the reconnaissance capabilities identified during Week 2.
