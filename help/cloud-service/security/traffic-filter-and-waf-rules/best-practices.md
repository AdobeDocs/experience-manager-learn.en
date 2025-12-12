---
title: Best practices for traffic filter rules including WAF rules
description: Learn recommended best practices for configuring traffic filter rules including WAF rules in AEM as a Cloud Service to enhance security and mitigate risks.
version: Experience Manager as a Cloud Service
feature: Security
topic: Security, Administration, Architecture
role: Admin, Developer
level: Intermediate
doc-type: Tutorial
last-substantial-update: 2025-06-04
jira: KT-18310
thumbnail: null
exl-id: 4a7acdd2-f442-44ee-8560-f9cb64436acf
---
# Best practices for traffic filter rules including WAF rules

Learn recommended best practices for configuring traffic filter rules including WAF rules in AEM as a Cloud Service to enhance security and mitigate risks.

>[!IMPORTANT]
>
>The best practices described in this article are not exhaustive and are not intended to be a substitute for your own security policies and procedures.

## General best practices

- Start with the [recommended set](./overview.md#adobe-recommended-rules) of standard traffic filter and WAF rules provided by Adobe, and tweak them based on your application's specific needs and threat landscape.
- Collaborate with your security team to determine which rules align with your organization's security posture and compliance requirements.
- Always test new or updated rules in Development environments before promoting them to Stage and Production.
- When declaring and validating rules, begin with the `action` type `log` to observe behavior without blocking legitimate traffic.
- Move from `log` to `block` only after analyzing sufficient traffic data and confirming that no valid requests are being affected.
- Introduce rules incrementally, involving QA, performance, and security testing teams to identify unintended side effects.
- Regularly review and analyze rule effectiveness using [dashboard tooling](https://github.com/adobe/AEMCS-CDN-Log-Analysis-Tooling). Frequency of review (daily, weekly, monthly) should align with your site's traffic volume and risk profile.
- Continuously refine rules based on new threat intelligence, traffic behavior, and audit results.

## Best practices for traffic filter rules

- Use Adobe [recommended standard traffic filter rules](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/traffic-filter-rules-including-waf#recommended-starter-rules) as a baseline, which includes rules for edge, origin protection, and OFAC-based restrictions.
- Review alerts and logs regularly to identify patterns of abuse or misconfiguration.
- Adjust threshold values for rate limits based on your application's traffic patterns and user behavior.

    See the following table for guidance on how to choose the threshold values:

    | Variation  | Value     |
    | :--------- | :------- |
    | Origin    | Take the highest value of the Max Origin Requests per IP/POP under **normal** traffic conditions (that is, not the rate at the time of a DDoS) and increase it by a multiple |
    | Edge    | Take the highest value of the Max Edge Requests per IP/POP under **normal** traffic conditions (that is, not the rate at the time of a DDoS) and increase it by a multiple |

    Also see the [choosing threshold values](../blocking-dos-attack-using-traffic-filter-rules.md#choosing-threshold-values) section for more details.

- Move to `block` action only after confirming that the `log` action does not impact legitimate traffic.

## Best practices for WAF rules

- Start with the Adobe [recommended WAF rules](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/traffic-filter-rules-including-waf#recommended-nonwaf-starter-rules), which include rules for blocking known bad IPs, detecting DDoS attacks, and mitigating bot abuse.
- The `ATTACK` WAF flag should alert you to potential threats. Make sure that there are no false positives before moving to `block`.
- If recommended WAF rules do not cover specific threats, consider creating custom rules based on your application's unique requirements. See a complete list of [WAF flags](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/traffic-filter-rules-including-waf#waf-flags-list) in the documentation.

## Implementing rules

Learn how to implement traffic filter rules and WAF rules in AEM as a Cloud Service:

<!-- CARDS
{target = _self}

* ./use-cases/using-traffic-filter-rules.md
  {title = Protecting AEM websites using standard traffic filter rules}
  {description = Learn how to protect AEM websites from DoS, DDoS and bot abuse using Adobe-recommended standard traffic filter rules in AEM as a Cloud Service.}
  {image = ./assets/use-cases/using-traffic-filter-rules.png}
  {cta = Apply Rules}

* ./use-cases/using-waf-rules.md
  {title = Protecting AEM websites using WAF traffic filter rules}
  {description = Learn how to protect AEM websites from sophisticated threats including DoS, DDoS, and bot abuse using Adobe-recommended Web Application Firewall (WAF) traffic filter rules in AEM as a Cloud Service.}
  {image = ./assets/use-cases/using-waf-rules.png}
  {cta = Activate WAF}
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Protecting AEM websites using standard traffic filter rules">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./use-cases/using-traffic-filter-rules.md" title="Protecting AEM websites using standard traffic filter rules" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="./assets/use-cases/using-traffic-filter-rules.png" alt="Protecting AEM websites using standard traffic filter rules"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./use-cases/using-traffic-filter-rules.md" target="_self" rel="referrer" title="Protecting AEM websites using standard traffic filter rules">Protecting AEM websites using standard traffic filter rules</a>
                    </p>
                    <p class="is-size-6">Learn how to protect AEM websites from DoS, DDoS and bot abuse using Adobe-recommended standard traffic filter rules in AEM as a Cloud Service.</p>
                </div>
                <a href="./use-cases/using-traffic-filter-rules.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Apply Rules</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Protecting AEM websites using WAF rules">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./use-cases/using-waf-rules.md" title="Protecting AEM websites using WAF rules" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="./assets/use-cases/using-waf-rules.png" alt="Protecting AEM websites using WAF rules"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./use-cases/using-waf-rules.md" target="_self" rel="referrer" title="Protecting AEM websites using WAF rules">Protecting AEM websites using WAF rules</a>
                    </p>
                    <p class="is-size-6">Learn how to protect AEM websites from sophisticated threats including DoS, DDoS, and bot abuse using Adobe-recommended Web Application Firewall (WAF) rules in AEM as a Cloud Service.</p>
                </div>
                <a href="./use-cases/using-waf-rules.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Activate WAF</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Additional resources

- [Traffic Filter Rules Including WAF Rules](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/traffic-filter-rules-including-waf)
- [Understanding DoS/DDoS prevention in AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/security/understanding-dos-and-prevention-approaches)
- [Blocking DoS and DDoS attacks using traffic filter rules](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/security/blocking-dos-attack-using-traffic-filter-rules)
