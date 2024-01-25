---
title: What is "The Dispatcher"
description: Understand what a Dispatcher actually is.
version: 6.5
topic: Administration
feature: Dispatcher
role: Admin
level: Beginner
thumbnail: xx.jpg
doc-type: Article
exl-id: 96c8dd09-e0a7-4abc-b04b-a805aaa67502
duration: 80
---
# What is "The Dispatcher"

[Table of Contents](./overview.md)

Starting with the basic description of what entails an AEM Dispatcher.

## Apache Web Server

Start with a basic Apache Web Server installation on a Linux server.

Basic explanation of what an Apache server does:

- Follows simple rules to serve files over the HTTP(s) protocols from its static document directory (`DocumentRoot`)
- Files stored in a default location (`/var/www/html`) are matched on requests and rendered in the requesting client's browser




## AEM specific module file (`mod_dispatcher.so`)

Then add a plugin to the Apache Web Server called the Dispatcher module

Basic explanation of what does the Adobe AEM Dispatcher module does:

- Augments the default file handler
- Filters out bad requests / Protects AEM's soft belly/endpoints
- Load balances if more than one renderer is present
- Allows for a living cache directory / Supports flushing of stagnant files
- It's the front door to all AMS installations and it delivers websites and assets to the client's browser
- It caches requests to re-serve at a much faster rate than an AEM server could accomplish on its own
- Much more...

## Web traffic workflow

Understanding which pieces are installed together to build a basic Dispatcher server leads us to have you understand the basic web traffic workflow for an Adobe Manager Services configuration.
 This should help you understand what role it plays in the chain of systems that serve content to visitors of your AEM content.

<b>Serving already cached content</b>

```
End User's Browser request 
    → Cloud Provider Load Balancer 
        → "The Dispatcher" 
            → Checks for cached request locally if found 
                → return request 
                    → End User
```

<b>Serving fresh content from AEM</b>

```
End User's Browser request 
    → Cloud Provider Load Balancer 
        → "The Dispatcher" 
            → Checks for cached request locally if NOT found 
                → requests content from publisher 
                    → publisher sends content 
                        → Dispatcher adds content to cache and replies 
                            → End User
```

<b>Content publishing/changes</b>

```
AEM Author User activates content 
    → Triggers content to be replicated to Publisher 
        → Publisher gets content and triggers the flush request to Dispatcher 
            → Dispatcher invalidates changed content 
            * Next request for that content will request fresh copy from publisher *
```

[Next -> Basic File Layout](./basic-file-layout.md)
