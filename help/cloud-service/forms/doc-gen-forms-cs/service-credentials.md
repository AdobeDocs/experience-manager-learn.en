---
title: AEM Forms Service Credentials
description: Download service credentials from AEM's Developer Console.
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Cloud Service
feature: Adaptive Forms
topic: Development
jira: KT-8192
thumbnail: 330519.jpg
exl-id: 74cb8c30-4c41-426c-a1b5-fc595a3167c8
duration: 458
---
# AEM Forms Service Credentials

Integrations with AEM as a Cloud Service must be able to securely authenticate to AEM. AEM's Developer Console generates Service Credentials, which are used by external applications, systems, and services to programmatically interact with AEM Author or Publish services over HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/330519?quality=12&learn=on)

The downloaded service credentials file is stored as a resource file called  service_token.json in the provided eclipse. The values in the service_token file are used to generate the JWT and exchange the JWT for an Access Token. The utility class GetServiceCredentials is used to fetch the property values from the service_token.json resource file.
