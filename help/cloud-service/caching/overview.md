---
title: AEM as a Cloud Service caching
description: General overview of AEM as a Cloud Service caching.
version: Experience Manager as a Cloud Service
feature: Dispatcher, Developer Tools
topic: Performance
role: Architect, Developer
level: Intermediate
doc-type: Article
last-substantial-update: 2023-08-28
jira: KT-13858
thumbnail: KT-13858.jpeg
exl-id: e76ed4c5-3220-4274-a315-a75e549f8b40
duration: 36
---
# AEM as a Cloud Service caching

In AEM as a Cloud Service, understanding caching is crucial. Caching involves storing and reusing previously fetched data to enhance system efficiency and reduce load times. This mechanism significantly accelerates content delivery, boosts website performance, and optimizes user experience.

AEM as a Cloud Service has multiple caching layers, and strategies that differ between the Author and Publish services. 

![AEM as a Cloud Service caching overview](./assets/overview/all.png){align="center"} 

## AEM caching

AEM as a Cloud Service has a robust, configurable multi-layer caching strategy, including a CDN, AEM Dispatcher, and optionally a customer managed CDN. Caching across layers can be fine-tuned to optimize performance, ensuring AEM only delivers the best experiences. AEM has different caching concerns for the Author and Publish services. Explore the caching strategies for each service below.


<div class="columns is-multiline" style="margin-top: 2rem">
    <div class="column is-half-tablet is-half-desktop is-half-widescreen" aria-label="AEM Publish service caching">
    <div class="card is-padded-small is-padded-big-mobile" style="height: 100%">
        <div class="card-image">
          <figure class="image is-16by9">
            <a href="./publish.md" title="AEM Publish service" tabindex="-1">
              <img class="is-bordered-r-small" src="./assets/overview/publish-card.png" alt="AEM Publish service caching">
            </a>
          </figure>
        </div>
        <div class="card-content is-padded-small">
          <div class="content">
            <p class="headline is-size-6 has-text-weight-bold"><a href="./publish.md" title="AEM Publish service caching">AEM Publish service caching</a></p>
            <p class="is-size-6">AEM Publish service uses a managed CDN and AEM Dispatcher to optimize end-user web experiences.</p>
            <a href="./publish.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
              <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Learn</span>
            </a>
          </div>
        </div>
      </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-half-widescreen" aria-label="AEM Author service caching">
        <div class="card is-padded-small is-padded-big-mobile" style="height: 100%">
            <div class="card-image">
            <figure class="image is-16by9">
                <a href="./author.md" title="AEM Author service caching" tabindex="-1">
                <img class="is-bordered-r-small" src="./assets/overview/author-card.png" alt="AEM Author service caching">
                </a>
            </figure>
            </div>
            <div class="card-content is-padded-small">
            <div class="content">
                <p class="headline is-size-6 has-text-weight-bold"><a href="./author.md" title="AEM Author service caching">AEM Author service caching</a></p>
                <p class="is-size-6">AEM Author service uses a managed CDN to provide optimized authoring experiences.</p>
                <a href="./author.md" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM">
                <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Learn</span>
                </a>
            </div>
            </div>
        </div>
    </div>
</div>
