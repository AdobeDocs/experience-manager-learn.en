---
title: Debugging AEM SDK
description: AEM SDK is the primary development environment used by developers, and supports a myriad of ways to debug AEM and deployed applications.
feature: Developer Tools
version: Experience Manager as a Cloud Service
doc-type: Tutorial
topic: Development
role: Developer
level: Beginner, Intermediate
exl-id: e27cf3de-ef89-44d7-819b-157f85f5a80f
duration: 41
TQID: https://experienceleague.adobe.com/GdxF4vrk29NaIvGZ9jBeQiIQ4vnaYZ1BUilVEdc3eI0
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
---
# Debugging AEM SDK

AEM SDK's local quickstart is the primary development environment used by developers, and supports a myriad of ways to debug AEM and deployed applications. This user guide takes, you through some of the more common debug tools and consoles for debugging your application on the AEM SDK's local quickstart.

## Logs 

Logs act as the frontline for debugging AEM applications, but are dependent on adequate logging in the deployed AEM application. 

[Debugging AEM SDK using logs](./logs.md)

## Remote debugging

Remote debugging of Java code running in AEM SDK's local quickstart allows for the step-through of live code execution in AEM from your IDE.

[Remote debugging the AEM SDK](./remote-debugging.md)

## OSGi web consoles

The AEM SDK's local quickstart has an OSGi web console that provides a variety of information and introspections into the local AEM runtime that are useful to understand how your application is recognized by, and functions within AEM.

[Debugging the AEM SDK using the OSGi web console](./osgi-web-consoles.md)

## Other tools

A variety of other tools can aid in debugging your application on the AEM SDK's local quickstart. 

[Other tools for debugging AEM SDK](./other-tools.md)
