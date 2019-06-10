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

# Set up Social Posting with Experience Fragments{#set-up-social-posting-with-experience-fragments}

Experience Fragments allow marketers to post experiences created in AEM to social media platforms. The video below details the setup and configuration necessary to publish Experience Fragments to Facebook and Pinterest.

>[!VIDEO](https://video.tv.adobe.com/v/20592/?quality=9)
*[Experience Fragments] - Setup and configuration to social post to Facebook and Pinterest*

## Checklist for configuring AEM Experience Fragments to post to Facebook and Pinterest

* AEM Author Instance is running on HTTPS
* Facebook Account + Facebook Developer App
* Pinterest Account + Pinterest Developer App
* AEM Cloud Services Configuration - Facebook
* AEM Cloud Services Configuration - Pinterest
* AEM Experience Fragment with Cloud Services for Facebook + Pinterest
* Experience Fragment Variation using Facebook Template
* Experience Fragment Variation using Pinterest Template

## Experience Fragment Redirect URI

This URI is used for Facebook and Pinterest apps as part of the Oauth flow.

```plain
 /* replace localhost:8443 with your aem host info */

 https://localhost:8443/libs/cq/experience-fragments/components/redirect
```

>[!NOTE]
>
>The video details the Facebook App set up for v2.10. A previous version of this video had an out-dated Facebook App setup from v2.8.0. If you are receiving the error *"Can't load URL: The domain of this URL isn't included in the app's domains. To be able to load this URL, add all domains and sub-domains of your app to the App Domains field in your app settings.”* checkout the video above 1:30 - 2:30.
