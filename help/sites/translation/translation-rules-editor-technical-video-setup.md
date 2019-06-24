---
title: Set up Translation Rules in AEM
seo-title: Setup Translation Rules in AEM
description: AEM 6.3 introduces a Translation Configuration UI to manage rules for translating content in AEM Sites. This video details the creation of a new translation rule for a custom component.
seo-description: AEM 6.3 introduces a Translation Configuration UI to manage rules for translating content in AEM Sites. This video details the creation of a new translation rule for a custom component.
uuid: 20955acd-ceae-4bff-b99b-b4bca5ae73a5
products: SG_EXPERIENCEMANAGER/6.3/SITES
topic-tags: language-support
discoiquuid: d659dd20-7619-48c7-8ada-b0cd6f314714
targetaudience: target-audience ongoing
index: y
internal: n
snippet: y
---

# Set up Translation Rules {#set-up-translation-rules-in-aem}

AEM 6.3 introduces a Translation Configuration UI to manage rules for translating content in AEM Sites. This video details the creation of a new translation rule for a custom component.

>[!VIDEO](https://video.tv.adobe.com/v/18135/?quality=9)

Translation rules identify content in AEM to be extracted for translation. Out of the box translation rules cover common use cases such as Text components and alt text for Image components. Depending on a projects translation requirements additional rules may be need. In general translation rules allow users to specify:

1. Properties that should be translated based on path and/or resource type
1. Filters for properties that should NOT be translated
1. Referenced content that should be translated (i.e Images or Content Fragments)

Introduced in 6.3 is a translation rules editor that will update the translation xml file. The Translation Configuration UI makes it easier to manage various translation rules and guards against typos when editing XML directly.

Access the Translation Configuration UI:

* **AEM Start Menu &gt; Tools &gt; General &gt; [Translation Configuration](http://localhost:4502/libs/cq/translation/translationrules/contexts.html)**

## Prior to AEM 6.3 {#prior-to-aem}

In prior AEM version translation rules were manually updated by editing an XML file located under the Translation workflow:

* `/etc/workflow/models/translation/translation_rules.xml`

For more detailed information about translation rules and capabilities see: [Identifying Content to Translate](https://docs.adobe.com/docs/en/aem/6-3/administer/sites/translation/tc-rules.html).
