---
title: Use the System Overview Dashboard
seo-title: Use the System Overview Dashboard in AEM
description: In previous versions of AEM administrators needed to look at several locations in order to get a full picture of the AEM instance. The System Overview aims to solve this by providing a high level view of the configuration, hardware, and health of the AEM instance all from a single dashboard.
seo-description: In previous versions of AEM administrators needed to look at several locations in order to get a full picture of the AEM instance. The System Overview aims to solve this by providing a high level view of the configuration, hardware, and health of the AEM instance all from a single dashboard.
uuid: bfdd5079-5329-46ac-8d10-a416c8d5afd4
contentOwner: dgordon
products: SG_EXPERIENCEMANAGER/6.4/MANAGING
topic-tags: monitoring
discoiquuid: 84d56074-330b-4e80-9d08-533f23ab6621
targetaudience: target-audience new;target-audience ongoing
index: y
internal: n
snippet: y
---

# Use the System Overview Dashboard

Adobe Experience Manager's (AEM) System Overview provides a high level view of the configuration, hardware, and health of the AEM instance all from a single dashboard.

>[!VIDEO](https://video.tv.adobe.com/v/21340?quality=12)

1. The System Overview can be accessed from: **AEM Start** &gt; **Tools** &gt; **Operations** &gt; **System Overview**

   Directly at **&lt;server-host&gt;/libs/granite/operations/content/systemoverview.html**

1. The information from the System Overview can be exported by clicking the download button. The information is also exposed via the following REST endpoint:
1. Below is a sample output of the JSON that is exported from the System Overview:

   ```shell
   {
       "Health Checks": {
           "1 Critical": "System Maintenance",
           "3 Warn": "Replication Queue, Log Errors, Sling/Granite Content Access Check"
       },
       "Instance": {
           "Adobe Experience Manager": "6.4.0",
           "Run Modes": "s7connect, crx3, non-composite, author, samplecontent, crx3tar",
           "Instance Up Since": "2018-01-22 10:50:37"
       },
       "Repository": {
           "Apache Jackrabbit Oak": "1.8.0",
           "Node Store": "Segment Tar",
           "Repository Size": "0.26 GB",
           "File Data Store": "crx-quickstart/repository/datastore"
       },
       "Maintenance Tasks": {
           "Failed": "AuditLog Maintenance Task, Project Purge, Workflow Purge",
           "Succeeded": "Data Store Garbage Collection, Lucene Binaries Cleanup, Revision Clean Up, Version Purge, Purge of ad-hoc tasks"
       },
       "System Information": {
           "Mac OS X": "10.12.6",
           "System Load Average": "2.29",
           "Usable Disk Space": "89.44 GB",
           "Maximum Heap": "0.97 GB"
       },
       "Estimated Node Counts": {
           "Total": "232448",
           "Tags": "62",
           "Assets": "267",
           "Authorizables": "210",
           "Pages": "1592"
       },
       "Replication Agents": {
           "Blocked": "publish, publish2",
           "Idle": "offloading_b3deb296-9b28-4f60-8587-c06afa2e632c, offloading_outbox, offloading_reverse_b3deb296-9b28-4f60-8587-c06afa2e632c, publish_reverse, scene7, screens, screens2, test_and_target"
       },
       "Distribution Agents": {
           "Blocked": "publish"
       },
       "Workflows": {
           "Running Workflows": "15",
           "Failed Workflows": "15",
           "Failed Jobs": "150"
       },
       "Sling Jobs": {
           "Failed": "305"
       }
   }
   ```
