---
title: Managing AEM hosts for AEM GraphQL
description: Learn how to configure AEM hosts in AEM Headless app.
version: Cloud Service
feature: GraphQL API
topic: Headless, Content Management
role: Developer, Architect
level: Intermediate
jira: KT-10831
thumbnail: KT-10831.jpg
exl-id: a932147c-2245-4488-ba1a-99c58045ee2b
---
# Managing AEM hosts

Deploying an AEM Headless application requires attention to how AEM URLs are constructed to ensure the correct AEM host/domain is used. The primary  URL/request types to be aware of are:

+ HTTP requests to __[AEM GraphQL APIs](#aem-graphql-api-requests)__
+ __[Image URLs](#aem-image-urls)__ to image assets referenced in Content Fragments, and delivered by AEM

Typically, an AEM Headless app interacts with a single AEM service for both GraphQL API and image requests. The AEM service changes based on the AEM Headless app deployment:

| AEM Headless deployment type  | AEM environment      | AEM service       |
|-------------------------------|:---------------------:|:----------------:|
| Production                    | Production            | Publish          |
| Authoring preview             | Production            | Preview          |
| Development                   | Development           | Publish          |

To handle deployment type permutations, each app deployment is built using a configuration specifying the AEM service to connect to. The configured AEM service's host/domain is then used to construct the AEM GraphQL API URLs and Image URLs. To determine the correct approach for managing build dependent configurations, reference the AEM Headless app's framework (for example, React, iOS, Android&trade;, and so on) documentation, as the approach varies by framework.

| Client type                               | [Single-page app (SPA)](../spa.md) | [Web Component/JS](../web-component.md) | [Mobile](../mobile.md)    | [Server-to-server](../server-to-server.md) |
|------------------------------------------:|:---------------------:|:----------------:|:---------:|:----------------:|
| AEM hosts configuration | &#10004;              | &#10004;         | &#10004;  | &#10004;         |

The following are examples of possible approaches for constructing URLs for [AEM GraphQL API](#aem-graphql-api-requests) and [image requests](#aem-image-requests), for several popular headless frameworks and platforms.

## AEM GraphQL API requests

The HTTP GET requests from the headless app to AEM's GraphQL APIs must be configured to interact with the correct AEM service, as described in the [table above](#managing-aem-hosts). 

When using [AEM Headless SDKs](../../how-to/aem-headless-sdk.md) (available for browser-based JavaScript, server-based JavaScript, and Java&trade;), an AEM host can initialize the AEM Headless client object with the AEM Service to connect with.

When developing a custom AEM Headless client, ensure the AEM service's host is parameterize-able based on build parameters.

### Examples 

The following are examples of how AEM GraphQL API requests can have the AEM host value made configurable for various headless app frameworks.

+++ React example

This example, loosely based on the [AEM Headless React app](../../example-apps/react-app.md), illustrates how AEM GraphQL API requests can be configured to connect to different AEM Services based on environment variables.

React apps should use the [AEM Headless Client for JavaScript](../../how-to/aem-headless-sdk.md) to interact with AEM's GraphQL APIs. The AEM Headless client, provided by the AEM Headless Client for JavaScript, must be initialized with the AEM Service host it connects to.

#### React environment file

React uses [custom environment files](https://create-react-app.dev/docs/adding-custom-environment-variables/), or `.env` files, stored in the root of the project to define build-specific values. For example, the `.env.development` file contains values used for during development, while `.env.production` contains values used for production builds.

+ `.env.development`

```
# Environment variable used to specify the AEM service the React app will connect to when running under this profile
REACT_APP_AEM_HOST=https://publish-p123-e456.adobeaemcloud.com
...
```

`.env` files for other uses [can be specified](https://create-react-app.dev/docs/adding-custom-environment-variables/#what-other-env-files-can-be-used) by postfixing `.env` and a semantic descriptor, such as `.env.stage` or `.env.production`. Different `.env` files can be used when running or building the React app, by setting the `REACT_APP_ENV` before executing an `npm` command. 

For example, a React app's `package.json` may contain the following `scripts` config:

+ `package.json`

```
...
"scripts": {
  "build:development": "REACT_APP_ENV=development npm run build",
  "build:stage": "REACT_APP_ENV=stage npm run build",
  "build:production": "REACT_APP_ENV=production npm run build"
},
...
```

#### AEM headless client

The [AEM Headless Client for JavaScript](../../how-to/aem-headless-sdk.md) contains an AEM Headless client that makes HTTP requests to AEM's GraphQL APIs. The AEM Headless client must be initialized with the AEM host it interacts with, using the value from the active `.env` file.

+ `src/api/headlessClient.js`

```
const { AEMHeadless } = require('@adobe/aem-headless-client-js');
...
// Get the environment variables for configuring the headless client, 
// specifically the `REACT_APP_AEM_HOST` which contains the AEM service host.
const {
    REACT_APP_AEM_HOST,         // https://publish-p123-e456.adobeaemcloud.com
    REACT_APP_GRAPHQL_ENDPOINT,
} = process.env;
...

// Initialize the AEM Headless client with the AEM Service host, which dictates the AEM service provides the GraphQL data.
export const aemHeadlessClient = new AEMHeadless({
    serviceURL: REACT_APP_AEM_HOST,        
    endpoint: REACT_APP_GRAPHQL_ENDPOINT
});
```

#### React useEffect(..) hook

Custom React useEffect hooks call the AEM Headless client, initialized with the AEM host, on behalf of the React component rendering the view. 

+  `src/api/persistedQueries.js`

```javascript
import { aemHeadlessClient , mapErrors} from "./headlessClient";
...
// The exported useEffect hook
export const getAdventureByPath = async function(adventurePath) {
    const queryVariables = {'adventurePath': adventurePath};
    return executePersistedQuery('wknd-shared/adventures-by-path', queryVariables);
}
...
// Private function that invokes the aemHeadlessClient
const executePersistedQuery = async function(persistedQueryPath, queryVariables) {
    let data;
    let errors;

    try {
        // Run the persisted query using using the aemHeadlessClient that's initialized with the AEM host
        const response = await aemHeadlessClient.runPersistedQuery(persistedQueryPath, queryVariables);
        // The GraphQL data is stored on the response's data field
        data = response.data;
        errors = response.errors ? mapErrors(response.errors) : undefined;
    } catch (e) {
        console.error(e.toJSON());
        errors = e;
    }

    return {data, errors}; 
}
```

#### React component

The custom useEffect hook, `useAdventureByPath` is imported, and used to get the data using the AEM Headless client and ultimately render the content to the end user.

+ 'src/components/AdventureDetail.js'

```javascript 
import { useAdventureByPath } from './api/persistedQueries';
...
// Query AEM GraphQL APIs via the useEffect hook that invokes the AEM Headless client initialized with the AEM host
let { data, error } = useAdventureByPath('/content/dam/wknd-shared/en/adventures/bali-surf-camp/adobestock-175749320.jpg')

...
```

+++

+++ iOS&trade; example 

This example, based on the [example AEM Headless iOS&trade; app](../../example-apps/ios-swiftui-app.md), illustrates how AEM GraphQL API requests can be configured to connect to different AEM hosts based on [build-specific configuration variables](https://developer.apple.com/documentation/xcode/adding-a-build-configuration-file-to-your-project?changes=l_3).

iOS&trade; apps require a custom AEM Headless client to interact with AEM's GraphQL APIs. The AEM Headless client must be written such that the AEM service host is configurable.

#### Build configuration

The XCode configuration file contains the default configuration details.

+ `Config.xcconfig`

```swift
// The http/https protocol scheme used to access the AEM_HOST
AEM_SCHEME = https

// Target hostname for AEM service, do not include the scheme: http:// or https://
AEM_HOST = publish-p123-e789.adobeaemcloud.com
...
```

#### Initialize the custom AEM headless client

The [example AEM Headless iOS app](https://github.com/adobe/aem-guides-wknd-graphql/tree/main/ios-app) uses a custom AEM headless client initialized with the config values for `AEM_SCHEME` and `AEM_HOST`.

```swift
...
let aemScheme: String = try Configuration.value(for: "AEM_SCHEME")  // https
let aemHost: String = try Configuration.value(for: "AEM_HOST")      // publish-p123-e456.adobeaemcloud.com

let aemHeadlessClient = Aem(scheme: aemScheme, host: aemHost);
```

The custom AEM headless client (`api/Aem.swift`) contains a method `makeRequest(..)` that prefixes AEM GraphQL APIs requests with the configured AEM `scheme` and `host`.

+ `api/Aem.swift`

```swift
/// #makeRequest(..)
/// Generic method for constructing and executing AEM GraphQL persisted queries
private func makeRequest(persistedQueryName: String, params: [String: String] = [:]) -> URLRequest {
    // Encode optional parameters as required by AEM
    let persistedQueryParams = params.map { (param) -> String in
        encode(string: ";\(param.key)=\(param.value)")
    }.joined(separator: "")
    
    // Construct the AEM GraphQL persisted query URL, including optional query params
    let url: String = "\(self.scheme)://\(self.host)/graphql/execute.json/" + persistedQueryName + persistedQueryParams;

    var request = URLRequest(url: URL(string: url)!);
    
    return request;
}
```

[New build configuration files can be created](https://developer.apple.com/documentation/xcode/adding-a-build-configuration-file-to-your-project?changes=l_3) to connect to different AEM services. The build-specific values for the `AEM_SCHEME` and `AEM_HOST` are used based on the selected build in XCode, resulting in the custom AEM Headless client to connect with the correct AEM service.

+++

+++ Android&trade; example

This example, based on the [example AEM Headless Android&trade; app](https://github.com/adobe/aem-guides-wknd-graphql/tree/main/android-app), illustrates how AEM GraphQL API requests can be configured to connect to different AEM Services based on build-specific (or flavors) configuration variables.

Android&trade; apps (when written in Java&trade;) should use the [AEM Headless Client for Java&trade;](https://github.com/adobe/aem-headless-client-java) to interact with AEM's GraphQL APIs. The AEM Headless client, provided by the AEM Headless Client for Java&trade;, must be initialized with the AEM Service host it connects to.

#### Build configuration file

Android&trade; apps define "productFlavors" that are used to build artifacts for different uses. 
This example shows how two Android&trade; product flavors can be defined, providing different AEM service hosts (`AEM_HOST`) values for development (`dev`) and production (`prod`) uses.

In the app's `build.gradle` file, a new `flavorDimension` named `env` is created. 

In the `env` dimension, two `productFlavors` are defined: `dev` and `prod`. Each `productFlavor` uses `buildConfigField` to set build-specific variables defining the AEM service to connect to.

+ `app/build.gradle`

```gradle
android {
    ...
    flavorDimensions 'env'
    productFlavors {
        dev {
            dimension 'env'
            applicationIdSuffix '.dev'
            buildConfigField "String", "AEM_HOST", '"http://10.0.2.2:4503"'
            ...
        }
        prod {
            dimension 'env'
            buildConfigField "String", "AEM_HOST", '"https://publish-p123-e789.adobeaemcloud.com"'
            ...
        }
    }
    ...
}
``` 

#### Android&trade; loader

Initialize the `AEMHeadlessClient` builder, provided by the AEM Headless Client for Java&trade; with the `AEM_HOST` value from the `buildConfigField` field.

+ `app/src/main/java/com/adobe/wknd/androidapp/loader/AdventuresLoader.java`

```java
public class AdventuresLoader extends AsyncTaskLoader<AdventureList> {
    ...

    @Override
    public AdventureList loadInBackground() {
        ...
        // Initialize the AEM Headless client using the AEM Host exposed via BuildConfig.AEM_HOST
        AEMHeadlessClientBuilder builder = AEMHeadlessClient.builder().endpoint(BuildConfig.AEM_HOST);
        AEMHeadlessClient client = builder.build();
        // With the AEM headless client initialized, make GraphQL persisted query calls to AEM
        ...    
    }
    ...
}
```

When building the Android&trade; app for different uses, specify the `env` flavor, and the corresponding AEM host value is used.

+++

## AEM image URLs

The image requests from the headless app to AEM must be configured to interact with the correct AEM service, as described in the [above table](#managing-aem-hosts).

Adobe recommends using [optimized images](../../how-to/images.md) made available through the `_dynamicUrl` field in AEM's GraphQL APIs. The `_dynamicUrl` field returns an host-less URL that can be prefixed with the AEM service host used to query AEM GraphQL APIs. For the `_dynamicUrl` field in the GraphQL response looks like:

```json
{
    ...
    "_dynamicUrl": "/adobe/dynamicmedia/deliver/dm-aid--dd42d814-88ec-4c4d-b5ef-e3dc4bc0cb42/example.jpg?preferwebp=true",
    ...
}
```

### Examples

The following are examples of how image URLs can prefix the AEM host value made configurable for various headless app frameworks. The examples assume the use of GraphQL queries that return image references using the `_dynamicUrl` field. 

For example:

#### GraphQL persisted query

This GraphQL query returns an image reference's `_dynamicUrl`. As seen in the [GraphQL response](#examples-react-graphql-response) which excludes a host.

```graphql
query ($path: String!) {
  adventureByPath(_path: $path, _assetTransform: { format: JPG, preferWebp: true }) {
    item {
      title,
      primaryImage {
        ... on ImageRef {
          _dynamicUrl
        }
      }
    }
  }
}
```

#### GraphQL response

This GraphQL response returns the image reference's `_dynamicUrl` which excludes a host.

```json
{
  "data": {
    "adventureByPath": {
      "item": {
        "adventurePrimaryImage": {
          "_dynamicUrl": "/adobe/dynamicmedia/deliver/dm-aid--de43411-88ec-4c4d-b5ef-e3dc4bc0cb42/adobestock-175749320.jpg?preferwebp=true",
        }
      }
    }
  }
}
```

+++ React example

This example, based on the [example AEM Headless React app](../../example-apps/react-app.md), illustrates how image URLs can be configured to connect to the correct AEM Services based on environment variables.

This example shows how prefix the image reference `_dynamicUrl` field, with a configurable `REACT_APP_AEM_HOST` React environment variable.

#### React environment file

React uses [custom environment files](https://create-react-app.dev/docs/adding-custom-environment-variables/), or `.env` files, stored in the root of the project to define build-specific values. For example, the `.env.development` file contains values used for during development, while `.env.production` contains values used for production builds.

+ `.env.development`

```
# Environment variable used to specify the AEM service the React app will connect to when running under this profile
REACT_APP_AEM_HOST=https://publish-p123-e456.adobeaemcloud.com
...
```

`.env` files for other uses [can be specified](https://create-react-app.dev/docs/adding-custom-environment-variables/#what-other-env-files-can-be-used) by postfixing `.env` and a semantic descriptor, such as `.env.stage` or `.env.production`. Different `.env` file can be used when running or building the React app, by setting the `REACT_APP_ENV` before executing an `npm` command. 

For example, a React app's `package.json` may contain the following `scripts` config:

+ `package.json`

```
...
"scripts": {
  "build:development": "REACT_APP_ENV=development npm run build",
  "build:stage": "REACT_APP_ENV=stage npm run build",
  "build:production": "REACT_APP_ENV=production npm run build"
},
...
```

#### React component

The React component imports the `REACT_APP_AEM_HOST` environment variable, and prefixes the image `_dynamicUrl` value, to provide a fully resolvable image URL.

This same `REACT_APP_AEM_HOST` environment variable is used to initialize the AEM Headless client used by `useAdventureByPath(..)` custom useEffect hook used to fetch the GraphQL data from AEM. Using the same variable to construct the GraphQL API request as the image URL, ensure that the React app interacts with the same AEM service for both use cases.

+ 'src/components/AdventureDetail.js'

```javascript 
...
// Import the AEM origin from the app's environment configuration
const AEM_HOST = env.process.REACT_APP_AEM_HOST; // https://publish-p123-e456.adobeaemcloud.com

let { data, error } = useAdventureByPath('/content/dam/wknd-shared/en/adventures/bali-surf-camp/bali-surf-camp')

return (
    // Prefix the image src URL with the AEM host
    <img src={AEM_HOST + data.adventureByPath.item.primaryImage._dynamicUrl }>
    {/* Resulting in: <img src="https://publish-p123-e456.adobeaemcloud.com/adobe/dynamicmedia/deliver/dm-aid--de43411-88ec-4c4d-b5ef-e3dc4bc0cb42/adobestock-175749320.jpg"/>  */}
)
```

+++

+++ iOS&trade; example

This example, based on the [example AEM Headless iOS&trade; app](../../example-apps/ios-swiftui-app.md), illustrates how AEM image URLs can be configured to connect to different AEM hosts based on [build-specific configuration variables](https://developer.apple.com/documentation/xcode/adding-a-build-configuration-file-to-your-project?changes=l_3).

#### Build configuration

The XCode configuration file contains the default configuration details.

+ `Config.xcconfig`

```swift
// The http/https protocol scheme used to access the AEM_HOST
AEM_SCHEME = https

// Target hostname for AEM service, do not include the scheme: http:// or https://
AEM_HOST = publish-p123-e789.adobeaemcloud.com
...
```

#### Image URL generator

In `Aem.swift`, the custom AEM headless client implementation, a custom function `imageUrl(..)` takes the image path as provided in the `_dynamicUrl` field in the GraphQL response, and prepends it with AEM's host. This function is then invoked in the iOS views whenever an image is rendered.

+ `WKNDAdventures/AEM/Aem.swift`

```swift

class Aem: ObservableObject {
    let scheme: String
    let host: String
    ...
    init(scheme: String, host: String) {
        self.scheme = scheme
        self.host = host
    }
    ...
    /// Prefixes AEM image dynamicUrl with the AEM scheme/host
    func imageUrl(dynamicUrl: String) -> URL {
        return URL(string: "\(self.scheme)://\(self.host)\(dynamicUrl)")!
    }
    ...
}
```

#### iOS view

The iOS view and prefixes the image `_dynamicUrl` value, to provide a fully resolvable image URL.

+ `WKNDAdventures/Views/AdventureListItemView.swift`

```swift
import SDWebImageSwiftUI
...
struct AdventureListItemView: View {
    @EnvironmentObject private var aem: Aem

    var adventure: Adventure
    
    var body: some View {
        HStack {
            // Path the image dynamicUrl to `aem.imageUrl(..)` to prepend the AEM service host     
            AdventureRowImage(imageUrl: aem.imageUrl(dynamicUrl: adventure.image()))
            Text(adventure.title)
            Spacer()
        }
    }
}
...
```

[New build configuration files can be created](https://developer.apple.com/documentation/xcode/adding-a-build-configuration-file-to-your-project?changes=l_3) to connect to different AEM services. The build-specific values for the `AEM_SCHEME` and `AEM_HOST` are used based on the selected build in XCode, resulting in the custom AEM Headless client to interact with the correct AEM service.

+++

+++ Android&trade; example

This example, based on the [example AEM Headless Android&trade; app](https://github.com/adobe/aem-guides-wknd-graphql/tree/main/android-app), illustrates how AEM image URLs can be configured to connect to different AEM Services based on build-specific (or flavors) configuration variables.

#### Build configuration file

Android&trade; apps define "productFlavors" which are used to build artifacts for different uses. 
This example shows how two Android&trade; product flavors can be defined, providing different AEM service hosts (`AEM_HOST`) values for development (`dev`) and production (`prod`) uses.

In the app's `build.gradle` file, a new `flavorDimension` named `env` is created. 

In the `env` dimension, two `productFlavors` are defined: `dev` and `prod`. Each `productFlavor` uses `buildConfigField` to set  build-specific variables defining the AEM service to connect to.

+ `app/build.gradle`

```gradle
android {
    ...
    flavorDimensions 'env'
    productFlavors {
        dev {
            dimension 'env'
            applicationIdSuffix '.dev'
            buildConfigField "String", "AEM_HOST", '"http://10.0.2.2:4503"'
            ...
        }
        prod {
            dimension 'env'
            buildConfigField "String", "AEM_HOST", '"https://publish-p123-e789.adobeaemcloud.com"'
            ...
        }
    }
    ...
}
``` 

#### Loading the AEM image

The Android&trade; uses an `ImageGetter` to fetch and locally cache image data from AEM. In `prepareDrawableFor(..)` the AEM service host, defined in the active build config, is used to prefix the image path creating a resolvable URL to AEM.

+ `app/src/main/java/com/adobe/wknd/androidapp/loader/RemoteImagesCache.java`

```java
...
public class RemoteImagesCache implements Html.ImageGetter {
    ...
    private final Map<String, Drawable> drawablesByPath = new HashMap<>();
    ...
    public void prepareDrawableFor(String path) {
        ...

        // Prefix the image path with the build config AEM_HOST variable
        String urlStr = BuildConfig.AEM_HOST + path;

        URL url = new URL(urlStr);
        HttpURLConnection connection = (HttpURLConnection) url.openConnection();
        // Get the image data from AEM 
        Drawable drawable = Drawable.createFromStream(is, new File(path).getName());
        ...
        // Save the image data into the cache using the path as the key
        drawablesByPath.put(path, drawable);
        ...    
    }

    @Override
    public Drawable getDrawable(String dynamicUrl) {
        // Get the image data from the cache using the dynamicUrl as the key
        return drawablesByPath.get(dynamicUrl);
    }
}
```

#### Android&trade; view

The Android&trade; view gets the image data by way of the `RemoteImagesCache` using the `_dynamicUrl` value from the GraphQL response.

+ `app/src/main/java/com/adobe/wknd/androidapp/AdventureDetailFragment.java`

```java
...
public class AdventureDetailFragment extends Fragment implements LoaderManager.LoaderCallbacks<Adventure> {
    ...
    private ImageView adventureDetailImage;
    ...

    private void updateContent() {
        ...
        adventureDetailImage.setImageDrawable(RemoteImagesCache.getInstance().getDrawable(adventure.getPrimaryImageDynamicUrl()));
        ...
    }
...
}
```

When building the Android&trade; app for different uses, specify the `env` flavor, and the corresponding AEM host value is used.

+++
