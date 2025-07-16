---
title: Normalizing requests
description: Learn how to normalize requests by transforming them using traffic filter rules in AEM as a Cloud Service.
version: Experience Manager as a Cloud Service
feature: Security
topic: Security, Administration, Architecture
role: Admin, Architect
level: Intermediate
doc-type: Tutorial
last-substantial-update: 2025-06-04
jira: KT-18313
thumbnail: 
---
# Normalizing requests

Learn how to normalize requests by transforming them using traffic filter rules in AEM as a Cloud Service.

## Why and when to transform requests

Request transformations are useful when you want to normalize incoming traffic and reduce unnecessary variance caused by unneeded query parameters or headers. This technique is commonly used to:

- Improve caching efficiency by stripping cache-busting parameters that aren't relevant to the AEM application.
- Protect the origin from abuse by minimizing request permutations and mitigating unnecessary processing.
- Sanitize or simplify requests before they are forwarded to AEM.

These transformations are typically applied at the CDN layer, especially for AEM Publish tiers that serve public traffic.

## Prerequisites

Before proceeding, ensure you've completed the required setup as described in the [How to set up traffic filter and WAF rules](../setup.md) tutorial. Also, you have cloned and deployed the [AEM WKND Sites Project](https://github.com/adobe/aem-guides-wknd) to your AEM environment.

## Example: Unset query parameters not needed by the application

In this example, you configure a rule that **removes all query parameters except** `search` and `campaignId` to reduce cache fragmentation.

- Add the following rule to the WKND project's `/config/cdn.yaml` file.

```yaml
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
data:
  requestTransformations:
    rules:
    # Unset all query parameters except those needed for search and campaignId
    - name: unset-all-query-params-except-those-needed
      when:
        reqProperty: tier
        in: ["publish"]
      actions:
        - type: unset
          queryParamMatch: ^(?!search$|campaignId$).*$
```

- Commit and push the changes to the Cloud Manager Git repository.

- Deploy the changes to the AEM environment using the Cloud Manager config pipeline [created earlier](../setup.md#deploy-rules-using-adobe-cloud-manager).

- Test the rule by accessing the WKND site's page, for example `https://publish-pXXXX-eYYYY.adobeaemcloud.com/us/en.html?search=foo&campaignId=bar&otherParam=baz`.

- In AEM logs (`aemrequest.log`), you should see that the request is transformed to `https://publish-pXXXX-eYYYY.adobeaemcloud.com/us/en.html?search=foo&campaignId=bar`, with the `otherParam` removed.

  ![WKND request transformation](../assets/how-to/aemrequest-log-transformation.png)

