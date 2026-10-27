# Integration Guide — Generic Interactive USA Map for AEM Sites

## 1. Overview

This guide explains how to integrate the **Generic Interactive USA Map** component into an existing Adobe Experience Manager (AEM) as a Cloud Service project.

The component is primarily designed to visualize **AEM Adaptive Form submissions by U.S. state**, but it can also display other aggregated state-level metrics from compatible REST APIs.

AEM developers can install the component, configure a REST endpoint through the authoring dialog, and display geographic data without modifying the map's rendering logic.

The component is independent of the backend datasource and does not require Azure SQL, Azure Functions, or any particular database technology.

## 2. Prerequisites

Before beginning, ensure you have:

- An AEM as a Cloud Service Maven project with a `ui.apps` module.
- Access to the project's source code and Adobe Cloud Manager deployment pipeline.
- An editable AEM Sites template.
- A REST API returning compatible JSON.
- Node.js only if you intend to modify or rebuild the frontend assets.

The repository provides precompiled JavaScript and CSS, so a separate frontend build is not required for basic installation.

## 3. Download the Component

Clone or download the Generic Interactive USA Map repository.

The repository contains:

```text
aem-generic-usa-map/
├── README.md
├── component/
│   ├── .content.xml
│   ├── usamap.html
│   └── _cq_dialog/
│       └── .content.xml
├── clientlib/
│   ├── .content.xml
│   ├── css.txt
│   ├── js.txt
│   ├── css/
│   │   └── usa-map.css
│   └── js/
│       └── usa-map.js
├── frontend/
│   ├── usa-map.js
│   └── usa-map.scss
├── examples/
│   └── sample-response.json
└── docs/
    └── integration-guide.md
```

The `component` directory contains the AEM component definition, HTL template, and authoring dialog.

The `clientlib` directory contains the deployable JavaScript and compiled CSS.

The `frontend` directory contains the source files for developers who want to customize the component.

## 4. Install the AEM Component

In your existing AEM Maven project, navigate to:

```text
ui.apps/src/main/content/jcr_root/apps/
```

Create:

```text
generic/components/usamap/
```

Copy the files from the repository's `component` directory into this folder.

The resulting structure should be:

```text
ui.apps/
└── src/main/content/jcr_root/apps/
    └── generic/
        └── components/
            └── usamap/
                ├── .content.xml
                ├── usamap.html
                └── _cq_dialog/
                    └── .content.xml
```

The component is registered with the Sling resource type:

```text
generic/components/usamap
```

Its component group is:

```text
Generic Data Visualization
```

## 5. Install the AEM Client Library

Create the following directory:

```text
ui.apps/src/main/content/jcr_root/apps/generic/clientlibs/clientlib-usamap/
```

Copy the contents of the repository's `clientlib` directory into it.

The resulting structure should be:

```text
clientlib-usamap/
├── .content.xml
├── css.txt
├── js.txt
├── css/
│   └── usa-map.css
└── js/
    └── usa-map.js
```

Verify that `.content.xml` contains:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root
    xmlns:jcr="http://www.jcp.org/jcr/1.0"
    jcr:primaryType="cq:ClientLibraryFolder"
    categories="[generic.usamap]"
    allowProxy="{Boolean}true"/>
```

The client library category must match the category referenced in `usamap.html`:

```text
generic.usamap
```

The component loads its JavaScript and CSS through this client library.

**Note:** If you use the precompiled client library, you do not need to integrate `frontend/usa-map.js` or `frontend/usa-map.scss` into your existing Webpack configuration. Avoid loading both copies simultaneously.

## 6. Update FileVault Configuration

Open:

```text
ui.apps/src/main/content/META-INF/vault/filter.xml
```

Ensure that the component and client library repository paths are included in the content package.

Example:

```xml
<filter root="/apps/generic/components/usamap"/>
<filter root="/apps/generic/clientlibs/clientlib-usamap"/>
```

Add these inside the existing `<workspaceFilter>` element.

Do not duplicate filters if broader entries already cover these paths.

If your project uses a separate repository structure package, ensure the new paths are also declared appropriately.

## 7. Configure External Map Dependencies

The map uses:

- D3.js for geographic rendering.
- TopoJSON for processing geographic boundaries.
- US Atlas for U.S. state geometry.

The current implementation loads these dependencies from external CDN endpoints.

Ensure your AEM site's Content Security Policy allows the required external scripts and geographic data requests.

For production environments, consider bundling approved versions of these dependencies locally to avoid reliance on external CDN availability.

## 8. Build and Deploy

From your AEM Maven project root, run:

```bash
mvn clean verify -DskipTests
```

Confirm that the build completes successfully.

Commit the component and client library files to your AEM project's Git repository.

Deploy the changes using your Adobe Cloud Manager pipeline.

After deployment, verify that the component is registered at:

```text
/apps/generic/components/usamap
```

and the client library is available at:

```text
/apps/generic/clientlibs/clientlib-usamap
```

## 9. Enable the Component in an AEM Template

In AEM Author:

1. Navigate to **Tools → General → Templates**.
2. Open the editable template used by your target page.
3. Switch to Structure mode.
4. Select the appropriate Layout Container.
5. Open its Policy settings.
6. Under Allowed Components, locate **Generic Data Visualization**.
7. Enable **Generic Interactive USA Map**.
8. Save the policy.

The component should now appear in the AEM Sites component browser.

## 10. Add the Component to a Page

Open an AEM Sites page in Edit mode.

Drag **Generic Interactive USA Map** into an allowed container.

Open its Configure dialog.

### General Settings

| Property | Example |
|---|---|
| Map Title | USA Form Submissions |
| Metric Label | Submissions |
| Show Summary Statistics | Enabled |

### Data Source Settings

| Property | Example |
|---|---|
| Data Source Type | REST API |
| Data Endpoint | `/api/forms/states/counts` |
| State Field | `state` |
| Value Field | `count` |

### Interaction Settings

Enable or disable state tooltips.

Save the configuration and publish the page.

## 11. REST API Data Contract

The component expects an HTTP GET endpoint returning aggregated state-level data in JSON format.

Example:

```json
{
  "states": [
    {"state": "CA", "count": 150},
    {"state": "TX", "count": 95},
    {"state": "NY", "count": 70}
  ]
}
```

The response must contain either a `states` array or a top-level array of state records.

Each record must contain:

- A two-letter U.S. state code.
- A numeric value associated with that state.

Field names are configurable through the component dialog.

For example:

```json
{
  "states": [
    {"stateCode": "CA", "submissionTotal": 150},
    {"stateCode": "TX", "submissionTotal": 95}
  ]
}
```

Configure:

```text
State Field: stateCode
Value Field: submissionTotal
```

**Important:** The REST API is responsible for retrieving, aggregating, and formatting the data into the expected state-level JSON structure. The component does not execute database queries or aggregate individual form submissions.

## 12. Try the Component with a Sample REST API

A sample REST API is available to help AEM developers evaluate the component without implementing their own backend.

**HTTP Method:** GET

**Endpoint:**

https://ic-document-service.onrender.com/api/states/sales

The API returns simulated sales data aggregated by U.S. state.

### Example Response

```json
{
  "total": 485,
  "states": [
    {"state": "CA", "count": 150},
    {"state": "TX", "count": 95},
    {"state": "NY", "count": 70},
    {"state": "FL", "count": 55},
    {"state": "WA", "count": 40},
    {"state": "GA", "count": 25},
    {"state": "IL", "count": 20},
    {"state": "AZ", "count": 15},
    {"state": "CO", "count": 10},
    {"state": "ME", "count": 5}
  ]
}
```

### Configure the Component

| Property | Value |
|---|---|
| Map Title | USA Sales Dashboard |
| Metric Label | Sales |
| Data Source Type | REST API |
| Data Endpoint | `https://ic-document-service.onrender.com/api/states/sales` |
| State Field | `state` |
| Value Field | `count` |
| Show Summary Statistics | Enabled |
| Show Tooltips | Enabled |

### Expected Result

The map displays:

- Total sales: **485**
- States represented: **10**
- Top state: **California (CA)**
- States shaded according to their sales values
- Interactive state selection showing each state's metric

### CORS Requirement

The sample API was initially configured to permit requests from specific AEM environments.

To use it from another AEM domain, the API must permit that origin through its CORS configuration.

Opening the endpoint directly in a browser does not verify cross-origin access.

The AEM site's Content Security Policy must also allow requests to the Render API hostname.

The sample endpoint is provided for demonstration purposes and may experience startup delays or temporary unavailability.

## 13. Integrate with an AEM Forms Submission API

To display actual AEM Adaptive Form submission counts, configure the component to use a REST API that returns submissions aggregated by U.S. state.

A typical architecture is:

```text
AEM Adaptive Form
       |
       v
Submission Backend
       |
       v
Database / Storage
       |
       v
State Aggregation REST API
       |
       v
Generic Interactive USA Map
```

The backend may use Azure SQL, PostgreSQL, another database, or an external service.

The component only requires a compatible JSON response.

If the REST API requires credentials, use an appropriately secured backend integration. Do not expose API keys or secrets in the component dialog or frontend JavaScript.

## 14. Verify the Integration

After publishing the page:

1. Confirm the map renders correctly.
2. Verify that the REST endpoint returns HTTP 200.
3. Confirm the map displays the expected state values.
4. Verify the summary statistics.
5. Click a state and confirm the corresponding value appears.
6. Test state tooltips when enabled.
7. Inspect the browser console for JavaScript errors.

## 15. Troubleshooting

| Issue | Possible Cause |
|---|---|
| Component not visible | Component registration or template policy |
| Map not rendering | Client library or external dependency loading |
| HTTP 404 | Incorrect REST endpoint |
| HTTP 401 | Authentication required or invalid credentials |
| CORS error | API does not permit the AEM origin |
| CSP error | Site blocks requests to the API hostname |
| Incorrect values | State/value field mapping mismatch |
| Slow loading | REST API latency or external dependency loading |

## 16. Customization

Developers can modify the component using:

```text
frontend/usa-map.js
frontend/usa-map.scss
```

After making changes, regenerate the deployable JavaScript and CSS in `clientlib/`.

Ensure the deployable files match the updated source.

## 17. Summary

The Generic Interactive USA Map provides a reusable visualization component for AEM Sites.

Its primary purpose is to display **aggregated AEM Adaptive Form submissions by U.S. state**, but it can also visualize other compatible state-based metrics.

By installing the component and configuring a REST endpoint, AEM developers can add geographic data visualization to their Sites pages without building a custom map or depending on a specific backend technology.