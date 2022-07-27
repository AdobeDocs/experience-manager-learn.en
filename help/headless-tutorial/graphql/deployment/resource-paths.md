---
title: Resolving image paths for AEM GraphQL
description: 
version: Cloud Service
feature: GraphQL API
topic: Headless, Content Management
role: Developer, Architect
level: Intermediate
kt: 
thumbnail: KT-.jpg
mini-toc-levels: 2
---

# Image paths for AEM GraphQL

https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/how-to/images.html

## Path requirements


| Client                      | Shares domain with AEM  | Separate domain from AEM | No domain (ex. Mobile, Server-side) |
|----------------------------:|:-----------------------:|:------------------------:|:-----------------------------------:|
| Requires Resource path      | &#10008;                | &#10004;                 | &#10004;  |

## Use AEM Host

```graphql
query ($path: String!) {
  adventureByPath(_path: $path) {
    item {
      title,
      primaryImage {
        ... on ImageRef {
          _path
        }
      }
    }
  }
}
```

```graphql
{
  "data": {
    "adventureByPath": {
      "item": {
        "adventurePrimaryImage": {
          "_path": "/content/dam/wknd-shared/en/adventures/bali-surf-camp/adobestock-175749320.jpg",
        }
      }
    }
  }
}
```

```javascript 
...
// Import the AEM origin from the app's environment configuration
const AEM_ORIGIN = env.process.REACT_APP_AEM_ORIGIN; // https://publish-p123-e456.aemcloud.com

let { data, error } = useAdventureByPath('/content/dam/wknd-shared/en/adventures/bali-surf-camp/adobestock-175749320.jpg')

return (
    {/* <img src="https://publish-p123-e456.aemcloud.com/content/dam/wknd-shared/en/adventures/bali-surf-camp/adobestock-175749320.jpg"/>  */}
    <img src={AEM_ORIGIN + data.adventureByPath.item.primaryImage._path }>
)
```

## Use AEM Host

```graphql
query ($path: String!) {
  adventureByPath(_path: $path) {
    item {
      title,
      primaryImage {
        ... on ImageRef {
          _publishUrl
        }
      }
    }
  }
}
```

```graphql
{
  "data": {
    "adventureByPath": {
      "item": {
        "adventurePrimaryImage": {
          "_publishUrl": "https://publish-p123-e789.adobeaemcloud.com/content/dam/wknd-shared/en/adventures/bali-surf-camp/adobestock-175749320.jpg"
        }
      }
    }
  }
}
```

```javascript 
...
let { data, error } = useAdventureByPath('/content/dam/wknd-shared/en/adventures/bali-surf-camp/adobestock-175749320.jpg')

return (
    {/* <img src="https://publish-p123-e789.adobeaemcloud.com/content/dam/wknd-shared/en/adventures/bali-surf-camp/adobestock-175749320.jpg"/>  */}
    <img src={AEM_ORIGIN + data.adventureByPath.item.primaryImage._publishUrl }>
)
```
