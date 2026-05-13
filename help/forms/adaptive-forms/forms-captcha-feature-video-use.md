---
title: Using CAPTCHAs with AEM Adaptive Forms
description: Adding and using a CAPTCHA with AEM Adaptive Forms.
feature: Adaptive Forms,Workflow
version: Experience Manager 6.4, Experience Manager 6.5
topic: Development
role: Developer
level: Intermediate
exl-id: 7e5dcc6e-fe56-49af-97e3-7dfaa9c8738f
last-substantial-update: 2019-06-09T00:00:00.000Z
duration: 260
TQID: https://experienceleague.adobe.com/MofLw374SkvRkKaetLcNWpQJrd-LhuUfMpKz5m78s9k
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
---
# Using CAPTCHAs with AEM Adaptive Forms{#using-captchas-with-aem-adaptive-forms}

Adding and using a CAPTCHA with AEM Adaptive Forms.

>[!VIDEO](https://video.tv.adobe.com/v/18336?quality=12&learn=on)

*This video walks through the process of adding a CAPTCHA to an AEM Adaptive Form using both the built-in AEM CAPTCHA service as well as Google's reCAPTCHA service.*

>[!NOTE]
>
>This feature is available only with AEM 6.3 onwards.

>[!NOTE]
>
>**To configure reCaptcha on publish instance please follow the steps**
>
>Configure reCaptach on author instance
>
>open the Felix [web console](http://localhost:4502/system/console/bundles) on the author instance
>
>search for com.adobe.granite.crypto.file bundle
>
>Note the bundle id. On my instance it is 20
>
>Navigate to the bundle id on the file system on your author instance 
>
>* &lt;author-aem-install-dir&gt;/crx-quickstart/launchpad/felix/bundle20/data
>* Copy the HMAC and master files
>
>Open the [felix web console](http://localhost:4502/system/console/bundles) on your publish instance. Search for com.adobe.granite.crypto.file bundle. Note the bundle id
>
>Navigate to the bundle id on the file system of your publish instance
>
>* &lt;publish-aem-install-dir&gt;/crx-quickstart/launchpad/felix/bundle20/data
>* delete the exisiting HMAC and master files.
>* paste the HMAC and master files copied from the author intance 
>
>Restart your AEM publish server

## Supporting materials {#supporting-materials}

* [Google reCAPTCHA](https://www.google.com/recaptcha)
