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
+ [AEM Headless SDK for Java&trade;](https://github.com/adobe/aem-headless-client-java)

## Persisted GraphQL queries

Querying AEM using GraphQL using persisted queries (as opposed to [client-defined GraphQL queries](#graphl-queries)) allows developers to persist a query (but not its results) in AEM, and then request the query to be executed by name. Persisted queries are similar to the concept of stored procedures in SQL databases. 

Persisted queries are more performant than client-defined GraphQL queries, as persisted queries are executed using HTTP GET, which is cache-able at the CDN and AEM Dispatcher tiers. Persisted queries also in effect, define an API, and decouple the need for the developer to understand the details of each Content Fragment Model.

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
    endpoint: '/content/cq:graphql/wknd-shared/endpoint.json',  // The AEM GraphQL endpoint, this is not used when invoking persisted queries.
})

/**
 * Uses the AEM Headless SDK to execute a persisted query with optional query variables.

 * @param {String} persistedQueryName the fully qualified name of the persisted query
 * @param {*} queryParameters an optional JavaScript object containing query parameters
 * @returns the GraphQL data or an error message 
 */
export async function executePersistedQuery(persistedQueryName, queryParameters) {
    let data;
    let errors;

    try {
        // AEM GraphQL queries are asynchronous, either await their return or use Promise-based .then(..) { ... } syntax
        const response = await aemHeadlessClient.runPersistedQuery(persistedQueryName, queryParameters);
        // The GraphQL data is stored on the response's data field
        data = response.data;
    } catch (e) {
        console.error(e.toJSON())
        errors = e;
    }

    return { data, errors };
};

// Execute the persisted query using its name 'wknd-shared/adventures-by-slug' and optional query variables
let { data, errors } = executePersistedQuery('wknd-shared/adventures-by-slug', { "slug": "bali-surf-camp" });
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

This code assumes a persisted query with the name `wknd-shared/adventure-by-slug` has been created on AEM Author and published to AEM Publish using GraphiQL.

```javascript
import AEMHeadless from '@adobe/aem-headless-client-js';
import { useEffect, useState } from "react";

// Initialize the AEMHeadless client with connection details
const aemHeadlessClient = new AEMHeadless({
    serviceURL: 'https://publish-p123-e789.adobeaemcloud.com', // The AEM environment to query
    endpoint: '/content/cq:graphql/wknd-shared/endpoint.json'         // The AEM GraphQL endpoint, this is not used when invoking persisted queries.
})

/**
 * Private, shared function that invokes the AEM Headless client. 
 * React components/views will invoke GraphQL via the custom React useEffect hooks defined below.
 * 
 * @param {String} persistedQueryName the fully qualified name of the persisted query
 * @param {*} queryParameters an optional JavaScript object containing query parameters
 * @returns the GraphQL data or an error message 
 */
async function fetchPersistedQuery(persistedQueryName, queryParameters) {
  let data;
  let err;

  try {
    // AEM GraphQL queries are asynchronous, either await their return or use Promise-based .then(..) { ... } syntax
    const response = await aemHeadlessClient.runPersistedQuery(
      persistedQueryName,
      queryParameters
    );
    // The GraphQL data is stored on the response's data field
    data = response?.data;
  } catch (e) {
    // An error occurred, return the error messages
    err = e
      .toJSON()
      ?.map((error) => error.message)
      ?.join(", ");
    console.error(e.toJSON());
  }

  return { data, err };
}

/**
 * Calls the 'wknd-shared/adventure-by-slug' and provided the {slug} as the persisted query's `slug` parameter.
 *
 * @param {String!} slug the unique slug used to specify the adventure to return
 * @returns a JSON object representing the adventure
 */
export function useAdventureBySlug(slug) {
  const [adventure, setAdventure] = useState(null);
  const [errors, setErrors] = useState(null);

  useEffect(() => {
    async function fetchData() {
      // The key is the variable name as defined in the persisted query, and may not match the model's field name
      const queryParameters = { slug: slug };
      
      // Invoke the persisted query, and pass in the queryParameters object as the 2nd parameter
      const { data, err } = await fetchPersistedQuery(
        "wknd-shared/adventure-by-slug",
        queryParameters
      );

      if (err) {
        // Capture errors from the HTTP request
        setErrors(err);
      } else if (data?.adventureList?.items?.length === 1) {
        // Set the adventure data after data validation (there should only be 1 matching adventure)
        setAdventure(data.adventureList.items[0]);
      } else {
        // Set an error if no adventure could be found
        setErrors(`Cannot find adventure with slug: ${slug}`);
      }
    }
    fetchData();
  }, [slug]);

  return { adventure, errors };
}
```

Invoke the custom React `useEffect` hook from elsewhere in a React component.

```javascript
import useAdventureBySlug from '...';

let { data, errors } = useAdventureBySlug('bali-surf-camp');
```

New `useEffect` hooks can be created for each persisted query the React app uses.

+++

<p>&nbsp;</p>

## GraphQL queries

AEM supports client-defined GraphQL queries, however it is AEM best practice to use [persisted GraphQL queries](#persisted-graphql-queries).

