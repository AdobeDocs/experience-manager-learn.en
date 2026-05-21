---
title: Restricting access
description: Learn how to restrict access by blocking specific requests using traffic filter rules in AEM as a Cloud Service.
version: Experience Manager as a Cloud Service
feature: Security
topic: Security, Administration, Architecture
role: Admin, Developer
level: Intermediate
doc-type: Tutorial
last-substantial-update: 2025-06-04T00:00:00.000Z
jira: KT-18312
thumbnail: null
exl-id: 53cb8996-4944-4137-a979-6cf86b088d42
TQID: https://experienceleague.adobe.com/yRyP1V-kZEObMevSOR8iM9TZtmm-3TZOSPmwTP9nsK4
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# Restricting access

Learn how to restrict access by blocking specific requests using traffic filter rules in AEM as a Cloud Service.

This tutorial demonstrates how to **block requests to internal paths from public IPs** in the AEM Publish service.

## Why and when to block requests

Blocking traffic helps enforce organizational security policies by preventing access to sensitive resources or URLs under certain conditions. Compared to logging, blocking is a stricter action and should be used when you are confident that traffic from specific sources is unauthorized or unwanted.

Common scenarios where blocking is appropriate include:

- Restricting access to `internal` or `confidential` pages to only internal IP ranges (for example, behind a corporate VPN).
- Blocking bot traffic, automated scanners, or threat actors identified by IP or geolocation.
- Preventing access to deprecated or unsecured endpoints during staged migrations.
- Limiting access to authoring tools or admin routes in Publish tiers.

## Prerequisites

Before proceeding, ensure you've completed the required setup as described in the [How to set up traffic filter and WAF rules](../setup.md) tutorial. Also, you have cloned and deployed the [AEM WKND Sites Project](https://github.com/adobe/aem-guides-wknd) to your AEM environment.

## Example: Block internal paths from public IPs

In this example, you configure a rule to block external access to an internal WKND page, such as `https://publish-pXXXX-eYYYY.adobeaemcloud.com/content/wknd/internal/demo-page.html`, from public IP addresses. Only users within a trusted IP range (such as a corporate VPN) can access this page.

You can either create your own internal page (for example, `demo-page.html`) or use the [attached package](../assets/how-to/demo-internal-pages-package.zip).

- Add the following rule to the WKND project's `/config/cdn.yaml` file.

```yaml
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
data:
  trafficFilters:
    rules:
    # Block requests to (demo) internal only page/s from public IP address but allow from internal IP address.
    # Make sure to replace the IP address with your own IP address.
    - name: block-internal-paths
      when:
        allOf:
          - reqProperty: path
            matches: /content/wknd/internal
          - reqProperty: clientIp
            notIn: [192.150.10.0/24]
      action: block    
```

- Commit and push the changes to the Cloud Manager Git repository.

- Deploy the changes to the AEM environment using the Cloud Manager config pipeline [created earlier](../setup.md#deploy-rules-using-adobe-cloud-manager).

- Test the rule by accessing the WKND site's internal page, for example `https://publish-pXXXX-eYYYY.adobeaemcloud.com/content/wknd/internal/demo-page.html` or using the CURL command below:

    ```bash
    $ curl -I https://publish-pXXXX-eYYYY.adobeaemcloud.com/content/wknd/internal/demo-page.html
    ```

- Repeat the above step from both the IP address that you used in the rule and then a different IP address (for example, using your mobile phone).

## Analyzing

To analyze the results of the `block-internal-paths` rule, follow the same steps as described in the [set-up tutorial](../setup.md#cdn-logs-ingestion)

You should see the **Blocked requests** and corresponding values in the client IP (cli_ip), host, URL, action (waf_action), and rule-name (waf_match) columns.

![ELK Tool Dashboard Blocked Request](../assets/how-to/elk-tool-dashboard-blocked.png)
