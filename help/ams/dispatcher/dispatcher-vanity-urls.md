---
title: Dispatcher vanity URLs
description: Understand how AEM deals with vanity URLs and additional techniques using rewrite rules to map content closer to the edge of delivery.
version: Cloud Service
topic: Administration, Performance
feature: Dispatcher
role: Admin
level: Beginner
thumbnail: xx.jpg
---

# Dispatcher Vanity URLs

[Table of Contents](./overview.html)

[<- Previous: Dispatcher Flushing](./dispatcher-flushing.md)

## Overview

This document will help you understand how AEM deals with vanity urls and some additional techniques using rewrite rules to map content closer to the edge of delivery

## What are Vanity URLs

When you have content that lives in a folder structure that makes sense it doesn't always live in a URL that's easy to reference.  Vanity URLs are like shortcuts.  Shorter or unique URLs that reference where the real content lives.

An example: `/aboutus` pointed at `/content/we-retail/us/en/about-us.html`

AEM Authors have the option to set vanity url properties on a piece of content in AEM and publish it.

For this feature to work you'll have to adjust the Dispatcher filters to allow the vanity through.  This becomes unreasonable to do with adjusting the Dispatcher configuration files at the rate that authors would need to setup these vanity page entries.

For this reason the Dispatcher module has a feature to auto-allow anything listed as a vanity in the content tree.


## How it works

### Authoring Vanity URLs

The author visits a page in AEM and visits the page properties and add's entries in the vanity url section.

Once they save their changes and activate the page the vanity is now assigned to this page.

#### Touch UI:

![Drop down dialog menu for AEM authoring UI on site editor screen](assets/dispatcher-vanity-urls/aem-page-properties-drop-down.png "aem-page-properties-drop-down")![aem page properties dialog page](assets/aem-page-properties.png "aem-page-properties")

#### Classic Content Finder:

![AEM siteadmin classic ui sidekick page properties](assets/aem-page-properties-sidekick.png "aem-page-properties-sidekick")![Classic UI page properties dialog box](assets/aem-page-properties-classic.png "aem-page-properties-classic")

<div style="color: #000;border-left: 6px solid #2196F3;background-color:#ddffff;"><b>Note:</b>
Please understand this is very prone to name space issues.

Vanity entries are global to all pages, this is just one of the short comings you have to plan for workarounds we'll explain a few of those later.
</div>

## Resource Resolving / Mapping

Each vanity entry is sling map entry for an internal redirect.

Thes maps are visible by visiting the AEM instances Felix console ( `/system/console/jcrresolver` )

Here is a screenshot of the a map entry created by a vanity entry:
![console screenshot of a vanity entry in the resource resolving rules](assets/vanity-resource-resolver-entry.png "vanity-resource-resolver-entry")

In the above example when we ask the AEM instance to visit `/aboutus` it will resolve to `/content/we-retail/us/en/about-us.html`

## Dispatcher auto-allow filters

The Dispatcher in a secure state filters out requests at the path `/` through the Dispatcher because that's the root of the JCR tree.

It's important to make sure publishers are only allowing content from the `/content` and other safe paths etc..  and not paths like `/system` etc..

Here is the rub, vanity urls live at the base folder of `/` so how do we allow them to reach the publishers while staying secure?

Simple dispatcher has an auto-filter allow mechanism and you have to install an AEM package and then configure the Dispatcher to point to that packages page.

[https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/granite/vanityurls-components](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/granite/vanityurls-components)

Dispatcher has a configuration section in it's farm file:

```
/vanity_urls { 
    /url    "/libs/granite/dispatcher/content/vanityUrls.html" 
    /file   "/tmp/vanity_urls" 
    /delay  300 
}
```

This configuration tells the Dispatcher to fetch this URL from it's AEM instance it fronts every 300 seconds to fetch the list of items we want to allow through.

It stores it's cache of the response in the `/file` argument so in this example `/tmp/vanity_urls`

So if you visit the AEM instance at the URI you'll see what it fetches:
![screenshot of the content rendered from /libs/granite/dispatcher/content/vanityUrls.html](assets/vanity-url-component.png "vanity-url-component")

It's literally a list, super simple

## Rewrite Rules as Vanity Rules

Why would we mention using rewrite rules instead of the default mechanism built into AEM as describe above?

Explained simply, namespace issues, performance, and higher level logic that can be handled better.

Let's go over an example of the vanity entry `/aboutus` to it's content `/content/we-retail/us/en/about-us.html` using Apache's `mod_rewrite` module to accomplish this.

```
RewriteRule ^/aboutus /content/we-retail/us/en/about-us.html [PT,L,NC]
```

This rule will look for the vanity `/aboutus` and fetch the full path from the renderer with the PT flag (Pass Through).

It also will stop processing all the other rules L flag (Last) which means it won't have to traverse a huge list of rules like JCR Resolving has to do.

Along with not having to proxy the request and wait for the AEM publisher to respond these two elements of this method make it much more performant.

Then the icing on the cake here is the NC flag (No Case-Sensitive) meaning if a customer flubs the URI with `/AboutUs` instead of `/aboutus` it will still work and allow the right page to fetched.

To create a rewrite rule to do this you would create a configuration file on the Dispatcher (example: `/etc/httpd/conf.d/rewrites/examplevanity_rewrite.rules`) and include it in the `.vhost` file that handles the domain that needs these vanity urls to apply.

Here is an example code snippet of the include inside `/etc/httpd/conf.d/enabled_vhosts/we-retail.vhost`

```
<VirtualHost *:80> 
 ServerName weretail.com 
 ServerAlias www.weretail.com 
        ........ SNIP ........ 
 <IfModule mod_rewrite.c> 
  ReWriteEngine on 
  LogLevel warn rewrite:info 
  Include /etc/httpd/conf.d/rewrites/examplevanity_rewrite.rules 
 </IfModule> 
        ........ SNIP ........ 
</VirtualHost>
```

## Which Method and Where

Using AEM to control vanity entries has the following benefits
- Authors can create them on the fly
- They live with the content and can be packaged up with the content

Using `mod_rewrite` to control vanity entries has the following benefits
- Faster to resolve content
- Closer to the edge of end user content requests
- More extensibility and options to control how content is mapped on other conditions
- Can be case insensitive

Use both methods but here's the advice and criteria on which one to use when:
- If the vanity is temporary and has low levels of traffic planned then use the AEM built in feature
- If the vanity is a staple endpoint that doesn't change often and has frequent use then use a `mod_rewrite` rule.
- If the vanity namespace (for example: `/aboutus`) has to be reused for lots of brands on the same AEM instance then use rewrite rules.

<div style="color: #000;border-left: 6px solid #2196F3;background-color:#ddffff;"><b>Note:</b>

If you want to use the AEM vanity feature and avoid namespace you can make a naming convention.  Using vanity urls that nested like `/brand1/aboutus`, `brand2/aboutus`, `brand3/aboutus`.
</div>

[Next -> Common Logging](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17914.html)