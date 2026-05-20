# Software Obsolescence Management Workflow v1.5.0

A Dynatrace Automation workflow that proactively tracks end-of-life (EOL) dates for operating systems, runtime technologies, and third-party libraries detected in your environment — and raises Davis custom events when software approaches or passes its obsolescence date.

## Architecture

The workflow uses a **config → parallel workers → alerting** pattern with five tasks:

```
                    ┌─────────────────────┐
                    │       config        │
                    │  (user settings)    │
                    └────┬───────┬───────┬┘
                         │       │       │
              ┌──────────▼┐  ┌───▼──────┐ ┌▼──────────────┐
              │get_os_eol  │  │get_tech  │ │get_library_eos│
              │  _data     │  │_eos_data │ │  _data        │
              └──────┬─────┘  └──────────┘ └───────────────┘
                     │
              ┌──────▼─────┐
              │alert_os_eos│
              └────────────┘
```

The three data-refresh tasks run **in parallel** after `config` completes. Each worker:
1. Fetches its config from the `config` task result via the Automation API
2. Refreshes EOL data for its domain (OS / technology / library)

The **alert_os_eos** task runs **after `get_os_eol_data` completes**, ensuring OS lifecycle data is up to date before alerting.

### Task Descriptions

| Task | Purpose |
|---|---|
| **config** | Centralised user configuration. Returns alert thresholds, management zone/tag restrictions, and support overrides as a JSON object. |
| **get_os_eol_data** | Refreshes OS version lifecycle data from [endoflife.date](https://endoflife.date). |
| **get_technology_eos_data** | Refreshes runtime/framework lifecycle data (Java, Spring Boot, .NET, etc.) from endoflife.date. |
| **get_library_eos_data** | Refreshes third-party library version data from [deps.dev](https://deps.dev). |
| **alert_os_eos** | Raises proactive Davis events for hosts running OS versions approaching or past their end-of-life date. Runs after OS data is refreshed. |

## Configuration

All user configuration is in the **config** task. Edit the following constants:

### Alert Thresholds

```js
const alertThresholds = {
  '0': 'CUSTOM_INFO',   // Already obsolete → raise CUSTOM_INFO event
  '30': 'CUSTOM_INFO'   // Within 30 days → raise CUSTOM_INFO event
}
```

- Set a threshold to `'CUSTOM_INFO'` or `'CUSTOM_ALERT'` to enable it.
- Set to `false` to disable that threshold.

### Management Zone Restrictions

```js
const alertManagementZoneRestrictions = [
  // '[MyApp] Infra layer',
  // 'Special MZ 208569',
]
```

Restricts alerting to hosts belonging to at least one of the listed management zones. Empty array = no restriction.

### Tag Restrictions

```js
const alertTagRestrictions = [
  // 'stage:prod',
  // 'kubernetes',
]
```

Restricts alerting to hosts with at least one matching tag. Empty array = no restriction.

> **Note:** When both management zone and tag restrictions are configured, they are combined with AND logic — a host must match both to be included.

### Support Overrides

```js
const supportOverrides = {
  // 'Ubuntu 18.04.6 LTS (Bionic Beaver) (kernel 5.4.0-1089-azure)': '2026-10-30',
  // 'Amazon Linux 2 (kernel 5.10.197-186.748.amzn2.x86_64)': '2025-04-03'
};
```

Override the EOL date for specific OS versions (e.g. when you have an extended support contract). Use the full OS name as it appears in Dynatrace as the key, and the extended support date (`YYYY-MM-DD`) as the value.

## How It Works

### Data Refresh (OS)

1. Fetches the full product catalogue from the [endoflife.date API](https://endoflife.date/api/all.json) and augments it with product display names scraped from the endoflife.date homepage.
2. Queries Dynatrace via DQL for up to **60 OS versions** that don't already have a recent `software-obsolescence-management.os-info` event (< 7 days old), randomised.
3. For each OS version, uses **fuzzy scoring** to match it to an endoflife.date product, then fetches the lifecycle data (EOL date, latest version, LTS status, cycle info).
4. Ingests the result as a `software-obsolescence-management.os-info` custom event with properties:

| Property | Description |
|---|---|
| `os` | Extracted OS name |
| `currentVersion` | Detected version number |
| `key` | Full OS version string from Dynatrace |
| `latestVersion` | Latest version across all cycles |
| `latestVersionPublishedAt` | Publish date of the latest version |
| `latestVersionInCycle` | Latest version within the matched cycle |
| `link` | Link to release notes |
| `currentCycle` | Matched release cycle |
| `currentCyclePublishedAt` | Release date of the matched cycle |
| `lts` | Whether the cycle is LTS |
| `eol` | End-of-life date for the matched cycle |

### Data Refresh (Technologies)

Same pattern as OS, but queries `dt.entity.process_group_instance` for software technologies (Java, Spring Boot, etc.). Uses `technologyToProductSlugMap` for manual mappings plus fuzzy scoring. Ingests results as `software-obsolescence-management.technology-info` events.

### Data Refresh (Libraries)

Queries `dt.entity.software_component` for detected libraries. Maps Dynatrace technology types to package managers:

| Dynatrace Type | Package Manager |
|---|---|
| `DOTNET` | NuGet |
| `NODE_JS` | npm |
| `JAVA` | Maven |
| `GO` | Go |

Calls the [deps.dev API](https://deps.dev) to retrieve latest stable version, publish dates, licenses, and origin links. Ingests results as `software-obsolescence-management.library-info` events.

### Proactive Alerting

1. Queries Dynatrace for all hosts with known OS versions, joining against previously-ingested `os-info` events to compute time before obsolescence.
2. Applies **support overrides** by injecting them into the DQL query.
3. Filters to hosts where obsolescence is within 90 days or up to 7 days past.
4. Buckets hosts into two threshold groups: `0` (already obsolete) and `30` (within 30 days).
5. Applies management zone and tag restrictions.
6. Deduplicates — skips hosts that already had an alert at the same or lower threshold in the last 30 days.
7. Ingests Davis custom events (`CUSTOM_INFO` or `CUSTOM_ALERT`) attached to the host entity.

### Fuzzy Matching

Both `getFreshOsData()` and `getFreshTechnologyData()` use a scoring algorithm to match detected software to endoflife.date products:

- **+10 points** for an exact manual map match or exact slug/name match
- **+1 point** for each matching word segment in slug or product name
- **Bonus** for unique matches (fewer than 3 products share the segment)
- Candidates scoring > 2 are sorted by score; the top match is used

### API Compatibility

The endoflife.date data fetching supports both the legacy API schema (flat cycle arrays) and the newer v2 schema (nested `result.releases[]` with object-typed `latest`, `isLts`, `eolFrom`, etc.). Field access uses fallback patterns for backward compatibility.

## Dependencies

- `dynatrace.automations` app (^1.2879.0)
- `@dynatrace-sdk/client-classic-environment-v2` — for ingesting Davis custom events
- `@dynatrace-sdk/client-query` — for executing DQL queries
- `@dynatrace-sdk/automation-utils` — for workflow execution context

### External APIs

| API | Used By | Purpose |
|---|---|---|
| endoflife.date | OS & Technology refresh | Product lifecycle data |
| deps.dev | Library refresh | Package version & licence data |

## Known Considerations

- The `raiseProactiveAlerts` function currently only analyses **OS obsolescence**. Technology and library alerting is not yet implemented — those data-refresh tasks only ingest info events for dashboard use.
- Alerting depends on the OS data being refreshed first (enforced by the `get_os_eol_data → alert_os_eos` task dependency). If `get_os_eol_data` fails, alerting will not run.
