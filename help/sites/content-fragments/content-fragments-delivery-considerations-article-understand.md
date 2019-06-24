---
title: Understanding AEM Content Fragment Delivery Considerations
seo-title: Understanding AEM Content Fragment Delivery Considerations
description: AEM 6.3 enhances Content Fragment integration with AEM Sites and introduces several technical implementation aspects worth understanding while delivering AEM projects using Content Fragments.
seo-description: AEM 6.3 enhances Content Fragment integration with AEM Sites and introduces several technical implementation aspects worth understanding while delivering AEM projects using Content Fragments.
page-status-flag: de-activated
uuid: dade6603-d6e3-4711-b7a3-090c62ad5e0a
products: SG_EXPERIENCEMANAGER/6.3/SITES
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
topic-tags: content-fragments
discoiquuid: 202958d6-462f-493c-a3cd-a7c77a86114e
targetaudience: target-audience advanced
index: y
internal: n
snippet: y
---

# Understanding AEM Content Fragment Delivery Considerations{#understanding-aem-content-fragment-delivery-considerations}

AEM 6.3 enhances Content Fragment integration with AEM Sites and introduces several technical implementation aspects worth understanding while delivering AEM projects using Content Fragments.

## Fragment Modules {#fragment-modules}

### Fragment Module processing configuration {#fragment-module-processing-configuration}

The AEM Content Fragment Updater OSGi services orchestrates the execution of **Fragment Modules** which perform the work.

The primary method for engagement with this OSGi service is via Sling Jobs issued with

* Job topic = **dam/cfm/updateprocessor**
* Event name = **&lt;event name defined below&gt;**
* Path =** /content/dam/path/to/content-fragment**

The **Fragment Modules** used to process fragment updates are defined in an overlay-able location at:

* Fragment module registry:** /mnt/overlay/dam/cfm/config/processing/&lt;run-mode&gt;/&lt;event-name&gt;/&lt;module-name&gt;**
* Event names: **fragmentchange, instanceupdate, replication**
* Module names: **mixedmedia, inbetween, prerender, dispatcherflush**

### Fragment Module definitions {#fragment-module-definitions}

#### mixedmedia {#mixedmedia}

The **mixedmedia** module converts Content Fragment mixed-media into AEM Image components as defined by the policy)

#### inbetween {#inbetween}

The **inbetween** module creates the responsive grid resources in-between Content Fragment paragraphs

#### prerender {#prerender}

The **prerender **fragment module renders the Content Fragment component (CFc) via a service-user account and synthetic, internal HTTP Request and stores the HTML output into a property named **test** on the CFc resource.

Remember, the entire HTML output is stored under the Page including HTML elements and attributes of the CFc itself or inter-paragraph components. This means that HTML may influence AEM Page search results.

#### dispatcherflush {#dispatcherflush}

The **dispatcherflush** module issues a dispatcher invalidation request for each page referencing the content fragment.

All **enabled** agents with the **serialization type = flush** will issue an invalidation request.

## Update of Content Fragment component {#update-of-content-fragment-component}

The update (or edit) of Content Fragment **component** on an AEM Page results in asynchronous post-processing that includes the inclusion of the Content Fragment component's content rendering in the Page's fulltext search index.
[ ![](assets/content-fragments--update-of-content-fragment-component.png)

Click to download

](/sites/using/content-fragments-delivery-considerations-article-understand/_jcr_content/main-pars/image.img.png/content-fragments--update-of-content-fragment-component.png)

1. An author modifies a Content Fragment **component** (CFc) on AEM Author.
1. A Sling POST Processor observes this modification and creates a Sling Job to process the change of the CFc.

   The Sling Job engages the AEM Content Fragment Update Processor Handler OSGi service, and looks up all registered Fragment Modules (Learn more about [Fragment Modules](#fragmentmodules)) via a resource-based module list.

   The default configuration for this use case only invokes the **prerender** fragment module.

1. The **prerender **fragment module renders the CFc via a service-user account and synthetic, internal HTTP Request and stores the HTML output into a property named **test** on the CFc resource.

    * Keep in mind the entire HTML output is stashed so its possible for HTML attributes to be included in the full text index for that Page. This HTML output also includes that of any inter-paragraph components that might exist; dragged by the author, or automatically injected via Content Fragment's inline mix-media support.

## Update of Content Fragment asset {#update-of-content-fragment-asset}

The modification of a Content Fragment **asset** on an AEM Page results in asynchronous post-processing that includes adjusting the Content Fragment component's (CFc) component resource structure to align to changes to CF paragraphs or mixed-media, and the inclusion of the Content Fragment component's content in the Page's fulltext search index.
[ ![](assets/content-fragments--update-of-content-fragment-asset.png)

Click to download

](/sites/using/content-fragments-delivery-considerations-article-understand/_jcr_content/main-pars/image_558095401.img.png/content-fragments--update-of-content-fragment-asset.png)

1. An author modifies a Content Fragment **asset** on AEM Author.
1. As part of processing the Contnet Fragment save request, the Content Fragment authoring servlet creates a Sling Job to process the changes to the Content Fragment asset..

   The Sling Job is created with the follow attributes:

    * Job topic = **dam/cfm/updateprocessor**
    * Event name = **fragmentupdate** 
    * Path =** /content/dam/path/to/content-fragment**

   This information is used by the AEM Content Fragment Update Processor to determine what work needs to be performed.

1. The Sling Job engages the AEM Content Fragment Update Processor Handler OSGi service, and looks up all registered Fragment Modules (Learn more about [Fragment Modules](#fragmentmodules)) via a resource-based module list.

   The default configuration for this use case invokes the **mixedmedia**, **inbetween** and **prerender** fragment modules.

1. The mixedmedia, inbetween, and prerender fragment modules inspect the Content Fragment in the context of the Content Fragment component (CFc) configuration and modify the CFc's component resource accordingly.

   See [Fragment Modules](#fragmentmodules) above to understand what each fragment module does.

## Replication of a Content Fragment {#replication-of-a-content-fragment}

The replication of a Content Fragment asset to AEM Publish results in async processing on AEM Pulish to ensure:

* referencing pages will render correctly based on (potentially) updated Content Fragment content
* the dispatcher cache is flushed to ensure the proper Page rendition that depends on the replicated Content Fragment is delivered.

>[!NOTE]
>
>As the flow below depicts, activations of Content Fragments can update Page, automatically changing how they appear to the end user.
>
>For example, 
>
>1. Let a Page that and a referenced Content Fragment (version 1) exist on AEM Publish
>1. A material change is made to the Content Fragment (version 2) on AEM Author (changing # of paragraphs, re-arranging inline mixed-media)
>1. The Content Fragment (version 2) is replicated from AEM Author to AEM Publish
>1. AEM Publish will process the activation of the Content Fragment (version 2) as described below, and re-build the Page's underlying Content Fragmment component resource structure, potentially adjusting Fragment Grid layout, or where inter-paragraph components display.
>
>When leveraging the Replication of Content Fragment functionality, it is important to be comfortable with how changes of the Content Fragment may effect how the referencing Pages display them. A custom governance workflow may be required to review how referencing Pages will be effected by the change to the Content Fragment.

![](assets/content-fragments--replication-of-content-fragment.png)

Click to download

>[!NOTE]
>
>This replication flow **ONLY** adheres to Content Fragment **ACTIVATIONS**. 
>
>DEACTIVATIONS are not processed as it is not possible to determine the type of resource deactivated (deleted). In order to support cache invalidations for deactivations a statlevel of 0 or 1 must be used, or a custom dispatcher cache flushing scheme is required.
>
>*Note, a dispatcher statlevel of 0 or 1 may incurr high cache invalidation rates putting extra stress on the AEM Publish tier. Please perform adequate perfomance tests against real use scenarios before setting a dispatcher statlevel of 0 or 1.*

1. AEM Author replicates a Content Fragment **asset** to AEM Publish.
1. As usual, a replication event is emitted for said replication, and noticed by a Content Fragment replication event handler.

   In parallel, denoted by **2`, **the normal dispatcher flush agents with "On Receive" enabled, issue the usual flush request for the Content Fragment asset resource itself.

1. If event handler determines the replication event payload is a candidate for Content Fragment processing, and creates a Sling Job to perform the work. The Sling Job is created with the follow attributes:

    * Job topic = **dam/cfm/updateprocessor**
    * Event name = **replication** 
    * Path =** /content/dam/path/to/content-fragment**

   This information is used by the AEM Content Fragment Update Processor to determine what work needs to be performed.

1. The Sling Job engages the AEM Content Fragment Update Processor Handler OSGi service, and looks up all registered Fragment Modules (Learn more about [Fragment Modules](#fragmentmodules)) via a resource-based module list.

   The default configuration for this use case invokes the **mixedmedia**, **inbetween,** **prerender **and** dispatcherflush** fragment modules.

1. The first 3 fragment modules processed, **mixedmedia**, **inbetween**, and **prerender**, update all Pages that reference the replicated Content Fragment and update the referencing Content Fragment component (CFc) resources to align with any changes to the Content Fragment's structure (number of paragraphs or inline mixed-media).
1. The last fragment modules, **dispatcherflush**, issues an dispatcher invalidation request for each Page that references the replicated Content Fragment.

   It is possible to remove the dispatcherflush fragment module from processing if a custom dispatcher cache invalidation scheme is better suited. To do this overlay the [Fragment Module processing configuration resource](#fragmentmodules) at:

    * **/mnt/overlay/dam/cfm/config/processing/publish/replication **

   to exclude the **dispatcherflush** name.

1. The dispatcher flush agents perform the invalidations to AEM Dispatcher in the usual manner.

## Performance considerations {#performance-considerations}

As depicted in the above flows, a key element of Content Fragment update processing is asynchronous, requires searched for referencing Pages, and updating referencing Pages.

The Content Fragment update processing load scales as:

**(# of content fragment updates/activations) X (# of referencing pages)**

* Authors are encouraged to minimize the # of Content Fragment "Saves" (# of content fragment updates)
* As the re-use of Content Fragment (# of reference pages) grows large, evaluate the impact.
* As the processing is mostly asynchronous (via Sling Jobs), based on the load, be aware changes may not immediately reflect on referencing Pages.

## Content Fragment update job code sample {#content-fragment-update-job-code-sample}

The following code can be used from within an OSGi Service to execute the AEM Content Fragment Update Processor on a specific Contnet Fragment.

*Remember the Fragment Modules to process are selected both by the executing AEM's runmode (ex. author or publish) and event name, so ensure the corrent combination is employed.*

```java
@Reference
private JobManager jobManager;

...
    
final String EVENT_TOPIC = "dam/cfm/updateprocessor";
String eventName = "fragmentchange " | "instanceupdate " | "replication"
    
final Map<String, Object> jobProperties = new HashMap<String, Object>();
jobProperties.put("event", eventName);
jobProperties.put("path", "/content/dam/path/to/content-fragment);

jobManager.addJob(EVENT_TOPIC, jobProperties);
```

## Supporting materials {#supporting-materials}

* [Download the Update of Content Fragment component diagram](/sites/using/content-fragments-delivery-considerations-article-understand/_jcr_content/main-pars/image.img.png/content-fragments--update-of-content-fragment-component.png)
* [Download the Update of Content Fragment asset diagram](/sites/using/content-fragments-delivery-considerations-article-understand/_jcr_content/main-pars/image_558095401.img.png/content-fragments--update-of-content-fragment-asset.png)
* [Download the Replication of a Content Fragment diagram](/sites/using/content-fragments-delivery-considerations-article-understand/_jcr_content/main-pars/image_1076988524.img.png/content-fragments--replication-of-content-fragment.png)

