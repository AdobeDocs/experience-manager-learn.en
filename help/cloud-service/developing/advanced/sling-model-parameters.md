---
title: Parameterize Sling Models from HTL
description: Learn how to pass in parameters from HTL to a Sling Model in AEM.
version: Cloud Service
topic: Development
feature: Sling Model
role: Developer
jira: KT-15923
level: Intermediate, Experienced
---

# Parameterize Sling Models from HTL

Adobe Experience Manager (AEM) offers a robust framework for building dynamic and adaptable web applications. One of its powerful features is the ability to parameterize Sling Models, enhancing their flexibility and reusability. This tutorial will guide you through creating a parameterized Sling Model and using it in HTL (HTML Template Language) to render dynamic content.

## HTL script

In this example, the HTL script sends two parameters to the `ParameterizedModel` Sling Model. The model manipulates these parameters in its `getValue()` method and returns the result for display.

This example passes two String parameters, however you can pass any type of value or object to the Sling Model, as long as the [Sling Model field type, annotated with `@RequestAttribute`](#sling-model-implementation) matches the type of object or value passed from HTL.

```html
<sly data-sly-use.myModel="${'com.example.core.models.ParameterizedModel' @ myParameterOne='Hello', myParameterTwo='World'}"
     data-sly-test.isReady="${myModel.isReady()}">

    <p>
        ${myModel.value}
    </p>

</sly>

<sly data-sly-use.placeholderTemplate="core/wcm/components/commons/v1/templates.html"
     data-sly-call="${placeholderTemplate.placeholder @ isEmpty=!isReady}">
</sly>
```

- **Parameterization:** The `data-sly-use` statement creates an instance of `ParameterizedModel` with `myParameterOne` and `myParameterTwo`.
- **Conditional Rendering:** `data-sly-test` checks if the model is ready before displaying content.
- **Placeholder Call:** The `placeholderTemplate` handles cases where the model is not ready.

## Sling Model implementation

Here's how you implement the Sling Model:

```java
package com.example.core.models.impl;

import org.apache.commons.lang3.StringUtils;
import org.apache.sling.api.SlingHttpServletRequest;
import org.osgi.service.component.annotations.Model;
import org.osgi.service.component.annotations.RequestAttribute;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

@Model(
    adaptables = { SlingHttpServletRequest.class },
    adapters = { ParameterizedModel.class }
)
public class ParameterizedModelImpl implements ParameterizedModel {
    private static final Logger log = LoggerFactory.getLogger(ParameterizedModelImpl.class);

    // Use the @RequestAttribute annotation to inject the parameter set in the HTL.
    // Note that the Sling Model field can be any type, but must match the type of object or value passed from HTL.
    @RequestAttribute
    private String myParameterOne;

    // If the HTL parameter name is different from the Sling Model field name, use the name attribute to specify the HTL parameter name
    @RequestAttribute(name = "myParameterTwo")
    private String mySecondParameter;

    // Do some work with the parameter values
    @Override
    public String getValue() {
        return myParameterOne + " " + mySecondParameter + ", from the parameterized Sling Model!";
    }

    @Override
    public boolean isReady() {
        return StringUtils.isNotBlank(myParameterOne) && StringUtils.isNotBlank(mySecondParameter);
    }
}
```

- **Model Annotation:** The `@Model` annotation designates this class as a Sling Model, adaptable from `SlingHttpServletRequest` and implementing the `ParameterizedModel` interface.
- **Request Attributes:** The `@RequestAttribute` annotation injects HTL parameters into the model.
- **Methods:** `getValue()` concatenates the parameters, and `isReady()` checks that the parameters are not blank.

The `ParameterizedModel` interface is defined as follows:

```java
package com.example.core.models;

import org.osgi.annotation.versioning.ConsumerType;

@ConsumerType
public interface ParameterizedModel {
    /**
     * Get an example string value from the model. This value is the concatenation of the two parameters.
     * 
     * @return the value of the model
     */
    String getValue();

    /**
     * Check if the model is ready to be used.
     *
     * @return {@code true} if the model is ready, {@code false} otherwise
     */
    boolean isReady();
}
```

## Example output

With parameters `"Hello"` and `"World"`, the HTL script generates the following output:

```html
<p>
    Hello World, from the parameterized Sling Model!
</p>
```

This demonstrates how parameterized Sling Models in AEM can be influenced based on input parameters provided via HTL.

