---
title: Set up Social Posting with AEM Experience Fragments
seo-title: Set up Social Posting with AEM Experience Fragments
description: Experience Fragments allow marketers to post experiences created in AEM to social media platforms. The video below details the setup and configuration necessary to publish Experience Fragments to Facebook and Pinterest.
seo-description: Experience Fragments allow marketers to post experiences created in AEM to social media platforms. The video below details the setup and configuration necessary to publish Experience Fragments to Facebook and Pinterest.
uuid: 438a9a88-e68c-47ef-9a5e-f190a8160fc8
products: SG_EXPERIENCEMANAGER/6.3/SITES
topic-tags: authoring
discoiquuid: 164e0afa-568e-4445-a955-bcb93440710c
targetaudience: target-audience advanced
index: y
internal: n
snippet: y
---

# Set up Social Posting with Experience Fragments {#set-up-social-posting-with-experience-fragments}

Experience Fragments allow marketers to post experiences created in AEM to social media platforms. The video below details the setup and configuration necessary to publish Experience Fragments to Facebook and Pinterest.

>[!VIDEO](https://video.tv.adobe.com/v/20592/?quality=9)
*[Experience Fragments] - Setup and configuration to social post to Facebook and Pinterest*

## Checklist for configuring Experience Fragments to post to Facebook and Pinterest

1. AEM Author Instance is running on HTTPS
2. Facebook Account + Facebook Developer App
3. Pinterest Account + Pinterest Developer App
4. AEM Cloud Services Configuration - Facebook
5. AEM Cloud Services Configuration - Pinterest
6. AEM Experience Fragment with Cloud Services for Facebook + Pinterest
7. Experience Fragment Variation using Facebook Template
8. Experience Fragment Variation using Pinterest Template

## Experience Fragment Redirect URI

This URI is used for Facebook and Pinterest apps as part of the Oauth flow.

```plain
 /* replace localhost:8443 with your aem host info */

 https://localhost:8443/libs/cq/experience-fragments/components/redirect
```

