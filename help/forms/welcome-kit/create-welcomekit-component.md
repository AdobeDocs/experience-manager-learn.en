---
title: Create welcome kit component
description: Create an AEM sites page with links to download assets based on submitted form data.
feature: Adaptive Forms
version: 6.5
topic: Development
role: Developer
level: Beginner
last-substantial-update: 2022-12-14
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



