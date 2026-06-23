> **Note**
> The content of this repo is not officially supported by Dynatrace!

# :tada: :tada: Welcome to the Customer Success hub :tada: :tada:

You'll find open source solutions that help you level up your observability game with Dynatrace.


## Dynatrace Tenant Review
*The assistant that helps you get the maximum value from the Dynatrace platform.*

![Dynatrace Tenant Review](./Dynatrace%20Tenant%20Review/screenshot.png "Dynatrace Tenant Review")

This Dashboard highly leverages code tiles to perform a wide and deep analysis of your actual state of configuration and adoption of top Dynatrace capabilities.

Admins can download and import the JSON definition of the DTR Dashboard in their own tenant to discover what fundamentals, best practices and recommendations they should prioritize and implement to maximize Dynatrace's positive impact in their organization.

The Dynatrace Tenant Review is:
 - **Safe**: The Dashboards app and the DTR are both restricted to read-only permissions/calls by design. Furthermore, no data ever leaves the Dynatrace tenant.
 - **Fast**: The analytics happens where the data resides, in Grail™.
 - **Open source**: Copy, inspect, customize and share it in a few clicks!

## Platform Adoption Dashboard
*The dashboard that gives you full visibility into platform adoption, user engagement, automation health and AI usage across your Dynatrace environment.*

![Platform Adoption Dashboard](./Platform%20Adoption/screenshot.png "Platform Adoption Dashboard")

This Dashboard leverages Grail™ events, query execution telemetry, workflow events and billing data to surface actionable insights about how your organization uses Dynatrace. With 57 tiles across 5 labelled sections it covers active users, stickiness, app adoption rankings, lifecycle cohorts, legacy migration tracking, workflow health, DQL analytics, Dynatrace Intelligence and Dynatrace Assist usage, and more.

Admins can download and import the JSON definition of the Dashboard in their own tenant to understand which teams are active, which platform capabilities are under-utilized, and where to focus enablement efforts.

The Platform Adoption Dashboard is:

 - **Safe**: Restricted to read-only audit event queries by design. No data ever leaves the Dynatrace tenant.
 - **Fast**: All analytics happen where the data resides, in Grail™.
 - **Open source**: Copy, inspect, customize and share it in a few clicks!

**Installation**: Download and import the JSON of the Dashboard into your Dynatrace tenant via the Dashboards app.

**Usage**:

- Monitor overall platform adoption with KPI cards (Active Users, Stickiness, User Sessions, Maturity Score)
- Track user lifecycle cohorts (New, Active, At-Risk, Churned) and retention
- Identify top power users and app-level usage rankings
- Measure 3rd Gen adoption rate — hybrid users are weighted at 0.5x for a more accurate migration signal
- Identify Classic-Only Users without Gen3 activity (API/UUID noise filtered out)
- Analyze DQL query volume, data consumption and domain coverage
- Monitor workflow execution health and automation trends
- Track Dynatrace Assist and Dynatrace Intelligence usage across the platform
- Review 5 dedicated **Dynatrace Assist Report** tiles at the top of the dashboard: Adoption Report, Platform Breadth, Dormant Users, At-Risk/Churned Cohorts, and Grail Blind Spots
- Generate a **Dynatrace Assist narrative report** summarizing adoption trends, top users, trending/fading apps, and recommended next steps for the past 30 days
- Share filtered views with stakeholders to drive adoption initiatives

**What's new in v1.3.0**:

- Branding updated: Davis CoPilot → **Dynatrace Assist**, Davis AI → **Dynatrace Intelligence**, sessions/pageviews → **userSessions/userActions**
- Gen3 Adoption Rate formula corrected: hybrid users now weighted at **0.5x** instead of counted as full adopters
- Classic-Only Users tile rebuilt to cross-reference Gen3 data — API calls and UUID-style logins no longer inflate the count
- External API Access and Platform Capability Usage tiles rebuilt with correct DQL fields
- 5 new **Dynatrace Assist Report** tiles added and grouped at the top of the dashboard
- 5 new section headers added for easier navigation
- All 44 existing tile descriptions rewritten for clarity; encoding corruption resolved
- Total tile count: **48 → 57**

## Software Obsolescence Management
*The solution that lets you stay on top of your software portfolio.*

![Software Obsolescence Management](./Software%20Obsolescence%20Management/screenshot.png "Software Obsolescence Management")

The JavaScript Workflow regularly refreshes obsolescence data required for your environment from external open source APIs. The DQL Dashboard matches this external data with native Dynatrace data to let you discover prioritized maintenance actions to keep your software components and operations safe, compliant and supported by the corresponding vendors (when applicable).

**Installation**: Download and import the JSON definition of the Dashboard in their own tenant and follow the instructions provided in its bottom-right corner tile.

**Usage**:
- Scope the audit by Segment, Management Zone or Tag
- Filter by obsolescence statuses
- Filter by Operating Systems, Technologies and Libraries
- Prioritize your maintenance by vulnerability and obsolescence risk, criticity and radius of the affected software components or even time remaining before obsolescence
- Share the filtered view's URL to the responsible team so that they keep their software safe and supported
- Navigate to the associated entity by clicking any entry in the full-detail tables and then on "Open record with"
- Extend your OneAgent coverage to reduce obsolescence risks. The [Discovery mode](https://www.dynatrace.com/platform/infrastructure-observability/foundation-and-discovery/) + [Code Module injection](https://docs.dynatrace.com/docs/observe/infrastructure-monitoring/hosts/monitoring-modes#code-module-injection) are sufficient for that capability.
- [Activate AppSec](https://docs.dynatrace.com/docs/secure/application-security/application-protection) to reduce security risks from vulnerabilities. The [Discovery mode](https://www.dynatrace.com/platform/infrastructure-observability/foundation-and-discovery/) + [Code Module injection](https://docs.dynatrace.com/docs/observe/infrastructure-monitoring/hosts/monitoring-modes#code-module-injection) are sufficient for that capability.
- Update the "SupportOverrides" variable with your own support terms (cf. installation step 7)
- Get alerted 30 days before any OS becomes obsolete
- Track the solution's usage of the platform to understand and optimize its cost

**Request For Enhancement**: https://dt-url.net/som-rfe

**Credits**:
- [endoflife.date](https://endoflife.date) (for OS and Technology obsolescence data)
- [deps.dev](https://deps.dev) (for Library obsolescence data)
- [Dynatrace AppSec](https://docs.dynatrace.com/docs/secure/application-security/vulnerability-analytics/vulnerabilities) (for Vulnerability insights)
