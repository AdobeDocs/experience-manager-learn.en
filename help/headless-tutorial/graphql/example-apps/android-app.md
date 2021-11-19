---
title: Android App - AEM Headless Example
description: Example applications are a great way to explore the headless capabilities of Adobe Experience Manager (AEM). An Android application is provided that demonstrates how to query content using the GraphQL APIs of AEM. The Apollo Client Android is used to generate the GraphQL queries and map data to Swift objects to power the app. SwiftUI is used to render a simple list and detail view of the content.
version: Cloud Service
mini-toc-levels: 1
kt: 9166
thumbnail: KT-9166.jpg
feature: Content Fragments, GraphQL API
topic: Headless, Content Management
role: Developer
level: Beginner
exl-id: 7873e263-b05a-4170-87a9-59e8b7c65faa
---
# Android App

Example applications are a great way to explore the headless capabilities of Adobe Experience Manager (AEM). An Android application is provided that demonstrates how to query content using the GraphQL APIs of AEM. The [AEM Headless Client for Java](https://github.com/adobe/aem-headless-client-java) is used to execute the GraphQL queries and map data to Java objects to power the app.

View the [source code on GitHub](https://github.com/adobe/aem-guides-wknd-graphql/tree/main/android-app)

>[!VIDEO](https://video.tv.adobe.com/v/338093/?quality=12&learn=on)

## Prerequisites {#prerequisites}

The following tools should be installed locally:

* [Android Studio](https://developer.android.com/studio)
* [Git](https://git-scm.com/)

## AEM Requirements

The application is designed to connect to an AEM **Publish** environment with the latest release of the [WKND Reference site](https://github.com/adobe/aem-guides-wknd/releases/latest) installed.

* [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html)
* [AEM 6.5.10+](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/new-features-latest-service-pack.html)

We recommend [deploying the WKND Reference site to a Cloud Service environment](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#coding-against-the-right-aem-version). A local setup using [the AEM Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) or [AEM 6.5 QuickStart jar](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html?lang=en#install-local-aem-instances) can also be used.

## How to use

1. Clone the `aem-guides-wknd-graphql` repository:

    ```shell
    git clone git@github.com:adobe/aem-guides-wknd-graphql.git
    ```

1. Launch [Android Studio](https://developer.android.com/studio) and open the folder `android-app`
1. Modify the file `config.properties` at `app/src/main/assets/config.properties` and update `contentApi.endpoint` to match your target AEM environment:
    
    ```plain
    contentApi.endpoint=http://10.0.2.2:4502
    contentApi.user=admin
    contentApi.password=admin
    ```

1. Download an [Android Virtual Device](https://developer.android.com/studio/run/managing-avds) (min API 28)
1. Build and deploy the app using the Android emulator.


### Connecting to AEM environments

`10.0.2.2` is a [special alias](https://developer.android.com/studio/run/emulator-networking) for localhost when using the emulator. So `10.0.2.2:4502` is equivalent to `localhost:4502`. If connecting to an AEM publish environment (recommended), no authorization is required and `contentAPi.user` and `contentApi.password` can be left blank. 

If connecting to an AEM author environment [authorization](https://github.com/adobe/aem-headless-client-java#using-authorization) is required. By default the application is set up to use basic authentication with a username and password of `admin:admin`. The [AEMHeadlessClientBuilder](https://github.com/adobe/aem-headless-client-java/blob/main/client/src/main/java/com/adobe/aem/graphql/client/AEMHeadlessClientBuilder.java) provides the ability to use [token-based authentication](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html). To use token-based authentication update client builder in `AdventureLoader.java` and `AdventuresLoader.java`:

  ```java
  /* Comment out basicAuth
   if (user != null && password != null) {
     builder.basicAuth(user, password);
    }
  */
  
  // use token-authentication where `token` is a String representing the token
  builder.tokenAuth(token)
  ```

## The code

Below is a brief summary of the important files and code used to power the application. The full code can be found on [GitHub](https://github.com/adobe/aem-guides-wknd-graphql/tree/main/android-app).

### Fetching Content

The [AEM Headless Client for Java](https://github.com/adobe/aem-headless-client-java) is used by the app to execute the GraphQL query against AEM and load the adventure content into the app.

`AdventuresLoader.java` is the file that fetches and loads the initial list of Adventures on the home screen of the application. It makes use of [Persisted Queries](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/video-series/graphql-persisted-queries.html) which is [pre-packaged](https://github.com/adobe/aem-guides-wknd/tree/master/ui.content/src/main/content/jcr_root/conf/wknd/settings/graphql/persistentQueries/adventures-all/_jcr_content) with the WKND reference site. The endpoint is `/wknd/adventures-all`. `AEMHeadlessClientBuilder` instantiates a new instance based on the api endpoint set in `config.properties`.

```java
//AdventuresLoader.java

public static final String PERSISTED_QUERY_NAME = "/wknd/adventures-all";
...
AEMHeadlessClientBuilder builder = AEMHeadlessClient.builder().endpoint(config.getContentApiEndpoint());
// optional authentication for basic auth
String user = config.getContentApiUser();
String password = config.getContentApiPassword();
if (user != null && password != null) {
    builder.basicAuth(user, password);
}

AEMHeadlessClient client = builder.build();
// run a persistent query and get a response
GraphQlResponse response = client.runPersistedQuery(PERSISTED_QUERY_NAME);
```

`AdventureLoader.java` is the file that fetches and loads the Adventure content for each of the detail views. Again the `AEMHeadlessClient` is used to execute the query. A regular graphQL query is executed based on the path to the Adventure content fragment. The query is maintained in a separate file named [adventureByPath.query](https://github.com/adobe/aem-guides-wknd-graphql/blob/main/android-app/app/src/main/assets/adventureByPath.query)

```java
AEMHeadlessClientBuilder builder = AEMHeadlessClient.builder().endpoint(config.getContentApiEndpoint());
String user = config.getContentApiUser();
String password = config.getContentApiPassword();
if (user != null && password != null) {
    builder.basicAuth(user, password);
}
AEMHeadlessClient client = builder.build();

// based on the file adventureByPath.query
String query = readFile(getContext(), QUERY_FILE_NAME);

// construct a parameter map to dynamically pass in adventure path
Map<String, Object> params = new HashMap<>();
params.put("adventurePath", this.path);

// execute the query based on the adventureByPath query and passed in parameters
GraphQlResponse response = client.runQuery(query, params);
```

`Adventure.java` is a POJO that gets initialized with the JSON data from the GraphQL request.

`RemoteImagesCache.java` is a utility class that helps prepare remote images in a cache so that they can be used with Android UI elements. The Adventure content references images in AEM Assets via a URL and this class is used to display that content.

### Views

`AdventureListFragment.java` - when called triggers the `AdventuresLoader` and displays the returned adventures in a list.

`AdventureDetailFragment.java` - initializes `AdventureLoader` and displays the details of a single adventure.

## Additional Resources

* [Getting Started with AEM Headless - GraphQL Tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html)
* [AEM Headless Client for Java](https://github.com/adobe/aem-headless-client-java)
