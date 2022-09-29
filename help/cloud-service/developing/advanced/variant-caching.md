---
title: Caching page variants with AEM as a Cloud Service
description: Learn how to set up and use AEM as a cloud service to support caching page variants.
role: Architect, Developer
topic: Development
feature: CDN Cache, Dispatcher
exl-id: fdf62074-1a16-437b-b5dc-5fb4e11f1355
---
# Caching page variants

Learn how to set up and use AEM as a cloud service to support caching page variants.

## Example use cases 

+ Any service provider who is offering a different set of service offerings and corresponding pricing options based on the user's geo location and the cache of pages with dynamic content should be managed at CDN and Dispatcher. 

+ A retail customer has stores across the country and each store has different offers based on where they are located and the cache of pages with dynamic content should be managed at CDN and Dispatcher. 

## Solution overview

+ Identify the variant key and the number of values it may have. In our example, we vary by US state, so the max number is 50. This is small enough to not cause problems with the variant limits at the CDN. [Review variant limitations section](#variant-limitations).

+ AEM code must set the cookie __"x-aem-variant"__ to the visitor's preferred state (eg. `Set-Cookie: x-aem-variant=NY`) on the initial HTTP request's corresponding HTTP response.

+ Subsequent requests from the visitor send that cookie (eg. `"Cookie: x-aem-variant=NY"`) and the cookie is transformed at the CDN level into a pre-defined header (i.e. `x-aem-variant:NY`) which is passed to the dispatcher.

+ An Apache rewrite rule modifies the request path to include the header value in the page URL as an Apache Sling Selector (eg. `/page.variant=NY.html`). This allows AEM Publish to serve different content based on the selector and the dispatcher to cache one page per variant.

+ The response sent by AEM Dispatcher must contain an HTTP response header `Vary: x-aem-variant`. This instructs the CDN to store different cache copies for different header values.

>[!TIP]
>
>Whenever a cookie is set (eg. Set-Cookie: x-aem-variant=NY) the response should not be cacheable (should have Cache-Control: private or Cache-Control: no-cache)

## HTTP request flow

![Variant Cache Request Flow](./assets/variant-cache-request-flow.png)

>[!NOTE]
>
>The initial HTTP request flow above must take place before any content is requested that uses variants.

## Usage

1. To demonstrate the feature, we will use [WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)'s implementation as an example. 

1. Implement a [SlingServletFilter](https://sling.apache.org/documentation/the-sling-engine/filters.html) in AEM to set `x-aem-variant` cookie on the HTTP response, with a variant value. 

1. AEM's CDN automatically transforms `x-aem-variant` cookie into an HTTP header of the same name. 

1. Add an Apache Web server mod_rewrite rule to your `dispatcher` project, that modifies the request path to include the variant selector.

1. Deploy the filter and rewrite rules using Cloud Manager.

1. Test the overall request flow. 

## Code Samples 

+ Sample SlingServletFilter to set `x-aem-variant` cookie with a value in AEM.

    ```
    package com.adobe.aem.guides.wknd.core.servlets.filters;

    import javax.servlet.*;
    import java.io.IOException;

    import org.apache.sling.api.SlingHttpServletRequest;
    import org.apache.sling.api.SlingHttpServletResponse;
    import org.apache.sling.servlets.annotations.SlingServletFilter;
    import org.apache.sling.servlets.annotations.SlingServletFilterScope;
    import org.osgi.service.component.annotations.Component;
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;


    // Invoke filter on  HTTP GET /content/wknd.*.foo|bar.html|json requests.
    // This code and scope is for example purposes only, and will not interfere with other requests.
    @Component
    @SlingServletFilter(scope = {SlingServletFilterScope.REQUEST},
            resourceTypes = {"cq:Page"},
            pattern = "/content/wknd/.*",
            extensions = {"html", "json"},
            methods = {"GET"})
    public class PageVariantFilter implements Filter {
        private static final Logger log = LoggerFactory.getLogger(PageVariantFilter.class);
        private static final String VARIANT_COOKIE_NAME = "x-aem-variant";

        @Override
        public void init(FilterConfig filterConfig) throws ServletException { }

        @Override
        public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
            SlingHttpServletResponse slingResponse = (SlingHttpServletResponse) servletResponse;
            SlingHttpServletRequest slingRequest = (SlingHttpServletRequest) servletRequest;

            // Check is the variant was previously set
            final String existingVariant = slingRequest.getCookie(VARIANT_COOKIE_NAME).getValue();

            if (existingVariant == null) {
                // Variant has not been set, so set it now
                String newVariant = "NY"; // Hard coding as an example, but should be a calculated value
                slingResponse.setHeader("Set-Cookie", VARIANT_COOKIE_NAME + "=" + newVariant + "; Path=/; HttpOnly; Secure; SameSite=Strict");
                log.debug("x-aem-variant cookie is set with the value {}", newVariant);
            } else {
                log.debug("x-aem-variant previously set with value {}", existingVariant);
            }

            filterChain.doFilter(servletRequest, slingResponse);
        }

        @Override
        public void destroy() { }
    }
    ```

+ Sample Rewrite rule in the __dispatcher/src/conf.d/rewrite.rules__ file which is managed as source code in Git, and deployed using Cloud Manager.

    ```
    ...

    RewriteCond %{REQUEST_URI} ^/us/.*  
    RewriteCond %{HTTP:x-aem-variant} ^.*$  
    RewriteRule ^([^?]+)\.(html.*)$ /content/wknd$1.variant=%{HTTP:x-aem-variant}.$2 [PT,L] 

    ...
    ```

## Variant limitations

+ AEM's CDN can manage up to 200 variations. That means the `x-aem-variant` header can have up to 200 unique values. For more information, review the [CDN configuration limits](https://docs.fastly.com/en/guides/resource-limits).

+ Care must be taken to ensure your chosen variant key never exceeds this number.  For instance, a user Id is not a good key as it would easily exceed 200 values for most websites, whereas the states/territories in a country are a better fit if there are less than 200 states in that country. 

>[!NOTE]
>
>When the variants exceed 200, the CDN will respond with "Too many variants" response instead of the page content.
