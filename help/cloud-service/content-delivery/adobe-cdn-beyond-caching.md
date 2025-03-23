---
title: Adobe CDN - Advanced features beyond caching
description: Learn about advanced features of Adobe CDN beyond caching, such as configuring traffic at the CDN, setting up tokens and credentials, CDN error pages and more.
version: Experience Manager as a Cloud Service
feature: Website Performance, CDN Cache
topic: Architecture, Performance, Content Management
role: Developer, Architect, User, Leader
level: Beginner
doc-type: Article
duration: 0
last-substantial-update: 2024-08-21
jira: KT-15123
thumbnail: KT-15123.jpeg
exl-id: 8948a900-01e9-49ed-9ce5-3a057f5077e4
---
# Adobe CDN - Advanced features beyond caching

Learn about advanced features of Adobe Content Delivery Network (CDN) beyond caching, such as configuring traffic at the CDN, setting up tokens and credentials, CDN error pages and more.

Beyond caching content, Adobe CDN offers several advanced features that can help to optimize your website performance. These features include:

- Configuring traffic at the CDN
- Configuring CDN credentials and authentication
- CDN error pages

These features are **self-service** features. Configured in the `cdn.yaml` file of your AEM project and deployed using the Cloud Manager config pipeline.

>[!VIDEO](https://video.tv.adobe.com/v/3433104?quality=12&learn=on)

## Configuring traffic at the CDN

Let's understand the key capabilities related to _Configuring traffic at the CDN_:

- **DoS attack prevention:** Adobe CDN absorbs DoS attacks at the network layer, preventing them from reaching your origin server.
- **Rate limiting:** To protect your origin server from being overwhelmed with too many requests, you can configure rate limiting on the CDN.
- **Web Application Firewall (WAF):** The WAF protects your website from common web application vulnerabilities, such as SQL injection, cross-site scripting, and more. The Enhanced Security license or WAF-DDoS Protection license is required to use this feature.
- **Request transformation:** Modify incoming requests such as setting or unsetting headers, modifying query parameters, cookies and more.
- **Response transformation:** Modify outgoing responses such as setting or unsetting headers.
- **Origin selection:** Route traffic to different origin servers (Adobe and non-Adobe) based on the request URL.
- **URL redirect:** Redirect requests (HTTP 301/302) to a different absolute or relative URL.

## Configuring CDN credentials and authentication

Let's understand the key capabilities related to _Configuring CDN credentials and authentication_:

- **Purge API Token**: Enables you to create your own purge key for purging a single or group or all resources from the cache.
- **Basic Authentication**: A lightweight authentication mechanism when you want to restrict access to your website or a part of it. Mostly required as part of various review processes before going live.
- **HTTP Header validation**: Used when a customer managed CDN is routing traffic to Adobe CDN. The Adobe CDN validates the incoming request based on the `X-AEM-Edge-Key` header value. Enables you to create your own value for the `X-AEM-Edge-Key` header.

## CDN error pages

Let's understand the key capabilities related to _CDN error pages_:

- **Branded error pages**: Display a branded error page to your users in the _unlikely scenario_ when the Adobe CDN is unable to reach your origin server.

## How to implement

The implementation of these advanced features involves two steps:

1. **Update CDN config file**: Update the `cdn.yaml` file in your AEM project with the required configurations. The configurations are added as rules and they follow a rule syntax. The rule three main components: `name`, `when` and `action`.

2. **Deploy CDN config file**: Deploy the updated `cdn.yaml` file using the Cloud Manager config pipeline. For more information, see [Deploy rules through Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/how-to-setup#deploy-rules-through-cloud-manager).

### Example

In below example, the sample WKND site is configured to redirect the `/top3` URL to `/us/en/top3.html`.

```yaml
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
data:
  redirects:
    rules:
      - name: redirect-top3-adventures
        when: { reqProperty: path, equals: "/top3" }
        action:
          type: redirect
          status: 302
          location: /us/en/top3.html
```

## Related Tutorials

[Protecting websites with traffic filter rules](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview)

[Configure and deploy HTTP Header validation CDN rule](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/content-delivery/custom-domain-names-with-customer-managed-cdn#configure-and-deploy-http-header-validation-cdn-rule)

[How to purge the CDN cache](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache)

[Configuring CDN Error Pages](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/content-delivery/custom-error-pages#cdn-error-pages)

[Configuring Traffic at the CDN](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#client-side-redirectors)

[Configuring CDN Credentials and Authentication](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-credentials-authentication)

