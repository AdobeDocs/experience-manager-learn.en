---
title: Use oak-run.jar to Manage Indexes
seo-title: Use oak-run.jar to Manage Indexes in AEM
description: oak-run.jar's index command consolidates a number of features to manage Oak indexes in AEM, from gathering index statistics, running index consistency checks, and re/indexing indexes themselves.
seo-description: oak-run.jar's index command consolidates a number of features to manage Oak indexes in AEM, from gathering index statistics, running index consistency checks, and re/indexing indexes themselves.
version: 6.4, 6.5
feature: oak
topics: search
activity: use
audience: architect, developer, implementer
doc-type: technical-video
uuid: 1bfc58a1-c1e9-41e5-b762-43b56ff240dc
discoiquuid: 5768953e-562a-4766-9e28-360d3b856d1c
---

# Use oak-run.jar to Manage Indexes

oak-run.jar's index command consolidates a number of features to manage Oak indexes in AEM, from gathering index statistics, running index consistency checks, and re/indexing indexes themselves.

>[!NOTE]
>
>Within this article and videos the terms indexing and re-indexing are used interchangeably and considered the same operation.

## oak-run.jar index Command Basics

>[!VIDEO](https://video.tv.adobe.com/v/21475/?quality=9)

* The version of [oak-run.jar](https://repository.apache.org/service/local/artifact/maven/redirect?r=releases&g=org.apache.jackrabbit&a=oak-run&v=1.8.0) used must match the version of Oak used on the AEM instance.
* Managing indexes using oak-run.jar leverages the **index** command with various flags to support different operations.

    * `java -jar oak-run*.jar index ...`

## Index Statistics

>[!VIDEO](https://video.tv.adobe.com/v/21477/?quality=12)

* `oak-run.jar` dumps all index definitions, important index stats and index contents for offline analysis.
* The index statistics gathering is safe to execute on in-use AEM instances.

## Index Consistency Check

>[!VIDEO](https://video.tv.adobe.com/v/21476/?quality=12)

* `oak-run.jar` quickly determines if lucene Oak indexes are corrupt.
* The consistency check is safe to run on in-use AEM instance for consistency check levels 1 and 2.

## TarMK Online indexing with oak-run.jar {#tarmkonlineindexingwithoakrunjar}

>[!VIDEO](https://video.tv.adobe.com/v/21479/?quality=12)

* Online indexing of TarMK using oak-run.jar is faster than setting `reindex=true` on the `oak:queryIndexDefinition` node. Despite this performance increase, online indexing using oak-run.jar still requires a maintenance window to perform the indexing.

* Online indexing of TarMK using oak-run.jar should **not** be executed against AEM instances outside of the AEM's instances maintenance window.

## TarMK Offline indexing with oak-run.jar

>[!VIDEO](https://video.tv.adobe.com/v/21478/?quality=12)

* Offline indexing of TarMK using oak-run.jar is the simplest oak-run.jar based indexing approach for TarMK as it requires a single oak-run.jar command, however it requires the AEM instance to be shutdown.

## TarMK Out-of-band indexing with oak-run.jar

>[!VIDEO](https://video.tv.adobe.com/v/21480/?quality=12)

* Out-of-band indexing on TarMK using oak-run.jar minimizes the impact of indexing on in-use AEM instances.
* Out-of-band indexing is the recommended indexing approach for AEM installations where the time to re/index exceeds the available maintenance windows.

## MongoMK Online indexing with oak-run.jar

* Online index with oak-run.jar on MongoMK and RDBMK is the recommended method for re/indexing MongoMK (and RDBMK) AEM installations. **No other method should be used for MongoMK or RDBMK.**
* This indexing needs to be executed only against a single AEM instance in the cluster.
* Online indexing of MongoMK is safe to execute against a running AEM cluster, as the repository traversal will occur on only a single MongoDB node, allowing the others to continue serving requests without significant performance impact.

The oak-run.jar index command to perform an online indexing of MongoMK is the [same as the TarMK Online indexing with oak-run.jar](#tarmkonlineindexingwithoakrunjar) with the difference that the segment store parameter points to the MongoDB instance that contains the Node store.

```
java -jar oak-run*.jar index
 --reindex
 --index-paths=/oak:index/lucene
 --read-write
 --fds-path=/path/to/datastore mongodb://server:port/aem
```

## Supporting materials

* [Download oak-run.jar](https://repository.apache.org/#nexus-search;gav~org.apache.jackrabbit~oak-run~~~~kw,versionexpand)
    * *Ensure the downloaded version matches the version of Oak installed on AEM as described above*
* [Apache Jackrabbit Oak oak-run.jar Index Command Documentation](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html)
