---
title: Next.js - AEM Headless Example
description: Example applications are a great way to explore the headless capabilities of Adobe Experience Manager (AEM). This Next.js application demonstrates how to query content using AEM's GraphQL APIs using persisted queries.
version: Cloud Service
mini-toc-levels: 1
feature: Content Fragments, GraphQL API
topic: Headless, Content Management
role: Developer
level: Beginner
jira: KT-10721
thumbnail: KT-10721.jpg
last-substantial-update: 2023-05-10
badgeVersions: label="AEM Headless as a Cloud Service" before-title="false"
exl-id: 4f67bb37-416a-49d9-9d7b-06c3573909ca
duration: 303
---
# Next.js App

Example applications are a great way to explore the headless capabilities of Adobe Experience Manager (AEM). This Next.js application demonstrates how to query content using AEM's GraphQL APIs using persisted queries. The AEM Headless Client for JavaScript is used to execute the GraphQL persisted queries that power the app.

![Next.js app with AEM Headless](./assets/next-js/next-js.png)

View the [source code on GitHub](https://github.com/adobe/aem-guides-wknd-graphql/tree/main/next-js)

## Prerequisites {#prerequisites}

The following tools should be installed locally:

+ [Node.js v18](https://nodejs.org/)
+ [Git](https://git-scm.com/)

## AEM requirements

The Next.js app works with the following AEM deployment options. All deployments requires [WKND Shared v3.0.0+](https://github.com/adobe/aem-guides-wknd-shared/releases/latest) or [WKND Site v3.0.0+](https://github.com/adobe/aem-guides-wknd/releases/latest) to be installed on the AEM as a Cloud Service environment.

This example Next.js app is designed to connect to __AEM Publish__ service.

### AEM Author requirements

The Next.js is designed to connect to __AEM Publish__ service, and access unprotected content. The Next.js can be configured to connect to AEM Author via the `.env` properties described below. Images served from AEM Author require authentication, and thus the user accessing the Next.js app must also be logged into AEM Author. 

## How to use

1.  Clone the `adobe/aem-guides-wknd-graphql` repository:

    ```shell
    $ git clone git@github.com:adobe/aem-guides-wknd-graphql.git
    ```
  
1.  Edit the `aem-guides-wknd-graphql/next-js/.env.local` file and set `NEXT_PUBLIC_AEM_HOST` to the AEM service. 

    ```plain
    # AEM service
    NEXT_PUBLIC_AEM_HOST=https://publish-p123-e456.adobeaemcloud.com/
    ...
    ```

    If connecting to AEM Author service, authentication must be provided as AEM Author service is secure by default.

    To use a local AEM account set `AEM_AUTH_METHOD=basic` and provide the user name and password in the `AEM_AUTH_USER` and `AEM_AUTH_PASSWORD` properties.

    ```plain
    ...
    # The variables are not prefixed with NEXT_PUBLIC so they are only available server-side
    AEM_AUTH_METHOD=basic
    AEM_AUTH_USER=aem-user-account 
    AEM_AUTH_PASSWORD=password-for-the-aem-user-account
    ``` 

    To use an [AEM as a Cloud Service local development token](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html#generating-the-access-token) set `AEM_AUTH_METHOD=dev-token` and provide the full dev token value in the `AEM_AUTH_DEV_TOKEN` property.

    ```plain
    ...
    # The variables are not prefixed with NEXT_PUBLIC so they are only available server-side
    AEM_AUTH_METHOD=dev-token
    AEM_AUTH_DEV_TOKEN=my-dev-token
    ``` 

1.  Edit the `aem-guides-wknd-graphql/next-js/.env.local` file and validate  `NEXT_PUBLIC_AEM_GRAPHQL_ENDPOINT` is set to the appropriate AEM GraphQL endpoint. 

    When using [WKND Shared](https://github.com/adobe/aem-guides-wknd-shared/releases/latest) or [WKND Site](https://github.com/adobe/aem-guides-wknd/releases/latest), use the `wknd-shared` GraphQL API endpoint.

    ```plain
    ...
    NEXT_PUBLIC_AEM_GRAPHQL_ENDPOINT=wknd-shared
    ...
    ```

1.  Open a command prompt and start the Next.js app using the following commands:

    ```shell
    $ cd aem-guides-wknd-graphql/next-js
    $ npm install
    $ npm run dev
    ```

1.  A new browser window opens the Next.js app at [http://localhost:3000](http://localhost:3000)
1.  The Next.js app displays a list of adventures. Selecting an adventure opens its details in a new page.

## The code

Below is a summary of how the Next.js app is built, how it connects to AEM Headless to retrieve content using GraphQL persisted queries, and how that data is presented. The full code can be found on [GitHub](https://github.com/adobe/aem-guides-wknd-graphql/tree/main/next-js).

### Persisted queries

Following AEM Headless best practices, the Next.js app uses AEM GraphQL persisted queries to query adventure data. The app uses two persisted queries:

+ `wknd/adventures-all` persisted query, which returns all adventures in AEM with an abridged set of properties. This persisted query drives the initial view's adventure list.

```
# Retrieves a list of all Adventures
#
# Optional query variables:
# - { "offset": 10 }
# - { "limit": 5 }
# - { 
#    "imageFormat": "JPG",
#    "imageWidth": 1600,
#    "imageQuality": 90 
#   }
query ($offset: Int, $limit: Int, $sort: String, $imageFormat: AssetTransformFormat=JPG, $imageWidth: Int=1200, $imageQuality: Int=80) {
  adventureList(
    offset: $offset
    limit: $limit
    sort: $sort
    _assetTransform: {
      format: $imageFormat
      width: $imageWidth
      quality: $imageQuality
      preferWebp: true
  }) {
    items {
      _path
      slug
      title
      activity
      price
      tripLength
      primaryImage {
        ... on ImageRef {
          _path
          _dynamicUrl
        }
      }
    }
  }
}
```

+ `wknd/adventure-by-slug` persisted query, which returns a single adventure by `slug` (a custom property that uniquely identifies an adventure) with a complete set of properties. This persisted query powers the adventure detail views.

```
# Retrieves an Adventure Fragment based on it's unique slug.
#
# Required query variables:
# - {"slug": "bali-surf-camp"}
#
# Optional query variables:
# - { 
#     "imageFormat": "JPG",
#     "imageSeoName": "my-adventure",
#     "imageWidth": 1600,
#     "imageQuality": 90 
#   }
#  
# This query returns an adventure list but since the the slug property is set to be unique in the Content Fragment Model, only a single Content Fragment is expected.

query ($slug: String!, $imageFormat:AssetTransformFormat=JPG, $imageSeoName: String, $imageWidth: Int=1200, $imageQuality: Int=80) {
  adventureList(
    filter: {slug: {_expressions: [{value: $slug}]}}
    _assetTransform: {
      format: $imageFormat
      seoName: $imageSeoName
      width: $imageWidth
      quality: $imageQuality
      preferWebp: true
  }) {
    items {
      _path
      title
      slug
      activity
      adventureType
      price
      tripLength
      groupSize
      difficulty
      price
      primaryImage {
        ... on ImageRef {
          _path
          _dynamicUrl
        }
      }
      description {
        json
        plaintext
        html
      }
      itinerary {
        json
        plaintext
        html
      }
    }
    _references {
      ... on AdventureModel {
        _path
        slug
        title
        price
        __typename
      }
    }
  }
}
```

### Execute GraphQL persisted query

AEM's persisted queries are executed over HTTP GET and thus, the [AEM Headless client for JavaScript](https://github.com/adobe/aem-headless-client-js) is used to [execute the persisted GraphQL queries](https://github.com/adobe/aem-headless-client-js/blob/main/api-reference.md#aemheadlessrunpersistedquerypath-variables-options--promiseany) against AEM and load the adventure content into the app.

Each persisted query has a corresponding function in `src/lib//aem-headless-client.js`, that calls the AEM GraphQL end point, and returns the adventure data.

Each function in turn invokes the `aemHeadlessClient.runPersistedQuery(...)`, executing the persisted GraphQL query.

```js
// src/lib/aem-headless-client.js

...
/**
 * Invokes the 'adventures-all` persisted query using the parameterizable namespace.
 * 
 * @returns a GraphQL response of all adventures.
 */
async getAllAdventures() {
  const queryAdventuresAll = process.env.NEXT_PUBLIC_AEM_GRAPHQL_ENDPOINT + '/adventures-all';
    
  try {
    return await this.aemHeadlessClient.runPersistedQuery(queryAdventuresAll);
  } catch(e) {
    console.error(e)
  }    
}

// And so on, and so forth ... 

async getAdventureSlugs(queryVariables) { ... }

async getAdventuresBySlug(slug, queryVariables) { ... }
...
```

### Pages

The Next.js app uses two pages to present the adventure data.

+   `src/pages/index.js` 

    Uses [Next.js's getServerSideProps()](https://nextjs.org/docs/basic-features/data-fetching/get-server-side-props) to call `getAllAdventures()` and displays each adventure as a card.

    The use of `getServerSiteProps()` allows for Server-Side Rendering of this Next.js page.

+   `src/pages/adventures/[...slug].js` 

    A [Next.js Dynamic Route](https://nextjs.org/docs/routing/dynamic-routes) that displays a single adventure's details. This dynamic route prefetches each adventure's data using [Next.js's getStaticProps()](https://nextjs.org/docs/basic-features/data-fetching/get-static-props) via a call to `getAdventureBySlug(slug, queryVariables)` using the `slug` param passed in via the adventure selection on the `adventures/index.js` page, and `queryVariables` to control the image format, width, and quality.

    The dynamic route is able to pre-fetch the details for all adventures by using [Next.js's getStaticPaths()](https://nextjs.org/docs/basic-features/data-fetching/get-static-paths) and populating all possible route permutations based on the full list of adventures returned by the GraphQL query  `getAdventurePaths()`

    The use of `getStaticPaths()` and `getStaticProps(..)` allowed the Static Site Generation of these Next.js pages.

## Deployment configuration

Next.js apps, especially in the context of Server-side rendering (SSR) and Server-side generation (SSG), do not require advanced security configurations such as Cross-origin Resource Sharing (CORS).

However, if the Next.js does make HTTP requests to AEM from the context of the client, security configurations in AEM may be required. Review the [AEM Headless single-page app deployment tutorial](../deployment/spa.md) for more details.
