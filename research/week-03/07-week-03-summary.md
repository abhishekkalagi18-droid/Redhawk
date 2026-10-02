# Week 3 Progress Summary


## 1. Week Objective

The objective of Week 3 was to transform the research from Weeks 1 and 2 into a technical system design for RedHawk.

The work focused on defining system requirements, application architecture, database entities, REST APIs, reconnaissance-module interfaces, data flow, and security requirements.

## 2. System Requirements

The functional requirements identified include:

- User access
- Target management
- Reconnaissance job creation
- Modular reconnaissance execution
- Result processing
- Centralized asset inventory
- Dashboard visualization
- Asset details
- Report generation

The non-functional requirements include:

- Security
- Reliability
- Maintainability
- Scalability
- Performance
- Usability
- Observability

## 3. Architecture Designed

The proposed architecture separates RedHawk into the following layers:

```text
Frontend
   ↓
FastAPI Backend
   ↓
Scan Manager
   ↓
Reconnaissance Modules
   ↓
Result Processing
   ↓
Database
   ↓
API
   ↓
Dashboard / Reports
```

This separation allows each layer to evolve independently.

## 4. Reconnaissance Modules

The planned module structure is:

```text
ReconEngine
├── DNSRecon
├── SubdomainRecon
├── NetworkRecon
├── HTTPRecon
├── TechnologyRecon
└── OSINTRecon
```

Each module should have a consistent lifecycle:

```text
Validate
   ↓
Execute
   ↓
Parse
   ↓
Normalize
   ↓
Return Result
```

## 5. Database Design

The initial database entities are:

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

The database is designed to preserve both current observations and historical scan information.

## 6. API Design

The initial REST API groups endpoints around:

### Targets

```text
POST   /api/targets
GET    /api/targets
GET    /api/targets/{id}
DELETE /api/targets/{id}
```

### Scans

```text
POST /api/scans
GET  /api/scans
GET  /api/scans/{id}
```

### Assets

```text
GET /api/assets
GET /api/assets/{id}
```

Additional DNS, HTTP, and reporting endpoints can be introduced during implementation.

## 7. Data Flow

The planned end-to-end flow is:

```text
Target
 ↓
Validation
 ↓
Scan Job
 ↓
Recon Module
 ↓
Tool
 ↓
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
 ↓
API
 ↓
Dashboard
```

## 8. Security Requirements

The system design identified several important security controls:

- Target validation
- Authentication
- Authorization
- Secure command execution
- Input validation
- Scan timeouts
- Resource controls
- Audit logging
- Secure result storage
- Safe error handling

## 9. Key Design Decisions

### Modular Reconnaissance

Reconnaissance functionality should be implemented as independent modules.

### Centralized Data Model

Different tool outputs should be normalized into a common asset model.

### Structured Tool Output

Where available, machine-readable output should be preferred over parsing human-oriented terminal output.

### Background Scan Execution

Long-running scans should not block the API request.

### Source Tracking

Important observations should preserve their source and timestamp.

## 10. Week 3 Outcome

At the end of Week 3, RedHawk has a defined technical blueprint that can guide implementation.

The design now provides:

- Functional requirements
- Non-functional requirements
- System architecture
- Module architecture
- Database model
- API structure
- Data flow
- Security requirements

## 11. Transition to Week 4

Week 4 will focus on preparing the project for implementation.

Planned work:

1. Frontend/UI design
2. Dashboard layout
3. Target management interface
4. Scan interface
5. Results and asset pages
6. Backend project structure
7. Frontend project structure
8. API-to-frontend integration plan
9. Git/GitHub project organization
10. Development roadmap for Weeks 5–16

## 12. Conclusion

Week 3 converts the research phase into a structured technical design. The resulting architecture is modular and allows RedHawk to integrate multiple reconnaissance capabilities while maintaining a centralized asset inventory and reporting workflow.

All active reconnaissance functionality is intended for authorized systems and controlled laboratory environments.
