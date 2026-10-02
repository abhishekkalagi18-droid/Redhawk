# RedHawk Database Design


## 1. Database Objective

RedHawk will generate information from multiple reconnaissance modules. A structured database is required to preserve targets, scan jobs, discovered assets, services, DNS records, HTTP observations, and tool execution results.

The database should support both historical tracking and relationships between discovered assets.

## 2. Main Entities

The initial database model contains:

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

## 3. Users

The Users entity stores authentication-related information.

Possible fields:

```text
id
username
email
password_hash
created_at
```

Passwords should never be stored as plaintext.

## 4. Targets

A target represents an authorized domain, hostname, or IP address.

Possible fields:

```text
id
name
target_type
target_value
description
created_at
updated_at
```

Example:

```text
target_type: domain
target_value: example.com
```

## 5. ScanJobs

A scan job represents one reconnaissance execution.

Possible fields:

```text
id
target_id
status
created_at
started_at
completed_at
requested_modules
error_message
```

Possible status values:

```text
QUEUED
RUNNING
COMPLETED
FAILED
CANCELLED
```

## 6. Assets

Assets represent discovered external resources.

Possible fields:

```text
id
target_id
asset_type
asset_value
source
first_seen
last_seen
```

Examples:

```text
domain
subdomain
hostname
ip
url
```

## 7. Services

Services represent network services associated with an asset.

Possible fields:

```text
id
asset_id
port
protocol
state
service_name
service_version
source
observed_at
```

Example:

```text
asset: 203.0.113.10
port: 443
protocol: tcp
service: https
```

## 8. DNSRecords

DNS records store observations from DNS reconnaissance.

Possible fields:

```text
id
asset_id
record_type
record_name
record_value
ttl
source
observed_at
```

## 9. HTTPObservations

HTTP observations represent information collected from web endpoints.

Possible fields:

```text
id
asset_id
url
status_code
content_type
server
redirect_location
response_size
observed_at
```

## 10. Technologies

Technology records represent detected technologies.

Possible fields:

```text
id
asset_id
technology_name
category
version
source
confidence
observed_at
```

The `confidence` field can help distinguish strong observations from uncertain fingerprints.

## 11. ToolResults

ToolResults preserve information about individual tool executions.

Possible fields:

```text
id
scan_job_id
tool_name
module_name
status
started_at
completed_at
raw_output
error_message
```

Raw output can be useful for debugging and validation, but access should be controlled because it may contain sensitive assessment information.

## 12. Entity Relationships

Conceptually:

```text
User
 |
 +---- Targets
          |
          +---- ScanJobs
          |       |
          |       +---- ToolResults
          |
          +---- Assets
                  |
                  +---- Services
                  |
                  +---- DNSRecords
                  |
                  +---- HTTPObservations
                  |
                  +---- Technologies
```

## 13. Asset Correlation

The asset model should allow relationships between observations.

Example:

```text
api.example.com
      |
      +---- DNS A ----> 203.0.113.10
                           |
                           +---- 443/tcp
                                  |
                                  +---- HTTPS
```

This allows the dashboard to present a connected view rather than unrelated rows.

## 14. Deduplication

The same asset can be discovered through multiple sources.

Example:

```text
Source A → api.example.com
Source B → api.example.com
```

RedHawk should avoid creating unnecessary duplicate asset records.

A possible logical identity is:

```text
asset_type + normalized_asset_value
```

The system should still preserve multiple discovery sources.

## 15. Historical Tracking

Assets can change over time. RedHawk should preserve:

- First observed time
- Last observed time
- Discovery source
- Scan job

This supports future comparison between reconnaissance runs.

## 16. Database Design Principles

The database should prioritize:

- Data consistency
- Referential integrity
- Clear relationships
- Useful indexes
- Controlled access
- Historical traceability
- Extensibility

## 17. Conclusion

The proposed database model separates targets, scan jobs, assets, services, and reconnaissance observations while maintaining relationships between them. This structure will support the dashboard, reporting system, historical tracking, and future analysis features.
