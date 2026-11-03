---
title: Create welcome kit component
description: Create an AEM sites page with links to download assets based on submitted form data.
feature: Adaptive Forms
version: Experience Manager 6.5
topic: Development
role: Developer
level: Beginner
last-substantial-update: 2022-12-14T00:00:00.000Z
exl-id: 66496f0e-c121-4b6d-b371-084393ece3ca
duration: 20
TQID: 'https://experienceleague.adobe.com/VN2JO2z5KNs1ttxuekmRuFNmUwyGufPYWdw2YJtCylQ'
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Welcome kit component

A page component was created to list the assets in the page that can be downloaded by the end user. The paths to the individual assets are saved in a property called **paths**. The submitted form data determines the assets to be included.

The following code lists the assets on the page:

```html
   <p class="cmp-press-kit__press-kit-size">
        Welcome kit contains ${pressKit.assets.size} assets.
    </p>
<ul class="cmp-press-kit__asset-list" data-sly-list.asset="${pressKit.assets}">
    <li class="cmp-press-kit__asset-item">
        <div class="cmp-press-kit__asset " >
            <div class="cmp-press-kit__asset-content">
                <img class="cmp-press-kit__asset-image" src="${asset.path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png" alt="${asset.name}"/>
                <p class="cmp-press-kit__asset-title">${asset.title}</p>
            </div>
            <div class="cmp-press-kit__asset-actions">
                <a class="cmp-press-kit__asset-download-button" href="${asset.path}">Download</a>
            </div>
        </div>
    </li>
</ul>
</sly>
<sly data-sly-call="${placeholderTemplate.placeholder @ isEmpty=!ready}"></sly>

```
