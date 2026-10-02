# RedHawk System Requirements


## 1. Introduction

Week 1 established the project problem and objectives, while Week 2 studied reconnaissance techniques and candidate tools. Week 3 converts those findings into a concrete system design.

The purpose of this document is to define what RedHawk must provide from both a functional and technical perspective before implementation begins.

## 2. Functional Requirements

### FR-01: User Access

The system should provide controlled access to the RedHawk interface. Authentication can be introduced so that reconnaissance operations are not exposed to unauthorized users.

### FR-02: Target Management

An authorized user should be able to:

- Add a target within an approved scope.
- View previously added targets.
- Select a target for reconnaissance.
- Update target metadata.
- Remove a target when it is no longer required.

Target information should be validated before scanning.

### FR-03: Reconnaissance Job Creation

The user should be able to create a reconnaissance job for a selected target.

A job should contain information such as:

- Target
- Selected modules
- Requested scan type
- Creation time
- Current status
- Completion time

### FR-04: Reconnaissance Modules

The system should support modular reconnaissance capabilities, including:

- DNS reconnaissance
- Subdomain discovery
- Network/service discovery
- HTTP reconnaissance
- Technology identification
- OSINT collection where supported

Modules should be independently maintainable.

### FR-05: Scan Execution

The backend should execute authorized reconnaissance tasks and monitor their progress.

The application should distinguish states such as:

```text
QUEUED
RUNNING
COMPLETED
FAILED
CANCELLED
```

### FR-06: Result Processing

Raw tool output should be collected and processed.

The processing layer should:

1. Receive tool output.
2. Parse the output.
3. Validate extracted values.
4. Normalize the data.
5. Associate results with assets.
6. Store the result.

### FR-07: Asset Inventory

RedHawk should maintain a centralized inventory containing assets such as:

- Domains
- Subdomains
- Hostnames
- IP addresses
- Ports
- Services
- Web endpoints
- Technologies
- DNS records

### FR-08: Dashboard

The dashboard should provide an overview of reconnaissance results.

Possible dashboard information includes:

- Number of discovered assets
- Number of hosts
- Number of open ports
- Services detected
- Web assets
- Recent reconnaissance jobs
- Scan status

### FR-09: Asset Details

Users should be able to inspect an individual asset and view related information.

For example:

```text
api.example.com
├── IP: 203.0.113.10
├── Port: 443
├── Service: HTTPS
├── Technology: Web Server
└── HTTP observations
```

### FR-10: Reporting

The system should organize reconnaissance observations into a readable report.

The report should include:

- Target
- Scan date/time
- Modules used
- Discovered assets
- Services
- HTTP information
- Technology observations
- Errors or incomplete results

## 3. Non-Functional Requirements

### NFR-01: Security

The system should validate user input, protect authentication information, and restrict reconnaissance operations to authorized targets.

### NFR-02: Reliability

A failure in one reconnaissance module should not unnecessarily terminate unrelated modules.

### NFR-03: Maintainability

The system should use modular components so individual reconnaissance modules can be updated independently.

### NFR-04: Scalability

The architecture should allow additional tools and reconnaissance modules to be added later.

### NFR-05: Performance

The backend should avoid blocking the main application while long-running reconnaissance jobs execute.

### NFR-06: Usability

The interface should clearly communicate:

- What target is selected
- What scan is running
- Which modules are active
- Whether a scan succeeded or failed
- What results were discovered

### NFR-07: Observability

The system should maintain logs for important operations, including job creation, execution, completion, and failure.

## 4. Input Requirements

RedHawk may accept:

```text
Target domain
Hostname
IP address
Reconnaissance module selection
Scan configuration
```

Inputs must be validated before execution.

## 5. Output Requirements

The system should produce structured results rather than only terminal text.

Example:

```text
Asset
 ├── type: hostname
 ├── value: api.example.com
 ├── source: DNS
 └── discovered_at: timestamp
```

## 6. Scope Boundary

RedHawk is primarily an external reconnaissance and attack-surface discovery platform.

It should not automatically perform destructive actions or exploitation as part of the core reconnaissance workflow.

## 7. Conclusion

These requirements provide the functional and technical baseline for RedHawk. They will guide the architecture, API, database, frontend, and reconnaissance-engine design developed during Week 3.
