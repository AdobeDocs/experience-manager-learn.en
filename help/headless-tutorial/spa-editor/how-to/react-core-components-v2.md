---
title: How to use AEM React Editable Components v2
description: Learn how to use AEM React Editable Components v2 to power a React app.
version: Cloud Service
topic: Headless
feature: SPA Editor
role: Developer
level: Intermediate
kt: 10900
thumbnail: kt-10900.jpeg
---

# How to use AEM React Editable Components v2

AEM provides [AEM React Editable Components v2](https://www.npmjs.com/package/@adobe/aem-react-editable-components), an Node.js-based SDK that allows the creation of React components, that support in-context component editing using AEM SPA Editor.

+ [npm module](https://www.npmjs.com/package/@adobe/aem-react-editable-components)
+ [Github project](https://github.com/adobe/aem-react-editable-components)
+ [Adobe documentation](https://experienceleague.adobe.com/docs/experience-manager-65/developing/spas/spa-reference-materials.html)


For more details and code samples for AEM React Editable Components v2 review the technical documentation:

+ [Integration with AEM documentation](https://github.com/adobe/aem-react-editable-components/tree/master/src/core)
+ [Editable component documentation](https://github.com/adobe/aem-react-editable-components/tree/master/src/components)
+ [Helpers documentation](https://github.com/adobe/aem-react-editable-components/tree/master/src/api)

## AEM pages

AEM React Editable Components work with both SPA Editor or Remote SPA React apps. Content populating the editable React components, must be exposed via AEM pages that extend the [SPA Page component](https://experienceleague.adobe.com/docs/experience-manager-64/developing/headless/spas/spa-page-component.html). AEM components, that maps to editable React components, must implement AEM's [Component Exporter framework](https://experienceleague.adobe.com/docs/experience-manager-65/developing/components/json-exporter-components.html) - such as [AEM Core WCM Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html).


## Dependencies

Ensure that the React app is running on Node.js 14+.

The minimal set of dependencies for the React app to use AEM React Editable Components v2 are: `@adobe/aem-react-editable-components`, `@adobe/aem-spa-component-mapping`, and  `@adobe/aem-spa-page-model-manager`.


+ `package.json`

```json
{
  ...
  "dependencies": {
    "@adobe/aem-react-editable-components": "^2.0.1",
    "@adobe/aem-spa-component-mapping": "^1.1.1",
    "@adobe/aem-spa-page-model-manager": "^1.4.4",
    ...
  },
  ...
}
```

>[!WARNING]
>
> [AEM React Core WCM Components Base](https://github.com/adobe/aem-react-core-wcm-components-base) and [AEM React Core WCM Components SPA](https://github.com/adobe/aem-react-core-wcm-components-spa) are not compatible with AEM React Editable Components v2.

## SPA Editor

When using the AEM React Editable Components with a SPA Editor-based React app, the AEM `ModelManager` SDK, as the SDK:

1. Retrieves content from AEM
1. Populates the React Edible components with AEM's content

Wrap the React app with an initialized ModelManager, and render the React app. The React app should contain one instance of the `<Page>` component exported from `@adobe/aem-react-editable-components`. The `<Page>` component has logic to dynamically create React components based on the `.model.json` provided by AEM.

+ `src/index.js`

```javascript
import { Constants, ModelManager } from '@adobe/aem-spa-page-model-manager';
import { Page } from '@adobe/aem-react-editable-components';
...
document.addEventListener('DOMContentLoaded', () => {
  ModelManager.initialize().then(pageModel => {
    const history = createBrowserHistory();
    render(
      <Router history={history}>    
        <Page
          history={history}
          cqChildren={pageModel[Constants.CHILDREN_PROP]}
          cqItems={pageModel[Constants.ITEMS_PROP]}
          cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]}
          cqPath={pageModel[Constants.PATH_PROP]}
          locationPathname={window.location.pathname}
        />
      </Router>,
      document.getElementById('spa-root')
    );
  });
});
```

The `<Page>` is passed as the AEM page's representation as JSON, via the `pageModel` provided by the `ModelManager`. The `<Page>` component dynamically creates React components for objects in the `pageModel` by matching the `resourceType` with a React component that registers itself to the resource type via `MapTo(..)`.

## Editable components

The `<Page>` is passed the AEM page's representation as JSON, via the `ModelManager`. The `<Page>` component then dynamically creates React components for each object in the JSON by matching the JS object's `resourceType` value with a React component that registers itself to the resource type via the component's `MapTo(..)` invocation. For example, the following would be used to instantiate an instance 

+ `HTTP GET /content/.../home.model.json`

```json
...
    ":items": {
        "example_123": {
                  "id": "example-a647cec03a",
                  "message": "Hello from an authored example component!",
                  ":type": "wknd-examples/components/example"
                }
    } 
...
```

The above JSON provided by AEM could be used to dynamically instantiate and populate an editable React component.

```javascript
import React from "react";
import { EditableComponent, MapTo } from "@adobe/aem-react-editable-components";

/**
 * The component's EditConfig is used by AEM's SPA Editor to determine if and how authoring placeholders should be displayed.
 */
export const ExampleEditConfig = {
  emptyLabel: "Example component",

  isEmpty: function (props) => {
    return props?.message?.trim().length < 1;
  }
};

/** 
 * Define a React component. The `props` passed into the component are derived form the
 * fields returned by AEM's JSON response for this component instance.
 */
export const Example = (props) => {
  // Return null if the component is considered empty. 
  // This is used to ensure an un-authored component does not break the experience outside the AEM SPA Editor
  if (ExampleEditConfig.isEmpty(props)) { return null; }

  // Render the component JSX. 
  // The authored component content is available on the `props` object.
  return (<p className="example__message">{props.message}</p>);
};

/**
 * Wrap the React component with <EditableComponent> to make it available for authoring in the AEM SPA Editor.
 * Provide the EditConfig the AEM SPA Editor uses to manage creation of authoring placeholders.
 * Provide the props that are automatically passed in via the parent component
 */
const EditableExample = (props) => {
  return (
    <EditableComponent config={ExampleEditConfig} {...props}>
      {/* Pass the ...props through to the Example component, since this is what does the actual component rendering */}
      <Example {...props} />
    </EditableComponent>
  );
};

/**
 * Map the editable component to a resourceType and export it as default.
 * If this component is embedded in another editable component (as show below), make sure to 
 * import the "non-editable" component instance for use in the embedding component.
 */
export default MapTo("wknd-examples/components/example")(EditableExample);
```

## Embedding components

Editable components can be reused and embedded in each other. There are two key considerations when embedding one editable component in another:

1. The JSON content from AEM for the embedding component must contain the content to satisfy the embedded components. This is done by creating a dialog for the AEM component that collects the requisite data. 
1. The "non-editable" instance of the React component must be embedded, rather than the "editable" instance which is wrapped with `<EditableComponent>`. The reason is, if the embedded component has the `<EditableComponent>` wrapper, the SPA Editor attempts to dress the inner component with the edit chrome (blue hover box), rather than the outer embedding component.

+ `HTTP GET /content/.../home.model.json`

```json
...
    ":items": {
        "embedding_456": {
                  "id": "example-a647cec03a",
                  "message": "Hello from an authored example component!",
                  "title": "A title for an embedding component!",
                  ":type": "wknd-examples/components/embedding"
                }
    } 
...
```

The above JSON provided by AEM could be used to dynamically instantiate and populate an editable React component that embeds another React component.


```javascript
import React from "react";
import { EditableComponent, MapTo } from "@adobe/aem-react-editable-components";
// Import the "non-editable" (not wrapped with <EditableComponent>) instance of the component 
import { Example } from "./Example.js";

export const EmbeddingEditConfig = {
  emptyLabel: "Embedding component",

  isEmpty: function (props) => {
    return props?.title?.trim().length < 1;
  }
};

export const Embedding = (props) => {
  if (EmbeddingEditConfig.isEmpty(props)) { return null; }

  return (<div className="embedding">
            {/* Embed the other components. Pass through props they need. */}
            <Example message={props.message}/>
            <p className="embedding__title">{props.title}</p>
        </div>);
};

const EditableEmbedding = (props) => {
  return (
    <EditableComponent config={EmbeddingEditConfig} {...props}>
      {/* Pass the ...props through to the Embedding component */}
      <Embedding {...props} />
    </EditableComponent>
  );
};

// Export as default the mapped EditableEmbedding
export default MapTo("wknd-examples/components/embedding")(EditableEmbedding);
```



