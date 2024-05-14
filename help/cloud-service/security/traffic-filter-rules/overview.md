---
title: Protecting websites with traffic filter rules (including WAF rules)
description: Learn about Traffic Filter rules, including its subcategory of Web Application Firewall (WAF) rules. How to create, deploy, and test the rules. Also, analyze the results to protect your AEM sites.
version: Cloud Service
feature: Security
topic: Security, Administration, Architecture
role: Admin, Architect
level: Intermediate
doc-type: Tutorial
last-substantial-update: 2023-10-26
jira: KT-13148
thumbnail: KT-13148.jpeg
exl-id: e6d67204-2f76-441c-a178-a34798fe266d
duration: 165
---
# Protecting websites with traffic filter rules (including WAF rules)

Learn about **traffic filter rules**, including its subcategory of **Web Application Firewall (WAF) rules** in AEM as a Cloud Service (AEMCS). Read about how to create, deploy, and test the rules. Also, analyze the results to protect your AEM sites.

>[!VIDEO](https://video.tv.adobe.com/v/3425401?quality=12&learn=on)

## Overview

Reducing the risk of security breaches is a top priority for any organization. AEMCS offers the traffic filter rules feature, including WAF rules, to safeguard websites and applications.

Traffic filter rules are deployed to the [built-in CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html) and are evaluated before the request reaches the AEM infrastructure. With this feature, you can significantly enhance the security of your website, ensuring that only legitimate requests are allowed to access the AEM infrastructure.

This tutorial guides you through the process of creating, deploying, testing, and analyzing the results of traffic filter rules, including WAF rules. 

You can read more about traffic filter rules in [this article](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/traffic-filter-rules-including-waf.html?lang=en).

>[!IMPORTANT]
>
> A subcategory of traffic filter rules called "WAF rules" require a WAF-DDoS Protection or Enhanced Security license.

We invite you to give feedback or ask questions about traffic filter rules by emailing **aemcs-waf-adopter@adobe.com**.

## Next step

Learn [how to set up](./how-to-setup.md) the feature so you can create, deploy, and test traffic filter rules. Read about setting up the **Elasticsearch, Logstash, and Kibana (ELK)** stack dashboard tooling to analyze the results of your AEMCS CDN logs.


