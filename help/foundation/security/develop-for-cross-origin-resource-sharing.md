---
title: Develop for Cross-Origin Resource Sharing (CORS) with AEM
description: A short example of leveraging CORS to access AEM content from an external web application via client-side JavaScript.
version: 6.4, 6.5
topic: Security, Development
role: Developer
level: Beginner
feature: Security
doc-type: Technical Video
exl-id: 867cf74e-44e7-431b-ac8f-41b63c370635
duration: 356
---
# Develop for Cross-Origin Resource Sharing (CORS)

A short example of leveraging [!DNL CORS] to access AEM content from an external web application via client-side JavaScript. This example uses the CORS OSGi configuration to enable CORS access on AEM. The OSGi configuration approach is viable when:

* A single origin is accessing AEM Publish content
* CORS access is required for AEM Author

If multi-origin access to AEM Publish is required, refer to [this documenation](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors.html?lang=en#dispatcher-configuration).

>[!VIDEO](https://video.tv.adobe.com/v/18837?quality=12&learn=on)

In this video:

* **www.example.com** maps to localhost via `/etc/hosts`
* **aem-publish.local** maps to localhost via `/etc/hosts`
* SimpleHTTPServer (a wrapper for [[!DNL Python]'s SimpleHTTPServer](https://docs.python.org/2/library/simplehttpserver.html)) is serving the HTML page via port 8000.
  * _No longer available in Mac App Store. Use similar such as [Jeeves](https://apps.apple.com/us/app/jeeves-local-http-server/id980824182?mt=12)._
* [!DNL AEM Dispatcher] is running on [!DNL Apache HTTP Web Server] 2.4 and reverse-proxying request to `aem-publish.local` to `localhost:4503`.

For more details, review [Understanding Cross-Origin Resource Sharing (CORS) in AEM](./understand-cross-origin-resource-sharing.md).

## www.example.com HTML and JavaScript

This Web page has logic that

1. Upon clicking the button
1. Makes an [!DNL AJAX GET] request to `http://aem-publish.local/content/we-retail/.../experience/_jcr_content.1.json`
1. Retrieves the `jcr:title` form the JSON response
1. Injects the `jcr:title` into the DOM

```xml
<html>
<head>
<script
  src="https://code.jquery.com/jquery-3.2.1.min.js"
  integrity="sha256-hwg4gsxgFZhOsEEamdOYGBf13FyQuiTwlAQgxVSNgt4="
  crossorigin="anonymous"></script>   
</head>
<body style="width: 960px; margin: 2rem auto; font-size: 2rem;">
    <button style="font-size: 2rem;"
            data="fn-getTitle">Get Title as JSON from AEM</button>
    <pre id="title">The page title AJAX'd in from AEM will injected here</pre>
    
    <script>
    $(function() { 
        
        /** Get Title as JSON **/
        $('body').on('click', '[data="fn-getTitle"]', function(e) { 
            $.get('http://aem-publish.local/content/we-retail/us/en/experience/_jcr_content.1.json', function(data) {
                $('#title').text(data['jcr:title']);
            },'json');
            
            e.preventDefault();
            return false;
        });
    });
    </script>
</body>
</html>
```

## OSGi factory configuration

The OSGi Configuration factory for [!DNL Cross-Origin Resource Sharing] is available via:

* `http://<host>:<port>/system/console/configMgr > [!UICONTROL Adobe Granite Cross-Origin Resource Sharing Policy]`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
    jcr:primaryType="sling:OsgiConfig"
    alloworigin="[https://www.example.com:8000]"
    alloworiginregexp="[]"
    allowedpaths="[/content/we-retail/.*]"
    exposedheaders="[]"
    maxage="{Long}1800"
    supportedheaders="[Origin,Accept,X-Requested-With,Content-Type,
Access-Control-Request-Method,Access-Control-Request-Headers]"
    supportedmethods="[GET]"
    supportscredentials="{Boolean}false"
/>
```

## Dispatcher configuration {#dispatcher-configuration}

### Allowing CORS request headers

To allow the required [HTTP request headers to passthrough to AEM for processing](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#specifying-the-http-headers-to-pass-through-clientheaders), they must be allowed in the Disaptcher's `/clientheaders` configuration.

```
/clientheaders {
   ...
   "Origin"
   "Access-Control-Request-Method"
   "Access-Control-Request-Headers"
}
```

### Caching CORS resposne headers
 
To allow the caching and serving of CORS headers on cached content, add following [/cache /headers configuration](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#caching-http-response-headers) to the AEM Publish `dispatcher.any` file.

```
/publishfarm {
    ...
    /cache {
        ...
        # CORS HTTP response headers
        # https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#the_http_response_headers
        /headers {
            ...
            "Access-Control-Allow-Origin"
            "Access-Control-Expose-Headers"
            "Access-Control-Max-Age"
            "Access-Control-Allow-Credentials"
            "Access-Control-Allow-Methods"
            "Access-Control-Allow-Headers"
        }
    ...
    }
...
}
```

**Restart the web server application** after making changes to the `dispatcher.any` file.

It is likely clearing the cache entirely is required to ensure headers are appropriately cached on the next request after a `/cache /headers` configuration update.

## Supporting materials {#supporting-materials}

* [Jeeves for macOS](https://apps.apple.com/us/app/jeeves-local-http-server/id980824182?mt=12)
* [Python SimpleHTTPServer](https://docs.python.o:qrg/2/library/simplehttpserver.html) (Windows/macOS/Linux compatible)

* [Understanding Cross-Origin Resource Sharing (CORS) in AEM](./understand-cross-origin-resource-sharing.md)
* [Cross-Origin Resource Sharing (W3C)](https://www.w3.org/TR/cors/)
* [HTTP Access Control (Mozilla MDN)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS)
