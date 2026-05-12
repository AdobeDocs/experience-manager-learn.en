---
title: AEM Forms Service Credentials
description: Download service credentials from AEM's Developer Console.
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
feature: Adaptive Forms
topic: Development
jira: KT-8192
thumbnail: 330519.jpg
exl-id: 74cb8c30-4c41-426c-a1b5-fc595a3167c8
duration: 453
TQID: https://experienceleague.adobe.com/mXEbCriy52iTP84WDujFEP4-1jXuwS3sQQ-hLMXlGjs
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
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
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
---
# AEM Forms Service Credentials

Integrations with AEM as a Cloud Service must be able to securely authenticate to AEM. AEM's Developer Console generates Service Credentials, which are used by external applications, systems, and services to programmatically interact with AEM Author or Publish services over HTTP.

>[!VIDEO](https://video.tv.adobe.com/v/330519?quality=12&learn=on)

The downloaded service credentials file is stored as a resource file called  service_token.json in the provided eclipse. The values in the service_token file are used to generate the JWT and exchange the JWT for an Access Token. The utility class GetServiceCredentials is used to fetch the property values from the service_token.json resource file.
