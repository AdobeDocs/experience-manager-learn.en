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