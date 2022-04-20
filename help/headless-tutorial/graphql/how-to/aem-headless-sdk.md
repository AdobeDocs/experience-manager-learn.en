---
title: Using the AEM Headless SDK
description: Learn how to make GraphQL queries using the AEM Headless SDK.
version: Cloud Service
topic: Headless
feature: GraphQL API
role: Developer
level: Intermediate
kt: 10269
thumbnail: KT-10269.jpeg
exl-id: 922a464a-2286-4132-9af8-f5a1fb5ce268
---
# AEM Headless SDK

The AEM Headless SDK is set of libraries that can be used by clients to quickly and easily interact with AEM Headless APIs over HTTP.

 The AEM Headless SDK is available for various platforms:

+ [AEM Headless SDK for client-side browsers (JavaScript)](https://github.com/adobe/aem-headless-client-js)
+ [AEM Headless SDK for server-side/Node.js (JavaScript)](https://github.com/adobe/aem-headless-client-nodejs)
+ [AEM Headless SDK for Java™](https://github.com/adobe/aem-headless-client-java)

## GraphQL queries

Querying AEM using GraphQL using queries (as opposed to [persisted GraphQL queries](#persisted-graphql-queries)) allows developers to define queries in code, specifying exactly what content to request from AEM.

GraphQL queries tend to be less performant than persisted queries, as they are executed using HTTP POST, which is less cache-able at the CDN and AEM Dispatcher tiers.

### Code examples{#graphql-queries-code-examples}

The following are code examples of how to execute a GraphQL query against AEM. 

+++ JavaScript example

Install the [@adobe/aem-headless-client-js](https://github.com/adobe/aem-headless-client-js) by running the `npm install` command from the root of your Node.js project.

```
$ npm i @adobe/aem-headless-client-js
```

This code example shows how to query AEM using the [@adobe/aem-headless-client-js](https://github.com/adobe/aem-headless-client-js) npm module using `async/await` syntax. The AEM Headless SDK for JavaScript also supports [Promise syntax](https://github.com/adobe/aem-headless-client-js#use-aemheadless-client).

```javascript
import AEMHeadless from '@adobe/aem-headless-client-js';

// Initialize the AEMHeadless client with connection details
const aemHeadlessClient = new AEMHeadless({
    serviceURL: 'https://publish-p123-e789.adobeaemcloud.com',  // The AEM environment to query, this can be pulled out to env variables
    endpoint: '/content/cq:graphql/wknd/endpoint.json',         // The AEM GraphQL endpoint, this can be pulled out to env variables
})

async function fetchQuery(query, queryParams) {
    let data

    try {
        // AEM GraphQL queries are asynchronous, either await their return or use Promise-based .then(..) { ... } syntax
        const response = await aemHeadlessClient.runQuery(query, queryParams);
        // The GraphQL data is stored on the response's data key
        data = response.data;
    } catch (e) {
        console.error(e.toJSON())
    }

    return data;
};

// Define the GraphQL query in-code
const adventureNamesQuery = `{
    adventuresList {
        items {
            adventureName
        }
    }
}`;

let data = fetchQuery(adventureNamesQuery);
```

+++


+++ React useEffect(..) example

Install the [@adobe/aem-headless-client-js](https://github.com/adobe/aem-headless-client-js) by running the `npm install` command from the root of your React project.

```
$ npm i @adobe/aem-headless-client-js
```

This code example shows how to use the [React useEffect(..) hook](https://reactjs.org/docs/hooks-effect.html) to execute an asynchronous call to AEM GraphQL.

Using `useEffect` to make the asynchronous GraphQL call in React is useful because it:

1. Provides synchronous wrapper for the asynchronous call to AEM.
1. Reduces unnecessarily requerying AEM.

```javascript
// src/useGraphQL.js

import { useState, useEffect } from 'react';
import AEMHeadless from '@adobe/aem-headless-client-js';

const aemHeadlessClient = new AEMHeadless({
    serviceURL: 'https://publish-p123-e789.adobeaemcloud.com', // The AEM environment to query, this can be pulled out to env variables
    endpoint: '/content/cq:graphql/global/endpoint.json'       // The AEM GraphQL endpoint, this can be pulled out to env variables
});

export function useGraphQL(query, queryParams) {
    let [data, setData] = useState(null);
    let [errors, setErrors] = useState(null);
  
    useEffect(() => {
        async function fetchData() {
            try {
                const response = await aemHeadlessClient.runQuery(query, queryParams);
                setData(response.data);
            } catch(error) {
                setErrors(error);
            };
        }
        fetchData();
    }, [query, queryParams]);
  
    return { data, errors }
}
```

Import and use the `useGraphQL` hook in the React component to query AEM.

```javascript
import useGraphQL from 'useGraphQL';

const adventuresQuery = `{
    adventuresList {
        items {
            adventureName
        }
    }
}`;

let { data, errors } = useGraphQL(adventuresQuery);
```

+++

<p>&nbsp;</p>

## Persisted GraphQL queries

Querying AEM using GraphQL using persisted queries (as opposed to [regular GraphQL queries](#graphl-queries)) allows developers to persist a query (but not its results) in AEM, and then request the query to be executed by name. Persisted queries is similar to the concept of stored procedures in SQL databases. 

Persisted queries tend to be more performant than regular GraphQL queries, as persisted queries are executed using HTTP GET, which is more cache-able at the CDN and AEM Dispatcher tiers. Persisted queries also in effect, define an API, and decouple the need for the developer to understand the details of each Content Fragment Model.

### Code examples{#persisted-graphql-queries-code-examples}

The following are code examples of how to execute a GraphQL persisted query against AEM. 

+++ JavaScript example

Install the [@adobe/aem-headless-client-js](https://github.com/adobe/aem-headless-client-js) by running the `npm install` command from the root of your Node.js project.

```
$ npm i @adobe/aem-headless-client-js
```

This code example shows how to query AEM using the [@adobe/aem-headless-client-js](https://github.com/adobe/aem-headless-client-js) npm module using `async/await` syntax. The AEM Headless SDK for JavaScript also supports [Promise syntax](https://github.com/adobe/aem-headless-client-js#use-aemheadless-client).

This code assumes a persisted query with the name `wknd/adventureNames` has been created on AEM Author and published to AEM Publish.

```javascript
import AEMHeadless from '@adobe/aem-headless-client-js';

// Initialize the AEMHeadless client with connection details
const aemHeadlessClient = new AEMHeadless({
    serviceURL: 'https://publish-p123-e789.adobeaemcloud.com',  // The AEM environment to query, this can be pulled out to env variables
    endpoint: '/content/cq:graphql/wknd/endpoint.json',         // The AEM GraphQL endpoint, this can be pulled out to env variables
})

async function fetchPersistedQuery(persistedQueryName) {
    let data

    try {
        // AEM GraphQL queries are asynchronous, either await their return or use Promise-based .then(..) { ... } syntax
        const response = await aemHeadlessClient.runPersistedQuery(persistedQueryName);
        // The GraphQL data is stored on the response's data field
        data = response.data;
    } catch (e) {
        console.error(e.toJSON())
    }

    return data;
};

// Execute the persisted query using its name
let data = fetchPersistedQuery('wknd/adventureNames');
```

+++

+++ React useEffect(..) example

Install the [@adobe/aem-headless-client-js](https://github.com/adobe/aem-headless-client-js) by running the `npm install` command from the root of your React project.

```
$ npm i @adobe/aem-headless-client-js
```

This code example shows how to use the [React useEffect(..) hook](https://reactjs.org/docs/hooks-effect.html) to execute an asynchronous call to AEM GraphQL.

Using `useEffect` to make the asynchronous GraphQL call in React is useful because:

1. It provides synchronous wrapper for the asynchronous call to AEM.
1. It reduces unnecessarily requerying AEM.

This code assumes a persisted query with the name `wknd/adventureNames` has been created on AEM Author and published to AEM Publish.

```javascript
import AEMHeadless from '@adobe/aem-headless-client-js';

// Initialize the AEMHeadless client with connection details
const aemHeadlessClient = new AEMHeadless({
    serviceURL: 'https://publish-p123-e789.adobeaemcloud.com', // The AEM environment to query
    endpoint: '/content/cq:graphql/wknd/endpoint.json'         // The AEM GraphQL endpoint
})

export function fetchPersistedQuery(persistedQueryName) {
  let [data, setData] = useState(null);
  let [errors, setErrors] = useState(null);

  useEffect(async () => {
    try {
        // AEM GraphQL queries are asynchronous, either await their return or use Promise-based .then(..) { ... } syntax 
        const response = await aemHeadlessClient.runPersistedQuery(persistedQueryName);
        // The GraphQL data is stored on the response's data field
        setData(response.data);
    }.catch((error) => {
        setErrors(error);
    });

  }, [persistedQueryName]);

  return { data, errors }
}
```

And invoke this code from elsewhere in the React code.

```javascript
import useGraphL from '...';

let { data, errors } = fetchPersistedQuery('wknd/adventureNames');
```

+++

<p>&nbsp;</p>
