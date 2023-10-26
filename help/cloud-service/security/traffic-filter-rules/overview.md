---
title: Protecting websites with traffic filter rules (including WAF rules)
description: Learn about Traffic Filter rules, including its subcategory of Web Application Firewall (WAF) rules. How to create, deploy, and test the rules. Also, analyze the results to protect your AEM sites.
version: Cloud Service
feature: Security
topic: Security, Administration, Architecture
role: Admin, Architect
level: Intermediate
doc-type: Tutorial
last-substantial-update: 2023-10-20
jira: KT-13148
thumbnail: KT-13148.jpeg
---

# Protecting websites with traffic filter rules (including WAF rules)

Learn about **Traffic Filter rules**, including its subcategory of **Web Application Firewall (WAF) rules** in AEM as a Cloud Service (AEMCS). Read about how to create, deploy, and test the rules. Also, analyze the results to protect your AEM sites.

## Overview

Reducing the risk of security breaches is a top priority for any organization. AEMCS offers the Traffic Filter rules feature, including WAF rules, to safeguard websites and applications.

Traffic Filter rules are deployed to the [built-in CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html) and are evaluated before the request reaches the AEM infrastructure. With this feature, you can significantly enhance the security of your website, ensuring that only legitimate requests are allowed to access the AEM infrastructure.

This tutorial guides you through the process of creating, deploying, testing, and analyzing the results of Traffic Filter rules, including WAF rules.

>[!IMPORTANT]
>
> Subcategory of Traffic Filter rules called "WAF rules" require a WAF-DDoS Protection license


## Next step

Learn [how to set up](./how-to-setup.md) the feature so you can create, deploy, and test Traffic Filter rules. Read about setting up the **Elasticsearch, Logstash, and Kibana (ELK)** stack dashboard tooling to analyze the results of your AEMCS CDN logs.



