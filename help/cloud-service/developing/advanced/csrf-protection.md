---
title: CSRF protection
description: Learn how to generate and add AEM CSRF tokens to allowed POST, PUT, and Delete requests to AEM for authenticated users.
version: Experience Manager as a Cloud Service
feature: Security
topic: Development, Security
role: Developer
level: Intermediate
doc-type: Code Sample
last-substantial-update: 2023-07-14
jira: KT-13651
thumbnail: KT-13651.jpeg
exl-id: 747322ed-f01a-48ba-a4a0-483b81f1e904
duration: 125
---
# CSRF protection

Learn how to generate and add AEM CSRF tokens to allowed POST, PUT, and Delete requests to AEM for authenticated users.

AEM requires a valid CSRF token to be sent for __authenticated__ __POST__, __PUT, or __DELETE__ HTTP requests to both AEM Author and Publish services. 

The CSRF token is not required for __GET__ requests, or __anonymous__ requests.

If a CSRF token is not sent with a POST, PUT, or DELETE request, AEM returns a 403 Forbidden response, and AEM logs the following error:

```log
[INFO][POST /path/to/aem/endpoint HTTP/1.1][com.adobe.granite.csrf.impl.CSRFFilter] isValidRequest: empty CSRF token - rejecting
[INFO][POST /path/to/aem/endpoint HTTP/1.1][com.adobe.granite.csrf.impl.CSRFFilter] doFilter: the provided CSRF token is invalid
```

See the [documentation for more details on AEM's CSRF protection](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/csrf-protection.html).


## CSRF client library

AEM provides a client library that can be used to generate and add CSRF tokens XHR and form POST requests, via patching core prototype functions. The functionality is provided by the `granite.csrf.standalone` client library category.

To use this approach, add `granite.csrf.standalone` as a dependency to the client library loading on your page. For example, if you are using the `wknd.site` client library category, add `granite.csrf.standalone` as a dependency to the client library loading on your page.

## Custom form submission with CSRF protection

If the use of [`granite.csrf.standalone` client library](#csrf-client-library) is not amenable to your use case, you can manually add a CSRF token to a form submission. The following example shows how to add a CSRF token to a form submission.

This code snippet demonstrates how on form submit, the CSRF token can be fetched from AEM, and added to a form input named `:cq_csrf_token`. Because the CSRF token has a short life, it's best to retrieve and set the CSRF token immediately before the form is submitted, ensuring its validity.

```javascript
// Attach submit handler event to form onSubmit
document.querySelector('form').addEventListener('submit', async (event) => {
    event.preventDefault();

    const form = event.target;
    const response = await fetch('/libs/granite/csrf/token.json');
    const json = await response.json();
    
    // Create a form input named ``:cq_csrf_token`` with the CSRF token.
    let csrfTokenInput = form.querySelector('input[name=":cq_csrf_token"]');
    if (!csrfTokenInput?.value) {
        // If the form does not have a CSRF token input, add one.
        form.insertAdjacentHTML('beforeend', `<input type="hidden" name=":cq_csrf_token" value="${json.token}">`);
    } else {
        // If the form already has a CSRF token input, update the value.
        csrfTokenInput.value = json.token;
    }
    // Submit the form with the hidden input containing the CSRF token
    form.submit();
});
```

## Fetch with CSRF protection

If the use of [`granite.csrf.standalone` client library](#csrf-client-library) is not amenable to your use case, you can manually add a CSRF token to an XHR or fetch requests. The following example shows how to add a CSRF token to an XHR made with fetch.

This code snippet demonstrates how to fetch a CSRF token from AEM, and add it to a fetch request's `CSRF-Token` HTTP request header. Because the CSRF token has a short life, it's best to retrieve and set the CSRF token immediately before the fetch request is made, ensuring its validity.
 
```javascript
/**
 * Get CSRF token from AEM.
 * CSRF token expire after a few minutes, so it is best to get the token before each request.
 * 
 * @returns {Promise<string>} that resolves to the CSRF token.
 */
async function getCsrfToken() {
    const response = await fetch('/libs/granite/csrf/token.json');
    const json = await response.json();
    return json.token;
}

// Fetch from AEM with CSRF token in a header named 'CSRF-Token'.
await fetch('/path/to/aem/endpoint', {
    method: 'POST',
    headers: {
        'CSRF-Token': await getCsrfToken()
    },
});
```

## Dispatcher configuration

When using CSRF tokens on AEM Publish service, the Dispatcher configuration must be updated to allow GET requests to the CSRF token endpoint. The following configuration allows GET requests to the CSRF token endpoint on the AEM Publish service. If this configuration is not added, the CSRF token endpoint returns a 404 Not Found response.

* `dispatcher/src/conf.dispatcher.d/filters/filters.any`

```
...
/0120 { /type "allow" /method "GET" /url "/libs/granite/csrf/token.json" }
...
```
