> **Note**
> The content of this repo is not officially supported by Dynatrace!

# :tada: :tada: Welcome to the Customer Success hub :tada: :tada:

You'll find open source solutions that help you level up your observability game with Dynatrace.


## Dynatrace Tenant Review
*The assistant that helps you get the maximum value from the Dynatrace platform.*

![Dynatrace Tenant Review](https://github.com/dynatrace-oss/CustomerSuccess/blob/main/Dynatrace%20Tenant%20Review/screenshot.png "Dynatrace Tenant Review")

This Dashboard highly leverages code tiles to perform a wide and deep analysis of your actual state of configuration and adoption of top Dynatrace capabilities.

Admins can download and import the JSON definition of the DTR Dashboard in their own tenant to discover what fundamentals, best practices and recommendations they should prioritize and implement to maximize Dynatrace's positive impact in their organization.

The Dynatrace Tenant Review is:
 - **Safe**: The Dashboards app and the DTR are both restricted to read-only permissions/calls by design. Furthermore, no data ever leaves the Dynatrace tenant.
 - **Fast**: The analytics happens where the data resides, in Grail™.
 - **Open source**: Copy, inspect, customize and share it in a few clicks!

## Software Obsolescence Management
*The solution that lets you stay on top of your software portfolio.*

![Software Obsolescence Management](https://github.com/dynatrace-oss/CustomerSuccess/blob/main/Software%20Obsolescence%20Management/screenshot.png "Software Obsolescence Management")

The JavaScript Workflow regularly refreshes obsolescence data required for your environment from external open source APIs. The DQL Dashboard matches this external data with native Dynatrace data to let you discover prioritized maintenance actions to keep your software components and operations safe, compliant and supported by the corresponding vendors (when applicable).

**Installation**: Download and import the JSON definition of the Dashboard in their own tenant and follow the instructions provided in its bottom-right corner tile.

**Usage**:
- Scope the audit by Management Zone or Tag by defining the corresponding variable (below the dashboard's title)
- Filter which obsolescence statuses you need to display to stay focus
- Prioritize your maintenance by vulnerability and obsolescence risk, criticity and radius of the affected software components
- Share the filtered view's URL to the responsible team so that they keep their software safe and supported
- Navigate to the associated entity by clicking any entry in the full-detail tables and then on "Open record with"
- Extend your OneAgent coverage to reduce obsolescence risks. The [Discovery mode](https://www.dynatrace.com/platform/infrastructure-observability/foundation-and-discovery/) + [Code Module injection](https://docs.dynatrace.com/docs/observe/infrastructure-monitoring/hosts/monitoring-modes#code-module-injection) are sufficient for that capability.
- [Activate AppSec](https://docs.dynatrace.com/docs/secure/application-security/application-protection) to reduce security risks from vulnerabilities. The [Discovery mode](https://www.dynatrace.com/platform/infrastructure-observability/foundation-and-discovery/) + [Code Module injection](https://docs.dynatrace.com/docs/observe/infrastructure-monitoring/hosts/monitoring-modes#code-module-injection) are sufficient for that capability.

**Request For Enhancement**: https://dt-url.net/som-rfe

**Credits**:
- [endoflife.date](https://endoflife.date) (for OS and Technology obsolescence data)
- [deps.dev](https://deps.dev) (for Library obsolescence data)
- [Dynatrace AppSec](https://docs.dynatrace.com/docs/secure/application-security/vulnerability-analytics/vulnerabilities) (for Vulnerability insights)
