---
title: Find and remove deprecated APIs in AEM as a Cloud Service
description: Learn how to find and remove deprecated APIs in AEM as a Cloud Service.
version: Experience Manager as a Cloud Service
role: Developer, Architect
level: Beginner
doc-type: tutorial
duration: 
jira: KT-20288
thumbnail: KT-20288.png
last-substantial-update: 2026-02-09
---

# Find and remove deprecated APIs in AEM as a Cloud Service

Learn how to find and remove deprecated APIs in AEM as a Cloud Service.

## Overview

AEM as a Cloud Service **Action Center** notifies you about _deprecated APIs_ in your project. To get the latest features, security updates, and smooth deployments of your code to AEM as a Cloud Service using Cloud Manager pipelines, remove deprecated APIs from your project.

In this tutorial, you learn how to find and remove deprecated APIs in your AEM as a Cloud Service environment using the [AEM Analyser Maven Plugin](https://github.com/adobe/aemanalyser-maven-plugin/blob/main/aemanalyser-maven-plugin/README.md).

## How to find deprecated APIs

Follow these steps to find deprecated APIs in your AEM as a Cloud Service project.

1. **Use the latest AEM Analyser Maven Plugin**

   In your AEM project, use the latest version of the [AEM Analyser Maven Plugin](https://github.com/adobe/aemanalyser-maven-plugin/blob/main/aemanalyser-maven-plugin/README.md).

   - In the main `pom.xml`, the plugin version is usually declared. Compare your version with the latest [released version](https://mvnrepository.com/artifact/com.adobe.aem/aemanalyser-maven-plugin).

        ```xml
        ...
        <aemanalyser.version>1.6.14</aemanalyser.version> <!-- Latest released version as of 09-Feb-2026 -->
        ...
        <!-- AEM Analyser Plugin -->
        <plugin>
            <groupId>com.adobe.aem</groupId>
            <artifactId>aemanalyser-maven-plugin</artifactId>
            <version>${aemanalyser.version}</version>
            <extensions>true</extensions>
        </plugin>
        ...
        ```

   - The plugin checks against the latest available AEM SDK. Use the latest AEM SDK version in your project's `pom.xml` file. It helps to surface the deprecated APIs as IDE warnings.

        ```xml
        ...
        <aem.sdk.api>2026.2.24288.20260204T121510Z-260100</aem.sdk.api> <!-- Latest available AEM SDK version as of 09-Feb-2026 -->
        ...
        ```

   - Ensure the `all` module runs the plugin in the `verify` phase.

        ```xml
        ...
        <build>
            <plugins>
                ...
                <plugin>
                    <groupId>com.adobe.aem</groupId>
                    <artifactId>aemanalyser-maven-plugin</artifactId>
                    <extensions>true</extensions>
                    <executions>
                        <execution>
                            <id>analyse-project</id>
                            <phase>verify</phase>
                            <goals>
                                <goal>project-analyse</goal>
                            </goals>
                        </execution>
                    </executions>
                </plugin>
                ...
            </plugins>
        </build>
        ...
        ```

2. **Run a build and check for warnings**

   When you run `mvn clean install`, the analyzer reports deprecated APIs as **[WARNING]** messages in the output. For example:

    ```shell
    ...
    [WARNING] The analyser found the following warnings for author and publish :
    [WARNING] [region-deprecated-api] com.adobe.aem.guides:aem-guides-wknd.core:4.0.5-SNAPSHOT: Usage of deprecated package found : org.apache.commons.lang : Commons Lang 2 is in maintenance mode. Commons Lang 3 should be used instead. Deprecated since 2021-04-30 For removal : 2021-12-31 (com.adobe.aem.guides:aem-guides-wknd.all:4.0.5-SNAPSHOT)
    ...
    ```

   It's easy to overlook these messages when focusing on build success or failure. 

3. **Get a clear list of deprecated APIs**

    The above step also provides the same information. However, run the `verify` phase on the `all` module to see all **[WARNING]** messages in one place. For example:

    ```shell
    $ mvn clean verify -pl all
    ```

   The **[WARNING]** messages in the build output list the deprecated APIs in your project.

## How to remove deprecated APIs

The AEM Analyser reports **what** is deprecated and provides the **recommendation** on how to fix it. However, use the table below to choose the right action, and follow the linked documentation when you need more detail.

### Deprecated API remediation strategy

| Analyzer warning type | What it indicates | Recommended action | Reference |
| --------------------- | ----------------- | ------------------ | --------- |
| Deprecated AEM API | API is to be removed from AEM as a Cloud Service | Replace usage with the supported public API | [API Removal Guidance](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features#api-removal-guidance) |
| Deprecated AEM package or class | Package or class is no longer supported | Refactor code to use the recommended alternative | [Deprecated APIs](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features#aem-apis) |
| Deprecated third-party library | Library will not be supported in future SDKs | Upgrade the dependency and refactor usage | [General Guidelines](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features#api-removal-guidance) |
| Deprecated Sling / OSGi patterns | Legacy annotations or APIs detected | Migrate to modern Sling and OSGi APIs | [Removal of Sling / OSGi patterns](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features#api-removal-guidance) |
| Planned removal (future date) | API still works but removal is enforced later | Schedule cleanup before pipeline enforcement | [Release notes](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/home) |

### Practical guidance

- Treat analyzer warnings as **future pipeline failures**, not optional messages.
- Fix deprecated APIs locally using the **latest AEM SDK**.
- Keep the analyzer output clean to avoid problems during future AEM upgrades.

Fixing deprecated APIs early keeps your project **upgrade-safe and deployment-ready**.

## Additional resources

- [AEM Analyser Maven Plugin](https://github.com/adobe/aemanalyser-maven-plugin/blob/main/aemanalyser-maven-plugin/README.md)
- [Deprecated and Removed Features and APIs](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features#api-removal-guidance)

