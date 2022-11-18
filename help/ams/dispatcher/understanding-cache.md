---
title: Dispatcher Understanding caching
description: Understand how the Dispatcher module operates it's cache.
topic: Administration, Performance
version: 6.5
role: Admin
level: Beginner
thumbnail: xx.jpg
---

# Understanding caching

[Table of Contents](./overview.md)

[<- Previous: Explanation of Configuration Files](./explanation-config-files.md)

This document will explain how Dispatcher caching happens and how it can be configured

## Caching Directories

We use the following default cache directories in our baseline installations

- Author
   - `/mnt/var/www/author`
- Publisher
   - `/mnt/var/www/html`

When each request traverses the Dispatcher the requests follow the configured rules to keep a locally cached version to response of eligible items

<div style="color: #000;border-left: 6px solid #2196F3;background-color:#ddffff;"><b>Note:</b>

We intentionally keep published workload separate from the author workload because when Apache looks for a file in the DocumentRoot it doesn't know which AEM instance it came from. So even if you have cache disabled in the author farm, if the author's DocumentRoot is the same as publisher it will serve files from the cache when present. Meaning you'll serve author files for from published cache and make for a really awful mix match experience for your visitors. 

Keeping separate DocumentRoot directories for different published content is also a very bad idea. You'll have to create multiple re-cached items that don't differ between sites like clientlibs as well as having to setup a replication flush agent for each DocumentRoot you setup. Increasing the amount of flush over head with each page activation. Rely on namespace of files and their full cached paths and avoid mutliple DocumentRoot's for published sites.
</div>

## Configuration Files

Dispatcher controls what qualifies as cacheable in the `/cache {` section of any farm file. 
In the AMS baseline configuration farms, you'll find our includes like shown below:


```
/cache { 
    /rules { 
        $include "/etc/httpd/conf.dispatcher.d/cache/ams_author_cache.any" 
    }
```


When creating the rules for what to cache or not, please refer to the documentation [here](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache)


## Caching author

There are a lot of implementations we've seen where people don't cache author content. 
They are missing out a huge upgrade in performance and responsiveness to their authors.

Let's talk about the strategy taken in configuring our author farm to cache properly.

Here is a base author `/cache {` section of our author farm file:


```
/cache { 
    /docroot "/mnt/var/www/author" 
    /statfileslevel "2" 
    /allowAuthorized "1" 
    /rules { 
        $include "/etc/httpd/conf.dispatcher.d/cache/ams_author_cache.any" 
    } 
    /invalidate { 
        /0000 { 
            /glob "*" 
            /type "allow" 
        } 
    } 
    /allowedClients { 
        /0000 { 
            /glob "*.*.*.*" 
            /type "deny" 
        } 
        $include "/etc/httpd/conf.dispatcher.d/cache/ams_author_invalidate_allowed.any" 
    } 
}
```

The important things to note here are that the `/docroot` is set to the cache directory for author.

<div style="color: #000;border-left: 6px solid #2196F3;background-color:#ddffff;"><b>Note:</b>

Make sure your `DocumentRoot` in the author's `.vhost` file matches the farms `/docroot` parameter
</div>

The cache rules include statement includes the file `/etc/httpd/conf.dispatcher.d/cache/ams_author_cache.any` which contains these rules:

```
/0000 { 
 /glob "*" 
 /type "deny" 
} 
/0001 { 
 /glob "/libs/*" 
 /type "allow" 
} 
/0002 { 
 /glob "/libs/*.html" 
 /type "deny" 
} 
/0003 { 
 /glob "/libs/granite/csrf/token.json" 
 /type "deny" 
} 
/0004 { 
 /glob "/apps/*" 
 /type "allow" 
} 
/0005 { 
 /glob "/apps/*.html" 
 /type "deny" 
} 
/0006 { 
 /glob "/libs/cq/core/content/welcome.*" 
 /type "deny" 
}
```

In an author scenario, content is changing all the time and on purpose. You only want to cache items that are not going to change frequently.
We have rules to cache `/libs` because they are part of the baseline AEM install and would change until you have installed a Service Pack, Cumulative Fix Pack, Upgrade, or Hotfix. So caching these elements make a ton of sense and really have huge benefits of the author experience of end users who use the site.

<div style="color: #000;border-left: 6px solid #2196F3;background-color:#ddffff;"><b>Note:</b>

Keep in mind that these rules also cache <b>`/apps`</b> this is where custom application code lives. If you're developing your code on this instance then it will prove to be very confusing when you save your file and don't see if reflect in the UI due to it serving up a cached copy. The intention here is that if you do a deployment of your code into AEM it too would be infrequent and part of your deployment steps should be to clear the author cache. Again the benefit is huge making your cacheable code run faster for the end users.
</div>


## ServeOnStale (AKA Serve on Stale / SOS)

This is one of those gems of a feature of the Dispatcher. If the publisher is under load or has become unresponsive it will typically throw a 502 or 503 http response code. If that happens and this feature is enabled the Dispatcher will be instructed to still serve what ever content is still in the cache as a best effort even if it's not a fresh copy. It's better to serve something if you've got it rather than just showing an error message that offers no functionality.

<div style="color: #000;border-left: 6px solid #2196F3;background-color:#ddffff;"><b>Note:</b>

Keep in mind that if the publisher renderer is having a socket timeout or 500 error message this feature will not trigger. If AEM is just unreachable this feature does nothing
</div>

This setting can be set in any farm but only makes sense to apply it on the publish farm files. Here is a syntax example of the feature enabled in a farm file:

```
/cache { 
    /serveStaleOnError "1"
```

## Caching pages with Query params / Arguments

<div style="color: #000;border-left: 6px solid #2196F3;background-color:#ddffff;"><b>Note:</b>

One of the normal behaviors of the Dispatcher module is that if a request has a query parameter in the URI (typically shown like `/content/page.html?myquery=value`) it will skip caching the file and go directly to the AEM instance. It's considering this request a dynamic page and shouldn't be cached. This can cause ill effects on cache efficiency.
</div>
<br/>

See this [article](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-should-have-its-ignoreurlparams-rules-configured-in-an-allow-list-manner) showing how important query parameters can affect your site performance.

By default you want to set the `ignoreUrlParams` rules to allow `*`.  Meaning that all query parameters are ignored and allow all pages to be cached regardless of the parameters used.

Here is an example where someone has built a social media deep link reference mechanism that uses the argument reference in the URI to know where the person came from.

<b>Ignorable Example:</b>

- https://www.we-retail.com/home.html?reference=android
- https://www.we-retail.com/home.html?reference=facebook

The page is 100% cacheable but doesn't cache because the arguments are present. 
Configuring your `ignoreUrlParams` as a allow list will help fix this issue:

```
/cache { 
    /ignoreUrlParams { 
        /0001 { /glob "*" /type "allow" }
    }
```

Now when the Dispatcher sees the request it will ignore the fact that the request has the `query` parameter of `?` reference and still cache the page

<b>Dynamic Example:</b>

- https://www.we-retail.com/search.html?q=fruit
- https://www.we-retail.com/search.html?q=vegetables

Keep in mind that if you do have query parameters that make a page change it's rendered output then you'll need to excempt them from your ignored list and make the page un-cacheable again.  For example a search page that uses a query parameter changes the raw html rendered.

So here is the html source of each search:

`/search.html?q=fruit`:

```
<html>
...SNIP...
    <div id='results'>
        <div class='result'>
            Orange
        </div>
        <div class='result'>
            Apple
        </div>
        <div class='result'>
            Strawberry
        </div>
    </div>
</html>
```

`/search.html?q=vegetables`:

```
<html>
...SNIP...
    <div id='results'>
        <div class='result'>
            Carrot
        </div>
        <div class='result'>
            Cucumber
        </div>
        <div class='result'>
            Celery
        </div>
    </div>
</html>
```

If you visited `/search.html?q=fruit` first then it would cache the html with results showing fruit.

Then you visit `/search.html?q=vegetables` second but it would show results of fruit.
This is because the query parameter of `q` is being ignored in regards to caching.  To avoid this issue you'll need to take note of pages that render different HTML based on query parameters and deny caching for those.

Example:

```
/cache { 
    /ignoreUrlParams { 
        /0001 { /glob "*" /type "allow" }
        /0002 { /glob "q" /type "deny"  }
    }
```

Pages that use query parameters via Javascript will still fully function ignoring the paramters in this setting.  Because they don't change the html file at rest.  They use javascript to update the browsers dom realtime on the local browser.  Meaning that if you consume the query parameters with javascript it's highly likely you can ignore this parameter for page caching.  Allow that page to cache and enjoy the performance gain!

<div style="color: #000;border-left: 6px solid #2196F3;background-color:#ddffff;"><b>Note:</b>

Keeping track of these pages does require some upkeep but is well worth the performance gains.  You can ask your CSE to run a report on your websites traffic to give you a list of all pages using query parameters over the last 90 days for you to analyze and make sure you know which pages to look at and which query paramters to not ignore
</div>
<br/>

## Caching response headers

It's pretty obvious that the Dispatcher caches `.html` pages and clientlibs (i.e. `.js`, `.css`), but did you know it can also cache particular response headers along side the content in a file with the same name but a `.h` file extension. This allows the next response to not only the content but the response headers that should go with it from cache.

AEM can handle more than just UTF-8 encoding

Sometimes items have special headers that help control cache TTL's encoding details, and last modified timestamps.

These values when cached are stripped by default and the Apache httpd webserver will do it's own job of processing the asset with it's normal file handling methods, which normally is limited to mime type guessing based on file extensions.

If you have the Dispatcher cache the asset and the desired headers you can expose the proper experience and assure the all the details make it to the clients browser.

Here is an example of a farm with the headers to cache specified:

```
/cache { 
 /headers { 
  "Cache-Control" 
  "Content-Disposition" 
  "Content-Type" 
  "Expires" 
  "Last-Modified" 
  "X-Content-Type-Options" 
 } 
}
```


In the example they have configured AEM to serve up headers the CDN looks for to know when to invalidate it's cache. Meaning now AEM can properly dictate which files get invalidated based on headers.

<div style="color: #000;border-left: 6px solid #2196F3;background-color:#ddffff;"><b>Note:</b>

Keep in mind you cannot use regular expressions or glob matching. It's a literal list of the headers to cache. Only put in a list of the literal headers you want it to cache.
</div>


## Auto-Invalidate Grace Period

On AEM systems that have a lot of activity from authors that do alot of page activations you can have a race condition where repeat invalidations occur. Heavily repeated flush requests are un-necessary and you can build in some tolerance to not repeat a flush until the grace period has cleared.

### Example of how this works:

If you have 5 request to invalidate `/content/exampleco/en/` all happen within a 3 second period.

With this feature off you'd invalidate the cache directory `/content/exampleco/en/` 5 times

With this feature on and set to 5 seconds it would invalidate the cache directory `/content/exampleco/en/` <b>once</b>

Here is an example syntax of this feature being configured for 5 second grace period:

```
/cache { 
    /gracePeriod "5"
```

## TTL Based Invalidation

A newer feature of the Dispatcher module was `Time To Live (TTL)` based invalidation options for cached items. When an item gets cached it looks for the presence of cache control headers and generates a file in the cache directory with the same name and a `.ttl` extension.

Here is an example of the feature being configured in the farm configuration file:

```
/cache { 
    /enableTTL "1"
```

<div style="color: #000;border-left: 6px solid #2196F3;background-color:#ddffff;"><b>Note:</b>
Keep in mind that AEM still needs to be configured to send TTL headers for Dispatcher to honor them. Toggling this feature only enables the Dispatcher to know when to remove the files that AEM has send cache control headers for. If AEM doesn't start sending TTL headers then Dispatcher won't do anything special here.
</div>

## Cache Filter Rules

Here is an example of a baseline configuration for which elements to cache on a publisher:

```
/cache{ 
    /0000 { 
        /glob "*" 
        /type "allow" 
    } 
    /0001 { 
        /glob "/libs/granite/csrf/token.json" 
        /type "deny" 
    }
```

We want to make our published site greedy as possible and cache everything.

If there is elements that break the experience when cached you can add rules to remove the option to cache that item. As you see in the example above the csrf tokens shouldn't ever be cached and have been excluded. Further details on writing these rules can be found [here](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache)

[Next -> Using and Understanding Variables](./variables.md)