---
title: Developing for Brand Portal with AEM Assets
seo-title: Developing for Brand Portal with AEM Assets
description: An abridged walk-through using AEM's DamSyncService API in conjunction with AEM Workflow to programmatically publish assets to AEM Assets Brand Portal.
seo-description: An abridged walk-through using AEM's DamSyncService API in conjunction with AEM Workflow to programmatically publish assets to AEM Assets Brand Portal.
uuid: f934152b-4e66-4402-b197-bbb561c33086
feature: asset-share, brand-portal
topics: authoring, sharing, collaboration, search, integrations, publishing, metadata, images, renditions
audience: developer, architect, administrator
doc-type: technical-video
activity: develop
version: 6.3, 6.4, 6.5
team: TM
---

# Developing for Brand Portal with AEM Assets{#developing-for-brand-portal-with-aem-assets}

An abridged walk-through using AEM's DamSyncService API in conjunction with AEM Workflow to programmatically publish assets to AEM Assets Brand Portal.

>[!VIDEO](https://video.tv.adobe.com/v/18494t1/?quality=9)

## DAMSyncService API {#damsyncservice-api}

Below is an abbreviated version of the code used in the WorkflowProcess demonstrated in the above video. The full, working code is available via [ACS AEM Commons' Brand Portal Sync Workflow Process](https://github.com/Adobe-Consulting-Services/acs-aem-commons/blob/master/bundle/src/main/java/com/adobe/acs/commons/workflow/process/impl/BrandPortalSyncProcess.java) and can be used as is, or adapted for use.

They key call outs are

1. Obtaining the `DAMSyncService` object
2. Collecting the workflow payload(s) path(s)
3. Passing the payload path(s) to

    1. `damSyncService.publishResourcesToMP(..)` to publish assets TO Brand Portal
    2. `damSyncService.unpublishResourcesFromMP(..)`to remove assets FROM Brand Portal

```java

import com.adobe.cq.dam.mac.sync.api.DAMSyncService;

public class BrandPortalSyncProcess implements WorkflowProcess {

  @Reference 
  private DAMSyncService damSyncService;

  public final void execute(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap metaDataMap) throws WorkflowException {
    List<String> assetPaths = new ArrayList<String>();
    assetPaths.add((String) workItem.getWorkflowData().getPayload());

    // Publish assets to Brand Portal    
    damSyncService.publishResourcesToMP(assetPaths, resourceResolver);

    // Unpublish assets from Brand Portal    
    damSyncService.unpublishResourcesFromMP(assetPaths, resourceResolver);

```

>[!NOTE]
>
>Remember, the `DAMSyncService` APIs use the usual asynchronous, job-based replication to publish assets to Brand Portal.
>
>To understand the ramifications of this, please read through [Understanding Brand Portal with AEM Assets](brand-portal-article-understand.md).

## Asset folder mpConfig property {#asset-folder-mpconfig-property}

All illustrated in the above video, a valid AEM Cloud Service configuration path must be provided in a property names mpConfig on an ancestor Assets Folder node.

This property must be on the Asset's folder node ( `sling:Folder` or `sling:OrderedFolder`, and NOT the folder's `jcr:content` node). For example:

```java

/content/dam/brand-assets-folder@mpConfig=/etc/cloudservices/mediaportal/brand-portal

```

If an asset is passed to the `DAMSyncService` and that assets does not have an ancestor Assets folder node with the `mpConfig` property set, the following exception will occur:

```java

Caused by: java.lang.NullPointerException: null
 at com.adobe.cq.dam.mac.sync.impl.DAMSyncServiceImpl.getTenantFromConfiguration(DAMSyncServiceImpl.java:784)
 at com.adobe.cq.dam.mac.sync.impl.DAMSyncServiceImpl.getTenantIdForPath(DAMSyncServiceImpl.java:437)
 at com.adobe.cq.dam.mac.sync.impl.DAMSyncServiceImpl.getAgentFilter(DAMSyncServiceImpl.java:571)
 at com.adobe.cq.dam.mac.sync.impl.DAMSyncServiceImpl.syncFolder(DAMSyncServiceImpl.java:265)
 at com.adobe.cq.dam.mac.sync.impl.DAMSyncServiceImpl.publishResourcesToMP(DAMSyncServiceImpl.java:217)
 at com.adobe.acs.commons.workflow.process.impl.BrandPortalSyncProcess.execute(BrandPortalSyncProcess.java:100)
 at com.day.cq.workflow.compatibility.CQWorkflowProcessRunner.execute(CQWorkflowProcessRunner.java:93)
 ... 9 common frames omitted

```

## Additional Resources{#additional-resources}

* [DamSyncService API Java Docs](https://docs.adobe.com/docs/en/aem/6-2/develop/ref/javadoc/com/adobe/cq/dam/mac/sync/api/DAMSyncService.html)
* [WorkflowProcess API Java Docs](https://docs.adobe.com/docs/en/aem/6-2/develop/ref/javadoc/com/adobe/granite/workflow/exec/WorkflowProcess.html)
* [AEM Assets Brand Portal Adobe Docs](https://helpx.adobe.com/experience-manager/brand-portal/using/brand-portal.html)
* [Brand Portal Sync Workflow Process code](https://github.com/Adobe-Consulting-Services/acs-aem-commons/blob/master/bundle/src/main/java/com/adobe/acs/commons/workflow/process/impl/BrandPortalSyncProcess.java)
