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

This Dashboard leverages Grail™ events, query execution telemetry, workflow events and billing data to surface actionable insights about how your organization uses Dynatrace. With 40 tiles it covers active users, stickiness, app adoption rankings, lifecycle cohorts, legacy migration tracking, workflow health, DQL analytics, AI/Copilot usage and more.

Admins can download and import the JSON definition of the Dashboard in their own tenant to understand which teams are active, which platform capabilities are under-utilized, and where to focus enablement efforts.

The Platform Adoption Dashboard is:

 - **Safe**: Restricted to read-only audit event queries by design. No data ever leaves the Dynatrace tenant.
 - **Fast**: All analytics happen where the data resides, in Grail™.
 - **Open source**: Copy, inspect, customize and share it in a few clicks!

**Installation**: Download and import the JSON of the Dashboard into your Dynatrace tenant via the Dashboards app.

**Usage**:

- Monitor overall platform adoption with KPI cards (Active Users, Stickiness, Sessions, Maturity Score)
- Track user lifecycle cohorts (New, Active, At-Risk, Churned) and retention
- Identify top power users and app-level usage rankings
- Measure 3rd Gen adoption rate and identify legacy migration candidates
- Analyze DQL query volume, data consumption and domain coverage
- Monitor workflow execution health and automation trends
- Track Davis Copilot and AI/Agent usage across the platform
- Generate a **Davis AI narrative report** summarizing adoption trends, top users, trending/fading apps, and recommended next steps for the past 30 days
- Share filtered views with stakeholders to drive adoption initiatives

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
