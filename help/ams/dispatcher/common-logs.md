---
title: AEM Dispatcher Common Logs
description: Take a look at common log entries from the Dispatcher and learning what they mean and how to address them.
version: 6.5
topic: Administration, Performance
feature: Dispatcher
role: Admin
level: Beginner
thumbnail: xx.jpg
exl-id: 7fe1b4a5-6813-4ece-b3da-40af575ea0ed
---
# Common Logs

[Table of Contents](./overview.md)

[<- Previous: Vanity URLs](./disp-vanity-url.md)

## Overview

Document will describe common log entries you'll see and what they mean and how to deal with them.

## GLOB warning

Sample Log Entry:

```
Fri Jul 20 03:35:09 2018 W pid 8300 (tid 139937910880384) /etc/httpd/conf/publish-filters.any:5: Allowing requests with globs is considered unsafe.
Please consult the documentation at 'https://www.adobe.com/go/docs_dispatcher_config_en' on how to use attributes 
method/url/query/protocol/path/selectors/extension/suffix instead.
```

Since Dispatcher module 4.2.x they started discouraging people to use the following type of matches in their filters file:

```
/0041 { /type "allow" /glob "* *.css *"   }
```

Instead, it's better to use the new syntax like:

```
/0041 { /type "allow" /url "*.css" }
```

Or even better to not match on a wildcard matcher at all:

```
/0041 { /type "allow" /extension "css" }
```

Doing either of the suggested methods would get rid of that error message from the logs.

## Filter Rejects


<div style="color: #000;border-left: 6px solid #2196F3;background-color:#ddffff;"><b>Note:</b>
These entries don't always show up even if rejections are happening if the log level is set too low. Set it to Info or debug to assure you can see if the filters are rejecting the requests.
</div>

Sample Log entry:

```
Fri Jul 20 17:25:48 2018 D pid 25939 (tid 139937517123328) Filter rejects: GET /libs/granite/core/content/login.html HTTP/1.1
```

or:

```
Fri Jul 20 22:16:55 2018 I pid 128803 "GET /system/console/" ! - 8ms publishfarm/-
```

<div style="color: #000;border-left: 6px solid red;background-color:#ddffff;"><b>Caution:</b>

Understand that the Dispatcher's rules were set to filter out that request. In this case the page attempted to be visited was rejected on purpose and we wouldn't want to do anything with this.
</div>

If your log looks like this entry:

```
Fri Jul 20 17:26:47 2018 D pid 20051 (tid 139937517123328) Filter rejects: 
GET /etc/designs/exampleco/fonts/montserrat-regular/montserrat-regular-webfont.eot HTTP/1.1
```

That's letting us know that our design file `.eot` is being blocked and we will want to fix that.
So we should look at our filters file and add the following line to allow `.eot` files through

```
/0011 { /type "allow" /method "GET" /extension 'eot' /path "/etc/designs/*" }
```

This would allow the file through and stop this from logging.
If you want to see what's being filtered out you can run this command on your log file:

```
$ grep "Filter rejects\|\!" /var/log/httpd/dispatcher.log | awk 'match($0, /\/.*\//, m){ print m0 }' | awk '{ print $1 }'| sort | uniq -c | sort -rn
```

## Timeouts from render

Socket timeout sample log entry:

```
Fri Jul 20 22:31:15 2018 W pid 3648 Unable to connect socket to 10.43.3.40:4502: Connection timed out 
Fri Jul 20 22:31:15 2018 W pid 3648 Unable to connect to any backend in farm authorfarm
```

This occurs when you have the wrong IP address configured in the renders section of your farm. That or the AEM instance stopped responding or listening and the Dispatcher can't reach it.

Check your firewall rules and that the AEM instance is running and healthy.

Gateway timeout sample log entries:

```
Fri Jul 20 22:32:42 2018 I pid 3648 "GET /favicon.ico" 502 - 54034ms authorfarm/- 
Fri Jul 20 22:35:45 2018 I pid 3648 "GET /favicon.ico" 503 - 54234ms authorfarm/-
```

This means the AEM instance had an open socket it could reach and timed out with the response. This means your AEM instance was too slow or un-healthy and Dispatcher reached it's configured timeout settings in the render section of the farm. Either increase the timeout setting or get your AEM instance healthy.

## Caching level

Sample Log entry:

```
Fri Jul 20 23:00:19 2018 I pid 16004 (tid 140134145820416) Current cache hit ratio: 87.94 %
```

This means your fetching from render level vs from cache is measured. You want to hit 80+ percent from cache, and you should follow the help [here](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html%3Flang%3Den):

To get this number as high as possible.

<div style="color: #000;border-left: 6px solid #2196F3;background-color:#ddffff;"><b>Note:</b>
Even if you have your cache settings in the farm file to cache everything you might be flushing too often or too agressively that can cause a lower percentage cache hit ratio to occur
</div>

## Missing Directory

Sample log entry:

```
Fri Jul 20 14:02:43 2018 E pid 4728 (tid 140662586435328) Unable to create parent directory /mnt/var/www/author/libs/dam/content/asseteditors/formitems.overlay.infinity.json/application: Not a directory
```

This will typically show up when an item is being fetched while a cache clear is occurring at the same time.

That or the document root directory has bad permissions on it or the wrong SELinux file context on the folder that is denying apache from creating the new needed sub-directories.

For permission issues look at the permissions of the documentroot and make sure they look similar to:

```
dispatcher$ ls -Z /var/www/
drwxr-xr-x+ apache apache system_u:object_r:httpd_sys_content_t:s0 html
```

## Vanity URL not found

Sample log entry:

```
Thu Sep 27 17:35:11 2018 D pid 18936 Checking vanity URLs 
Thu Sep 27 17:35:11 2018 D pid 18936 Vanity URL file (/tmp/vanity_urls) not found, fetching... 
Thu Sep 27 17:35:11 2018 W pid 18936 Unable to fetch vanity URLs from 10.43.0.42:4503/libs/granite/dispatcher/content/vanityUrls.html: remote server returned: HTTP/1.1 404 Not Found
```

This error occurs when you've configured your Dispatcher to use the dynamic auto-filter allow vanity URLs, but not finished the setup by installing the package on the AEM renderer.

To fix this please install the vanity url feature pack on the AEM instance and allow it to be ready by the anonymous user. Details [here](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17463.html%3Flang%3Den)

A working vanity URL set up looks like this:

```
Thu Sep 27 17:40:29 2018 D pid 21844 Checking vanity URLs 
Thu Sep 27 17:40:29 2018 D pid 21844 Vanity URL file (/tmp/vanity_urls) not found, fetching... 
Thu Sep 27 17:40:29 2018 D pid 21844 Loaded 18 vanity URLs from file /tmp/vanity_urls
```

## Missing Farm

Sample log entry:

```
Wed Nov 13 17:17:26 2019 W pid 19173:tid 140542738364160 No farm matches host 'we-retail.com', selected last farm 'publishfarm'
```

This error indicates that from all of the farm files available in `/etc/httpd/conf.dispatcher.d/enabled_farms/` they weren't able to find a matching entry from the `/virtualhost` section.

The farm files match traffic based on the domain name or path in which the request came in with. It uses glob matching and if it doesn't match then you've either not configured your farm properly, typo'd the entry into the farm, or have the entry missing entirely. When the farm doesn't match any entries it finally just defaults to the last farm included in the stack of farm files included. In this example it was `999_ams_publish_farm.any` which is named the generic name of publishfarm.

Here is an example farm file `/etc/httpd/conf.dispatcher.d/enabled_farms/300_weretail_publish_farm.any` that's been reduced to highlight the relevant parts.

## Item Served from

Sample log entry:

```
Tue Nov 26 16:41:34 2019 I pid 9208 (tid 140112092391168) "GET /content/we-retail/us/en.html" - + 24034ms publishfarm/0
```

The page was fetched via the GET http method for the content `/content/we-retail/us/en.html` and it took 24034 milliseconds. The part we wanted to pay attention to is at the very end `publishfarm/0`. You'll see that it targeted and matched the `publishfarm`. The request was fetched from render 0. Meaning that this page had to be requested from AEM then cached. Now let's request this page again and see what happens to the log.

[Next -> Read-Only Files](./immutable-files.md)
