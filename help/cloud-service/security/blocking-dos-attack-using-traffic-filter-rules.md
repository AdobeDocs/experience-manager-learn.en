---
title: Blocking DoS, DDoS and sophisticated attacks using traffic filter rules
description: Learn how to block DoS, DDoS and sophisticated attacks using traffic filter rules in AEM as a Cloud Service.
version: Experience Manager as a Cloud Service
feature: Security, Operations
topic: Security, Administration, Performance
role: Admin, Developer
level: Intermediate
doc-type: Tutorial
duration: 436
last-substantial-update: 2024-04-19
jira: KT-15184
thumbnail: KT-15184.jpeg
exl-id: 60c2306f-3cb6-4a6e-9588-5fa71472acf7
---
# Blocking DoS, DDoS and sophisticated attacks using traffic filter rules

Learn how to block Denial of Service (DoS), Distributed Denial of Service (DDoS) and sophisticated attacks using **traffic filter rules** in the AEM as a Cloud Service (AEMCS) managed CDN.

These attacks cause traffic spikes at the CDN and potentially at the AEM Publish service (aka origin) and can impact site responsiveness and availability.

This article provides an overview of the default protections for your AEM website, and how to extend those protections through customer configuration. It also describes how to analyze traffic patterns and configure standard traffic filter rules to block those attacks.

## Default protections in AEM as a Cloud Service

Let's understand the default DDoS protections for your AEM website:

- **Caching:** With good caching policies, the impact of a DDoS attack is more limited because the CDN prevents most requests from going to the origin and causing performance degradation.
- **Autoscaling:** The AEM author and publish services autoscale to handle traffic spikes, although they can still be impacted by sudden, massive increases in traffic.
- **Blocking:** The Adobe CDN blocks traffic to the origin if it exceeds an Adobe-defined rate from a particular IP address, per CDN PoP (Point of Presence).
- **Alerting:** The Actions Center sends a traffic spike at origin alert notification when traffic exceeds a certain rate. This alert fires off when traffic to any given CDN PoP exceeds an _Adobe-defined_ request rate per IP address. See [Traffic Filter Rules Alerts](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/traffic-filter-rules-including-waf#traffic-filter-rules-alerts) for more details.

These built-in protections should be considered a baseline for an organization's ability to minimize the performance impact of a DDoS attack. Since each website has different performance characteristics and may see that the performance degradation before the Adobe-defined rate limit is met, it is recommended to extend the default protections through _customer configuration_.

## Extending protection with traffic filter rules

Let's look at some additional, recommended measures that customers can take to protect their websites from DDoS attacks:

- Implement Adobe-recommended [standard traffic filter rules](./traffic-filter-and-waf-rules/use-cases/using-traffic-filter-rules.md) to identify potentially malicious traffic patterns by logging and alerting on suspicious behavior.
- Use the **WAF-DDoS Protection** or **Enhanced Security** add-on and implement Adobe-recommended [WAF Traffic Filter Rules](./traffic-filter-and-waf-rules/use-cases/using-waf-rules.md) to defend against sophisticated attacks, including those using advanced protocol or payload-based techniques.
- Increase cache coverage by configuring [request transformations](./traffic-filter-and-waf-rules/how-to/request-transformation.md) to ignore unnecessary query parameters.

## Get Started

Explore the following tutorials to configure Adobe-recommneded rules to block attacks.

<!-- CARDS
{target = _self}

* ./traffic-filter-and-waf-rules/setup.md
  {title = How to set up traffic filter rules including WAF rules}
  {description = Learn how to set up to create, deploy, test, and analyze the results of traffic filter rules including WAF rules.}
  {image = ./traffic-filter-and-waf-rules/assets/setup/rules-setup.png}
  {cta = Start Now}

* ./traffic-filter-and-waf-rules/use-cases/using-traffic-filter-rules.md
  {title = Protecting AEM websites using standard traffic filter rules}
  {description = Learn how to protect AEM websites from DoS, DDoS and bot abuse using Adobe-recommended standard traffic filter rules in AEM as a Cloud Service.}
  {image = ./traffic-filter-and-waf-rules/assets/use-cases/using-traffic-filter-rules.png}
  {cta = Apply Rules}

* ./traffic-filter-and-waf-rules/use-cases/using-waf-rules.md
  {title = Protecting AEM websites using WAF traffic filter rules}
  {description = Learn how to protect AEM websites from sophisticated threats including DoS, DDoS, and bot abuse using Adobe-recommended Web Application Firewall (WAF) traffic filter rules in AEM as a Cloud Service.}
  {image = ./traffic-filter-and-waf-rules/assets/use-cases/using-waf-rules.png}
  {cta = Activate WAF}

-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="How to set up traffic filter rules including WAF rules">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./traffic-filter-and-waf-rules/setup.md" title="How to set up traffic filter rules including WAF rules" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="./traffic-filter-and-waf-rules/assets/setup/rules-setup.png" alt="How to set up traffic filter rules including WAF rules"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./traffic-filter-and-waf-rules/setup.md" target="_self" rel="referrer" title="How to set up traffic filter rules including WAF rules">How to set up traffic filter rules including WAF rules</a>
                    </p>
                    <p class="is-size-6">Learn how to set up to create, deploy, test, and analyze the results of traffic filter rules including WAF rules.</p>
                </div>
                <a href="./traffic-filter-and-waf-rules/setup.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Start Now</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Protecting AEM websites using standard traffic filter rules">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./traffic-filter-and-waf-rules/use-cases/using-traffic-filter-rules.md" title="Protecting AEM websites using standard traffic filter rules" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="./traffic-filter-and-waf-rules/assets/use-cases/using-traffic-filter-rules.png" alt="Protecting AEM websites using standard traffic filter rules"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./traffic-filter-and-waf-rules/use-cases/using-traffic-filter-rules.md" target="_self" rel="referrer" title="Protecting AEM websites using standard traffic filter rules">Protecting AEM websites using standard traffic filter rules</a>
                    </p>
                    <p class="is-size-6">Learn how to protect AEM websites from DoS, DDoS and bot abuse using Adobe-recommended standard traffic filter rules in AEM as a Cloud Service.</p>
                </div>
                <a href="./traffic-filter-and-waf-rules/use-cases/using-traffic-filter-rules.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Apply Rules</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Protecting AEM websites using WAF traffic filter rules">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="./traffic-filter-and-waf-rules/use-cases/using-waf-rules.md" title="Protecting AEM websites using WAF traffic filter rules" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="./traffic-filter-and-waf-rules/assets/use-cases/using-waf-rules.png" alt="Protecting AEM websites using WAF traffic filter rules"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="./traffic-filter-and-waf-rules/use-cases/using-waf-rules.md" target="_self" rel="referrer" title="Protecting AEM websites using WAF traffic filter rules">Protecting AEM websites using WAF traffic filter rules</a>
                    </p>
                    <p class="is-size-6">Learn how to protect AEM websites from sophisticated threats including DoS, DDoS, and bot abuse using Adobe-recommended Web Application Firewall (WAF) traffic filter rules in AEM as a Cloud Service.</p>
                </div>
                <a href="./traffic-filter-and-waf-rules/use-cases/using-waf-rules.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Activate WAF</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->
