# Nmap Research


## 1. Introduction

Nmap, short for Network Mapper, is a widely used network discovery and security auditing tool. It is particularly relevant to RedHawk because exposed network ports and services are important components of an external attack surface.

RedHawk does not need to reproduce Nmap's scanning engine. Instead, it can use Nmap as a reconnaissance component and process its results.

## 2. Purpose of Nmap

Nmap can help security teams determine:

- Which hosts respond within an authorized scope
- Which network ports are accessible
- What services appear to be running
- Which service versions may be detectable
- Additional host information depending on scan configuration

The information is useful for creating an inventory of externally exposed services.

## 3. Ports and Services

Network applications commonly communicate through ports.

Example:

```text
22/tcp  → SSH
80/tcp  → HTTP
443/tcp → HTTPS
```

An open port represents an observable network endpoint. It does not automatically indicate a vulnerability.

For example:

```text
443/tcp open
```

means an HTTPS service appears accessible. Further assessment is required to determine whether the service has a security issue.

## 4. Basic Authorized Lab Scan

Against a system you own or have explicit permission to test:

```bash
nmap <authorized-lab-ip>
```

This can provide basic port and service discovery.

Service detection can be performed in a controlled lab:

```bash
nmap -sV <authorized-lab-ip>
```

The `-sV` option requests service/version detection.

## 5. Example Output

A simplified result may look like:

```text
PORT    STATE  SERVICE
22/tcp  open   ssh
80/tcp  open   http
443/tcp open   https
```

With service detection, additional information may appear:

```text
22/tcp  open  ssh    OpenSSH ...
80/tcp  open  http   Apache ...
```

The exact result depends on the target and network environment.

## 6. Structured Output

Terminal output is convenient for humans but less convenient for automated systems.

Nmap can produce structured XML output, which is useful for a backend application.

Conceptual workflow:

```text
Nmap Process
     ↓
XML Output
     ↓
Python Parser
     ↓
Validation
     ↓
Normalized Records
     ↓
Database
```

Structured output makes it easier for RedHawk to extract fields such as:

- Host address
- Port
- Protocol
- State
- Service
- Version

## 7. Proposed RedHawk Nmap Data Model

A service record can conceptually contain:

```text
ServiceRecord
├── target
├── host
├── port
├── protocol
├── state
├── service
├── version
├── source
└── scan_time
```

The `source` field is useful because an analyst should be able to determine where an observation originated.

## 8. Nmap Module Workflow

```text
User Selects Target
        ↓
Validate Target
        ↓
Create Scan Job
        ↓
Execute Nmap
        ↓
Monitor Process
        ↓
Collect Output
        ↓
Parse Results
        ↓
Validate Data
        ↓
Normalize Records
        ↓
Store Results
        ↓
Display in Dashboard
```

## 9. Error Handling

The RedHawk backend should handle common failures.

Examples include:

### Nmap Not Installed
The backend should return a clear dependency error.

### Invalid Target
The application should validate the input before starting a scan.

### Timeout
A scan should not block the entire application indefinitely.

### Empty Results
Empty results should be represented as an observation or scan result, not automatically interpreted as "no assets exist."

### Process Failure
The backend should record the failure and make the error visible to the user.

## 10. Security Considerations

Nmap functionality should be restricted to authorized security testing.

RedHawk should consider:

- Target validation
- Authentication and authorization
- Scan logging
- Rate and resource controls
- Clear scan status
- Safe handling of command arguments

Command construction should avoid unsafe string concatenation. Backend code should use secure process-execution mechanisms and validated arguments.

## 11. Limitations

Nmap results are influenced by:

- Firewalls
- Network filtering
- Routing
- Service configuration
- Scan options
- Network reliability

Therefore, the absence of a result does not always prove that an asset or service does not exist.

## 12. RedHawk Integration

Nmap can become the Network Recon module:

```text
             RedHawk
                 |
          Network Recon
                 |
               Nmap
                 |
          Structured Output
                 |
              Parser
                 |
          Service Records
                 |
             Database
```

## 13. Conclusion

Nmap is a strong candidate for RedHawk's network and service discovery functionality. The important architectural requirement is to treat Nmap as a controlled backend module whose structured results are parsed, validated, normalized, stored, and presented through RedHawk rather than simply displaying raw terminal output.
