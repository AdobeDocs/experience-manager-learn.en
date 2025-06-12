---
title: AEM Sites Videos and Tutorials
description: Browse videos and tutorials about the features and capabilities of Adobe Experience Manager Sites. AEM Sites is a leading experience management platform.
solution: Experience Manager, Experience Manager Sites
sub-product: Experience Manager Sites
topic: Content Management
doc-type: Catalog
exl-id: cde4ce7f-0afe-4632-8c1c-354586f296d5
---
# AEM Sites videos and tutorials {#overview}

{{edge-delivery-services}}

Adobe Experience Manager (AEM) Sites is a leading experience management platform. This user guide contains videos and tutorials on the many features and capabilities of AEM Sites.

## Three ways to build with AEM Sites

AEM Sites provides three ways to build, author and deliver experiences. Whether you're building full pages, optimizing for edge performance, or powering headless apps, AEM Sites offers flexible options to match your project needs:

1. **Edge Delivery Services** web sites leverage document-based authoring or Adobe Universal Editor to author content, which is then activated, and then delivered to end users by Edge Delivery Services as HTML webpages. This option is primarily for _new and existing projects_ that require high performance, scalability, and speed.
1. **Headless/API-first** web experiences use Content Fragment Editor or Universal Editor to author content, which is then activated, and delivered by AEM Publish as JSON. This option is primarily for _new and existing projects_ that require headless delivery of content to mobile apps, single-page applications (SPAs), or other headless applications.
1. **Traditional AEM** is not the most current approach to builder web experiences using AEM Sites. Traditional AEM uses AEM Author's Page Editor to author content, which is then activated, and delivered to end users by AEM Publish as HTML webpages. Traditional AEM is reccommended for _existing projects_.

These options are designed to meet the diverse needs of marketing organizations, to deliver personalized, engaging experiences at high-speed and scale across any channel or device.

>[!IMPORTANT]
>
> **Edge Delivery Services** is the latest way to build with AEM Sites. It is designed to deliver high-performance websites at scale, leveraging the power of Adobe's Edge Network.

The following diagram illustrates the different paths:

![AEM-Sites-Content-Authoring-and-Experience-Delivery-Paths.png](./assets/aem-sites-authoring-and-experience-delivery-paths.png){width="700" zoomable="yes"}

### Compare the ways to build with AEM Sites

The following table provides a high-level comparison of the three paths. It focuses on the content authoring and experience delivery nuances of each path.

|            |  Edge Delivery Services          | Headless / API-First                        |  Traditional AEM            |
|---------------------|------------------------------|---------------------------------|---------------------------------------------|
| **Best For** |  Websites with high traffic, performance, and scalability needs | Mobile apps, SPAs, and other headless applications | Existing projects (not most current approach) |
| **Authoring Tools** |  Document-based authoring, Universal Editor | Content Fragments, Universal Editor | Page Editor                  |
| **Authored Content Store**         |  Documents or AEM Author (JCR)                       | AEM Author (JCR)          |AEM Author (JCR)    |
| **Delivery** |  Edge Delivery Services                        |    AEM Publish (w/ Adobe CDN + Dispatcher)      | AEM Publish (w/ Adobe CDN + Dispatcher)       |
| **Delivery Content Store**         | Edge Delivery Services  | AEM Publish (JCR)           |  AEM Publish (JCR)    |
| **Delivery Format**   |  HTML                                  | JSON | HTML                    |
| **Development Technology**       |  JavaScript, CSS                | Any (e.g. Swift, React, etc.)        | Java&trade;, JavaScript, CSS    |
| **Implementation Stage** |  New & Existing Projects | New & Existing Projects | Existing Projects Only |

## Tutorials

Learn about each of the three paths to build with AEM Sites through the following tutorials:

<!-- CARDS

* https://www.aem.live/docs/
  {title = Edge Delivery Services - Guides}
  {description = Explore Edge Delivery Services with comprehensive guides. The Build, Publish, and Launch guides cover everything you need to get started with EDS.}
  {image = ./assets/edge-delivery-services.png}
  {target = _blank}
* https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-with-aem-headless/overview
  {title = Headless/API-First - Tutorials}
  {description = Learn how to build headless applications powered by AEM content. Tutorials cover frameworks like iOS, Android, and React—choose what fits your stack.}
  {image = ./assets/headless.png}
  {target = _self}
* https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview
  {title = Traditional AEM - WKND Tutorial}
  {description = Learn how to build a sample AEM Sites project using the WKND tutorial. This guide walks you through project setup, Core Components, Editable Templates, client-side libraries, and component development.}
  {image = ./assets/aem-wknd-spa-editor-tutorial.png}
  {target = _self}
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Edge Delivery Services - Guides">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://www.aem.live/docs/" title="Edge Delivery Services - Guides" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="./assets/edge-delivery-services.png" alt="Edge Delivery Services - Guides"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://www.aem.live/docs/" target="_blank" rel="referrer" title="Edge Delivery Services - Guides">Edge Delivery Services - Guides</a>
                    </p>
                    <p class="is-size-6">Explore Edge Delivery Services with comprehensive guides. The Build, Publish, and Launch guides cover everything you need to get started with EDS.</p>
                </div>
                <a href="https://www.aem.live/docs/" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Learn more</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Headless/API-First - Tutorials">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-with-aem-headless/overview" title="Headless/API-First - Tutorials" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="./assets/headless.png" alt="Headless/API-First - Tutorials"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-with-aem-headless/overview" target="_self" rel="referrer" title="Headless/API-First - Tutorials">Headless/API-First - Tutorials</a>
                    </p>
                    <p class="is-size-6">Learn how to build headless applications powered by AEM content. Tutorials cover frameworks like iOS, Android, and React—choose what fits your stack.</p>
                </div>
                <a href="https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-with-aem-headless/overview" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Learn more</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Traditional AEM - WKND Tutorial">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview" title="Traditional AEM - WKND Tutorial" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="./assets/aem-wknd-spa-editor-tutorial.png" alt="Traditional AEM - WKND Tutorial"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview" target="_self" rel="referrer" title="Traditional AEM - WKND Tutorial">Traditional AEM - WKND Tutorial</a>
                    </p>
                    <p class="is-size-6">Learn how to build a sample AEM Sites project using the WKND tutorial. This guide walks you through project setup, Core Components, Editable Templates, client-side libraries, and component development.</p>
                </div>
                <a href="https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Learn more</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

   
## Additional resources

* [AEM Sites Authoring documentation](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/sites/authoring/essentials/first-steps)
* [AEM Sites Developing documentation](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/developing/introduction/getting-started)
* [AEM Sites Administering documentation](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/sites/administering/home)
* [AEM Sites Deploying documentation](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/introduction/platform)
* [AEM as a Cloud Service tutorials](/help/cloud-service/overview.md)
* [AEM Assets tutorials](/help/assets/overview.md)
* [AEM Forms tutorials](/help/forms/overview.md)
* [AEM Foundation tutorials](/help/foundation/overview.md)
