---
title: Understanding DoS/DDoS prevention
description: Learn how to prevent and mitigate DoS and DDoS attacks against AEM.
version: 6.5, Cloud Service
feature: Security
topic: Security, Development
role: Admin, Architect, Developer
level: Beginner
doc-type: Article
duration: 75
last-substantial-update: 2024-03-30
jira: KT-15219
exl-id: 1d7dd829-e235-4884-a13f-b6ea8f6b4b0b
---
# Understanding DoS/DDoS prevention in AEM

Learn about the options available to prevent and mitigate DoS and DDoS attacks on your AEM environment. Before diving into the prevention mechanisms, a brief overview of [DoS](https://developer.mozilla.org/en-US/docs/Glossary/DOS_attack) and [DDoS](https://developer.mozilla.org/en-US/docs/Glossary/Distributed_Denial_of_Service).

- DoS (Denial of Service) and DDoS (Distributed Denial of Service) attacks are both malicious attempts to disrupt the normal functioning of a targeted server, service, or network, making it inaccessible to its intended users. 
- DoS attacks typically originate from a single source, while DDoS attacks come from multiple sources.
- DDoS attacks are often larger in scale compared to DoS attacks due to the combined resources of multiple attacking devices.
- These attacks are carried out by flooding the target with excessive traffic, and exploit vulnerabilities in network protocols.

The following table describes how to prevent and mitigate DoS and DDoS attacks:

<table>
    <tbody>
        <tr>
            <td><strong>Prevention Mechanism</strong></td>
            <td><strong>Description</strong></td>
            <td><strong>AEM as a Cloud Service</strong></td>
            <td><strong>AEM 6.5 (AMS)</strong></td>
            <td><strong>AEM 6.5 (On-prem)</strong></td>
        </tr>
        <tr>
            <td>Web Application Firewall (WAF)</td>
            <td>A security solution designed to protect web applications from various types of attacks.</td>
            <td>
            <a href="https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/examples-and-analysis#waf-rules" target="_blank">WAF-DDoS Protection license</a></td>
            <td><a href="https://docs.aws.amazon.com/waf/" target="_blank">AWS</a> or <a href="https://azure.microsoft.com/en-us/products/web-application-firewall" target="_blank">Azure</a> WAF via AMS contract.</td>
            <td>Your preferred WAF</td>
        </tr>
        <tr>
            <td>ModSecurity</td>
            <td>ModSecurity (aka `mod_security` Apache module) is an open-source, cross-platform solution that provides protection from a range of attacks against web applications.<br/> In AEM as a Cloud Service, this is only applicable to AEM Publish service as there is no Apache web server and AEM Dispatcher in front of AEM Author service.</td>
            <td colspan="3"><a href="https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection" target="_blank">Enable ModSecurity </a></td>
        </tr>
        <tr>
            <td>Traffic filter rules</td>
            <td>Traffic filter rules can be used to block or allow requests at the CDN layer.</td>
            <td><a href="https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/examples-and-analysis" target="_blank">Example traffic filter rules</a></td>
            <td><a href="https://docs.aws.amazon.com/waf/latest/developerguide/waf-rule-statement-type-rate-based.html" target="_blank">AWS</a> or <a href="https://learn.microsoft.com/en-us/azure/web-application-firewall/ag/rate-limiting-overview" target="_blank">Azure</a> rule limiting features.</td>
            <td>Your preferred solution</td>
        </tr>
    </tbody>
</table>

## Post-incident analysis and continuous improvement

While there isn't a one-size-fits-all standard flow for identifying and preventing DoS/DDoS attacks and it depends on your organization's security process. The **post-incident analysis and continuous improvement** is a crucial step in the process. Here are some best practices to consider:

- Identify the root cause of the DoS/DDoS attack by conducting a post-incident analysis, including reviewing logs, network traffic, and system configurations.
- Improve prevention mechanisms based on the findings from the post-incident analysis.

