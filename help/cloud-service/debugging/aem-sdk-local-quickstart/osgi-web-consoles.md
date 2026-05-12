---
title: Debugging AEM SDK using the OSGi web console
description: The AEM SDK’s local quickstart has an OSGi web console that provides a variety of information and introspections into the local AEM runtime that are useful to understand how your application is recognized by, and functions within AEM.
feature: Developer Tools
version: Experience Manager as a Cloud Service
doc-type: Tutorial
kt: 5265, 5366, 5267
topic: Development
role: Developer
level: Beginner, Intermediate
exl-id: 0929bc1a-376c-4e16-a540-a276fd5af164
duration: 486
TQID: https://experienceleague.adobe.com/cWoqY-xWdYY6KLUKL8yLmtSqyYeRGH7I5sbTAc0KgJY
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
---
# Debugging AEM SDK using the OSGi web console

The AEM SDK’s local quickstart has an OSGi web console that provides a variety of information and introspections into the local AEM runtime that are useful to understand how your application is recognized by, and functions within AEM.

AEM provides many OSGi consoles, each providing key insights into different aspects of AEM, however the following are typically the most useful in debugging your application.

## Bundles

>[!VIDEO](https://video.tv.adobe.com/v/34335?quality=12&learn=on)

The Bundles console is a catalog of the OSGi bundles, and their details, deployed to AEM, along with the ad hoc ability to start and stop them.

The Bundles console is located at:

+ Tools > Operations > Web Console > OSGi > Bundles
+ Or directly at: [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

Clicking into each bundle, provides details that help with the debugging your application.

+ Validating the OSGi bundle is present
+ Validating if an OSGi bundle is active
+ Determining if an OSGi bundle has unsatisfied imports preventing it from starting

## Components

>[!VIDEO](https://video.tv.adobe.com/v/34336?quality=12&learn=on)

The Components console is a catalog of all the OSGi components deployed to AEM, and provides a all information about them, from their defined OSGi component life cycle, to what OSGi services they may reference to 

The Components console is located at:

+ Tools > Operations > Web Console > OSGi > Components
+ Or directly at: [http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)

Key aspects that help with the debugging activities:

+ Validating the OSGi bundle is present
+ Validating if an OSGi bundle is active
+ Determining if an OSGi bundle has unsatisfied imports preventing it from starting
+ Obtaining the component's PID, in order create OSGi configurations for them in Git
+ Identifying OSGi property values bound to the active OSGi configuration

## Sling Models

>[!VIDEO](https://video.tv.adobe.com/v/34337?quality=12&learn=on)

The Sling Models console is located at:

+ Tools > Operations > Web Console > Status > Sling Models
+ Or directly at: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels )

Key aspects that help with the debugging activities:

+ Validating Sling Models are registered to the proper resource type
+ Validating Sling Models are adaptable from the correct objects (Resource or SlingHttpRequestServlet)
+ Validating Sling Model Exporters are properly registered
