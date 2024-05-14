---
title: Server-to-server Node.js app - AEM Headless Example
description: Example applications are a great way to explore the headless capabilities of Adobe Experience Manager (AEM). This server-side Node.js application demonstrates how to query content using AEM's GraphQL APIs using persisted queries.
version: Cloud Service
feature: Content Fragments, GraphQL API
topic: Headless, Content Management
role: Developer
level: Beginner
jira: KT-10798
thumbnail: KT-10798.jpg
last-substantial-update: 2023-05-10
badgeVersions: label="AEM Headless as a Cloud Service" before-title="false"
exl-id: 39b21a29-a75f-4a6c-ba82-377cf5cc1726
duration: 135
---
# Server-to-server Node.js app

Example applications are a great way to explore the headless capabilities of Adobe Experience Manager (AEM). This server-to-server application demonstrates how to query content using AEM's GraphQL APIs using persisted queries and print it on terminal.

![Server-to-server Node.js app with AEM Headless](./assets/server-to-server-app/server-to-server-app.png)

View the [source code on GitHub](https://github.com/adobe/aem-guides-wknd-graphql/tree/main/server-to-server)

## Prerequisites {#prerequisites}

The following tools should be installed locally:

+ [Node.js v18](https://nodejs.org/en)
+ [Git](https://git-scm.com/)

## AEM requirements

The Node.js application works with the following AEM deployment options. All deployments requires the [WKND Site v3.0.0+](https://github.com/adobe/aem-guides-wknd/releases/latest) to be installed.

+ [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html)
+ Optionally, [service credentials](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html) if authorizing requests (for example, connecting to AEM Author service).

This Node.js application can connect to AEM Author or AEM Publish based on the command-line parameters.

## How to use

1. Clone the `adobe/aem-guides-wknd-graphql` repository:

    ```shell
    $ git clone git@github.com:adobe/aem-guides-wknd-graphql.git
    ```

1. Open a terminal and run the commands:

    ```shell
    $ cd aem-guides-wknd-graphql/server-to-server-app
    $ npm install
    ```

1. The app can be run using the command: 

    ```
    $ node index.js <AEM_HOST> <OPTIONAL_SERVICE_CONFIG_FILE_PATH>
    ```

    For example, to run the app against AEM Publish without authorization:

    ```shell
    $ node index.js https://publish-p123-e789.adobeaemcloud.com
    ```

    To run the app against AEM Author with authorization:

    ```shell
    $ node index.js https://author-p123-e456.adobeaemcloud.com ./service-config.json
    ```

1. A JSON list of adventures from the WKND reference site should print in the terminal.

## The code

Below is a summary of how the server-to-server Node.js application is built, how it connects to AEM Headless to retrieve content using GraphQL persisted queries, and how that data is presented. The full code can be found on [GitHub](https://github.com/adobe/aem-guides-wknd-graphql/tree/main/server-to-server).

The common use case for server-to-server AEM Headless apps is to sync Content Fragment data from AEM into other systems, however this application is intentionally simple, and prints the JSON results from the persisted query. 

### Persisted queries

Following AEM Headless best practices, the application uses AEM GraphQL persisted queries to query adventure data. The application uses two persisted queries:

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

### Create AEM Headless client

```javascript
const { AEMHeadless, getToken } = require('@adobe/aem-headless-client-nodejs');

async function run() { 

    // Parse the AEM host, and optional service credentials from the command line arguments
    const args = process.argv.slice(2);
    const aemHost = args.length > 0 ? args[0] : null;                // Example: https://author-p123-e456.adobeaemcloud.com
    const serviceCredentialsFile = args.length > 1 ? args[1] : null; // Example: ./service-config.json

    // If service credentials are provided via command line argument,
    // use `getToken(..)` to exchange them with Adobe IMS for an AEM access token 
    let accessToken;
    if (serviceCredentialsFile) {
        accessToken = (await getToken(serviceCredentialsFile)).accessToken;
    }

    // Instantiate withe AEM Headless client to query AEM GraphQL APIs
    // The endpoint is left blank since only persisted queries should be used to query AEM's GraphQL APIs
    const aemHeadlessClient = new AEMHeadless({
        serviceURL: aemHost,
        endpoint: '',           // Avoid non-persisted queries
        auth: accessToken       // accessToken only set if the 2nd command line parameter is set
    })
    ...
}
```


### Execute GraphQL persisted query

AEM's persisted queries are executed over HTTP GET and thus, the [AEM Headless client for Node.js](https://github.com/adobe/aem-headless-client-nodejs) is used to [execute the persisted GraphQL queries](https://github.com/adobe/aem-headless-client-nodejs#within-asyncawait) against AEM and retrieves the adventure content.

The persisted query is invoked by calling `aemHeadlessClient.runPersistedQuery(...)`, and passing the persisted GraphQL query name. Once the GraphQL returns the data, pass it to the simplified `doSomethingWithDataFromAEM(..)` function, which prints the results - but typically would send the data to another system, or generate some output based on the retrieved data.

```js
// index.js

async function run() { 
    ...
    try {
        // Retrieve the data from AEM GraphQL APIs
        data = await aemHeadlessClient.runPersistedQuery('wknd-shared/adventures-all')
        
        // Do something with the data from AEM. 
        // A common use case is sending the data to another system.
        await doSomethingWithDataFromAEM(data);
    } catch (e) {
        console.error(e.toJSON())
    }
}
```
