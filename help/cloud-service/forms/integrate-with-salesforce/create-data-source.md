---
title: Create a cloud services configuration
description: Create data source to connect to Salesforce using the OAuth credentials
solution: Experience Manager, Experience Manager Forms
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
topic: Development
feature: Adaptive Forms, Integrations
jira: KT-7148
thumbnail: 331755.jpg
exl-id: e2d56e91-c13e-4787-a97f-255938b5d290
duration: 173
TQID: https://experienceleague.adobe.com/IyqVjF-K2-GOLAAtqCNfCFyrZqJaKcXoJGnpkJ41-4g
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a1df6763-63b5-45b4-8c8a-155a692a2b3e
    internal-label: Integrations
  - id: ae478996-b206-4712-9b0c-dc78a2644453
    internal-label: Integrations
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Create Data Source

Create a REST backed data source using the swagger file created in the earlier step.

>[!VIDEO](https://video.tv.adobe.com/v/331755?quality=12&learn=on)

| Setting             | Value                                                           |
|---------------------|-----------------------------------------------------------------|
| OAuth URL           | https://login.salesforce.com/services/oauth2/authorize          |
| Authorization Scope | api chatter_api full id openid refresh_token visualforce web    |
| Refresh Token URL   | https://newfocus-dev-ed.my.salesforce.com/services/oauth2/token |
| Access Token URL    | https://newfocus-dev-ed.my.salesforce.com/services/oauth2/token |


**The Refresh and Access Token URL's domain names will have to change to match your Salesforce account settings**