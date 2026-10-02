# RedHawk Frontend Architecture

## 1. Purpose

The RedHawk frontend provides the user-facing interface for target management, scan control, reconnaissance results, assets, and reports.

The frontend should communicate with the FastAPI backend through REST APIs rather than directly executing reconnaissance tools.

## 2. Proposed Technology Stack

- HTML/CSS/JavaScript or React-based frontend according to the implementation decision.
- REST API communication
- Responsive CSS
- Browser-based dashboard
- JSON data exchange

For the planned implementation, a modular frontend structure is recommended so that individual pages and components can be developed independently.

## 3. Proposed Frontend Structure

```text
frontend/
├── public/
├── src/
│   ├── components/
│   │   ├── Navbar
│   │   ├── Sidebar
│   │   ├── StatCard
│   │   ├── DataTable
│   │   ├── StatusBadge
│   │   └── LoadingState
│   ├── pages/
│   │   ├── Dashboard
│   │   ├── Targets
│   │   ├── Scans
│   │   ├── Assets
│   │   ├── Findings
│   │   └── Reports
│   ├── services/
│   │   └── api
│   ├── styles/
│   └── main
├── package.json
└── README.md
```

The exact framework structure can be adjusted during implementation.

## 4. Component Strategy

Reusable components should be preferred over duplicating UI code.

Examples:

### StatCard

Displays a metric such as:

- Total targets
- Total assets
- Running scans
- Completed scans

### DataTable

Used for:

- Targets
- Scans
- Assets
- Services
- DNS records

### StatusBadge

Displays states such as:

- Running
- Completed
- Failed
- Pending

### LoadingState

Provides consistent loading feedback while API requests are being processed.

## 5. API Service Layer

Frontend API calls should be separated from page components.

Example logical functions:

```text
getTargets()
createTarget()
deleteTarget()

createScan()
getScans()
getScanById()

getAssets()
getAssetById()

getReports()
```

This separation makes the frontend easier to maintain and test.

## 6. Frontend Routing

Recommended routes:

```text
/
 /dashboard
 /targets
 /targets/:id
 /scans
 /scans/:id
 /assets
 /assets/:id
 /findings
 /reports
 /settings
```

Route names may be adjusted during implementation.

## 7. Data Handling

The frontend should:

1. Send validated user input to the API.
2. Receive JSON responses.
3. Display loading state.
4. Handle successful responses.
5. Handle API errors.
6. Refresh relevant data when a scan completes.

## 8. Frontend Security Considerations

- Never place secret API keys in client-side source code.
- Do not trust client-side validation alone.
- Do not expose raw command execution interfaces.
- Sanitize displayed data where required.
- Use secure authentication mechanisms when implemented.
- Avoid storing sensitive information unnecessarily in browser storage.

## 9. Frontend Development Goal

The frontend architecture should allow developers to add new reconnaissance modules without redesigning the entire interface.
