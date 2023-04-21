---
title: Custom namespaces
description: Learn how to define and deploy custom namespaces to AEM as a Cloud Service.
version: Cloud Service
topic: Development, Content Management
feature: Metadata
role: Developer
level: Intermediate
kt: 11618
thumbnail: 3412319.jpg
last-substantial-update: 2022-12-14
exl-id: e86ddc9d-ce44-407a-a20c-fb3297bb0eb2
---
# Custom namespaces

Learn how to define and deploy custom [namespaces](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/4.5_Namespaces.html) to AEM as a Cloud Service. 

Custom namespaces are the optional part of a JCR property preceding a `:`. AEM uses several namespaces such as:

+ `jcr` for JCR system properties
+ `cq` for AEM (formerly known as Adobe CQ) properties
+ `dam` for AEM properties specific to DAM assets
+ `dc` for Dublin Core properties

... and many others. 

Namespaces can be used to denote the scope and intent of a property. Creating a custom namespace, often your company name, helps clearly identify nodes or properties specific to your AEM implementation and contain data specific to your business.

Custom namespaces are managed in [Sling Repository Initialization (repoinit)](https://sling.apache.org/documentation/bundles/repository-initialization.html) scripts, and deploys to AEM as a Cloud Service as OSGi configurations - and added to your [AEM project's](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) `ui.config` project.

>[!VIDEO](https://video.tv.adobe.com/v/3412319?quality=12&learn=on)

## Resources

+ [Sling Repository Initialization (repoinit) documentation](https://sling.apache.org/documentation/bundles/repository-initialization.html#repoinit-parser-test-scenarios)

## Code

The following code is used to configure a `wknd` namespace.

### RepositoryInitializer OSGi configuration

`/ui.config/src/main/content/jcr_root/apps/wknd-examples/osgiconfig/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~wknd-examples-namespaces.cfg.json`

```json
{

    "scripts": [
        "register namespace (wknd) https://site.wknd/1.0"
    ]
}
```

This allows custom properties using the `wknd` namespace, as denoted as the first parameter after the `register namespace` instruction, to be use in AEM. For more advanced script definitions, review the examples in the [Sling Repository Initialization (repoinit) documentation](https://sling.apache.org/documentation/bundles/repository-initialization.html#repoinit-parser-test-scenarios).
