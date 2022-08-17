---
title: Add Editable Container Components to a Remote SPA
description: Learn how to add editable container components to a remote SPA that allow AEM authors drag and drop components into them.
topic: Headless, SPA, Development
feature: SPA Editor, Core Components, APIs, Developing
role: Developer, Architect
level: Beginner
kt: 7635
thumbnail: kt-7635.jpeg
exl-id: e5e6204c-d88c-4e79-a7f4-0cfc140bc51c
---
# Editable container components

[Fixed components](./spa-fixed-component.md) provide some flexibility for authoring SPA content, however this approach is rigid and requires developers to define the exact composition of the editable content. To support the creation of exceptional experiences by authors, SPA Editor supports the use of container components in the SPA. Container components allow authors to drag and drop allowed components into the container, and author them, just like they can in traditional AEM Sites authoring!

![Editable container components](./assets/spa-container-component/intro.png)

In this chapter, we add an editable container to the home view allowing authors to compose and layout rich content experiences using AEM React Core Components directly in the SPA.

## Update the WKND App 

To add a container component to the Home view:

+ Import the AEM React Editable Component's ResponsiveGrid component
+ Import and register AEM React Core Components (Text and Image) for use in the container component

### Import in the ResponsiveGrid container component

To place an editable area to the Home view, we must:

1. Import the ResponsiveGrid component from `@adobe/aem-react-editable-components` 
1. Register it using `withMappable` so developers can place it in the SPA
1. Also, register with `MapTo` so it can be reused in other Container components, effectively nesting containers.

To do this:

1. Open the SPA project in your IDE
1. Create a React component at `src/components/aem/AEMResponsiveGrid.js`
1. Add the following code to `AEMResponsiveGrid.js`

    ```
    // Import the withMappable API provided bu the AEM SPA Editor JS SDK
    import { withMappable, MapTo } from '@adobe/aem-react-editable-components';

    // Import the base ResponsiveGrid component
    import { ResponsiveGrid } from "@adobe/aem-react-editable-components";
    
    // The sling:resourceType for which this Core Component is registered with in AEM
    const RESOURCE_TYPE = "wcm/foundation/components/responsivegrid";

    // Create an EditConfig to allow the AEM SPA Editor to properly render the component in the Editor's context
    const EditConfig = {
        emptyLabel: "Layout Container",  // The component placeholder in AEM SPA Editor
        isEmpty: function(props) { 
            return props.cqItemsOrder == null || props.cqItemsOrder.length === 0;
        },                              // The function to determine if this component has been authored
        resourceType: RESOURCE_TYPE     // The sling:resourceType this SPA component is mapped to
    };

    // MapTo allows the AEM SPA Editor JS SDK to dynamically render components added to SPA Editor Containers
    MapTo(RESOURCE_TYPE)(ResponsiveGrid, EditConfig);

    // withMappable allows the component to be hardcoded into the SPA; <AEMResponsiveGrid .../>
    const AEMResponsiveGrid = withMappable(ResponsiveGrid, EditConfig);

    export default AEMResponsiveGrid;
    ```

The code is similar `AEMTitle.js` that [imported the AEM Reach Core Components' Title component](./spa-fixed-component.md).


The `AEMResponsiveGrid.js` file should look like:

![AEMResponsiveGrid.js](./assets/spa-container-component/aem-responsive-grid-js.png)

### Use the AEMResponsiveGrid SPA component

Now that AEM's ResponsiveGrid component is registered in and available for use within the SPA, we can place it in the Home view.

1. Open and edit `react-app/src/Home.js`
1. Import the `AEMResponsiveGrid` component and place it above the `<AEMTitle ...>` component.
1. Set the following attributes on the `<AEMResponsiveGrid...>` component
    + `pagePath = '/content/wknd-app/us/en/home'`
    + `itemPath = 'root/responsivegrid'`

    This instructs the `AEMResponsiveGrid` component to retrieve its content from the AEM resource:

    + `/content/wknd-app/us/en/home/jcr:content/root/responsivegrid`

    The `itemPath` maps to the `responsivegrid` node defined in the `Remote SPA Page` AEM Template and is automatically created on new AEM Pages created from the `Remote SPA Page` AEM Template.

    Update `Home.js` to add the `<AEMResponsiveGrid...>` component.

    ```
    ...
    import AEMResponsiveGrid from './aem/AEMResponsiveGrid';
    ...

    function Home() {
        return (
            <div className="Home">
                <AEMResponsiveGrid
                    pagePath='/content/wknd-app/us/en/home' 
                    itemPath='root/responsivegrid'/>

                <AEMTitle
                    pagePath='/content/wknd-app/us/en/home' 
                    itemPath='title'/>
                <Adventures />
            </div>
        );
    }
    ```

The `Home.js` file should look like:

![Home.js](./assets/spa-container-component/home-js.png)

## Create editable components

To get the full effect of the flexible authoring experience containers provide in SPA Editor. We've already create an editable Title component, but let's make a few more that allow authors to use Text and Image AEM WCM Core Components in the newly added container component.

### Text component

1. Open the SPA project in your IDE
1. Create a React component at `src/components/aem/AEMText.js`
1. Add the following code to `AEMText.js`

    ```
    import { withMappable, MapTo } from '@adobe/aem-react-editable-components';
    import { TextV2, TextV2IsEmptyFn } from "@adobe/aem-core-components-react-base";

    const RESOURCE_TYPE = "wknd-app/components/text";

    const EditConfig = {    
        emptyLabel: "Text",
        isEmpty: TextV2IsEmptyFn,
        resourceType: RESOURCE_TYPE
    };

    MapTo(RESOURCE_TYPE)(TextV2, EditConfig);

    const AEMText = withMappable(TextV2, EditConfig);

    export default AEMText;
    ```

The `AEMText.js` file should look like:

![AEMText.js](./assets/spa-container-component/aem-text-js.png)

### Image component

1. Open the SPA project in your IDE
1. Create a React component at `src/components/aem/AEMImage.js`
1. Add the following code to `AEMImage.js`

    ```
    import { withMappable, MapTo } from '@adobe/aem-react-editable-components';
    import { ImageV2, ImageV2IsEmptyFn } from "@adobe/aem-core-components-react-base";

    const RESOURCE_TYPE = "wknd-app/components/image";

    const EditConfig = {    
        emptyLabel: "Image",
        isEmpty: ImageV2IsEmptyFn,
        resourceType: RESOURCE_TYPE
    };

    MapTo(RESOURCE_TYPE)(ImageV2, EditConfig);

    const AEMImage = withMappable(ImageV2, EditConfig);

    export default AEMImage;
    ```

1. Create an SCSS file `src/components/aem/AEMImage.scss` that provides custom styles for the `AEMImage.scss`. These styles target the AEM React Core Component's BEM-notation CSS classes.
1. Add the following SCSS to `AEMImage.scss`

    ```
    .cmp-image__image {
        margin: 1rem 0;
        width: 100%;
        border: 0;
     }
    ```

1. Import `AEMImage.scss` in `AEMImage.js` 

    ```
    ...
    import './AEMImage.scss';
    ...
    ```

The `AEMImage.js` and `AEMImage.scss` should look like:

![AEMImage.js and AEMImage.scss](./assets/spa-container-component/aem-image-js-scss.png)

### Import the editable components

The newly created `AEMText` and `AEMImage` SPA components are referenced in the SPA, and are dynamically instantiated based on the JSON returned by AEM. To ensure that these components are available to the SPA, create import statements for them in `Home.js`

1. Open the SPA project in your IDE
1. Open the file `src/Home.js`
1. Add import statements for `AEMText` and `AEMImage`

    ```
    ...
    import AEMText from './components/aem/AEMText';
    import AEMImage from './components/aem/AEMImage';
    ...
    ```


The result should look like:

![Home.js](./assets/spa-container-component/home-js-imports.png)

If these imports are _not_ added, the `AEMText` and `AEMImage` code is not be invoked by SPA, and thus, the components are not registered against the provided resource types.

## Configuring the container in AEM

AEM container components use policies to dictate their allowed components. This is a critical configuration when using SPA Editor, since only AEM WCM Core Components that have mapped SPA component counterparts are render-able by the SPA. Ensure only the components which we've provided SPA implementations for are allowed:

+ `AEMTitle` mapped to `wknd-app/components/title`
+ `AEMText` mapped to `wknd-app/components/text`
+ `AEMImage` mapped to `wknd-app/components/image`

To configure the Remote SPA Page template's reponsivegrid container:

1. Log in to AEM Author
1. Navigate to __Tools > General > Templates > WKND App__
1. Edit __Report SPA Page__

    ![Responsive Grid policies](./assets/spa-container-component/templates-remote-spa-page.png)

1. Select __Structure__ in the mode switcher in the top right
1. Tap to select the __Layout Container__ 
1. Tap the __Policy__ icon in the popup bar

    ![Responsive Grid policies](./assets/spa-container-component/templates-policies-action.png)

1. On the right, under the __Allowed Components__ tab, expand __WKND APP - CONTENT__
1. Ensure only following are selected:
    + Image
    + Text 
    + Title

    ![Remote SPA Page](./assets/spa-container-component/templates-allowed-components.png)

1. Tap __Done__

## Authoring the container in AEM

After the SPA updated to embed the `<AEMResponsiveGrid...>`, wrappers for three AEM React Core components (`AEMTitle`, `AEMText`, and `AEMImage`), and AEM is updated with a matching Template policy, we can start authoring content in the container component.

1. Log in to AEM Author 
1. Navigate to __Sites > WKND App__
1. Tap __Home__ and select __Edit__ from the top action bar
    + A "Hello World" Text component displays, as this was automatically added when generating the project from the AEM Project archetype
1. Select __Edit__ from the mode-selector in the top right of the Page Editor
1. Locate the __Layout Container__ editable area beneath the Title
1. Open the __Page Editor's side bar__, and select the __Components view__
1. Drag the following components into the __Layout Container__
    + Image 
    + Title
1. Drag the components to reorder them to the following order:
    1. Title
    1. Image
    1. Text    
1. __Author__ the __Title__ component
    1. Tap the Title component, and tap the __wrench__ icon to __edit__ the Title component
    1. Add the following text:  
        + Title: __Summer is coming, let's make the most of it!__
        + Type: __H1__
    1. Tap __Done__
1. __Author__ the __Image__ component
    1. Drag an image in from the Side bar (after switching to the Assets view) on the Image component
    1. Tap the Image component, and tap the __wrench__ icon to edit
    1. Check the __Image is decorative__ checkbox
    1. Tap __Done__
1. __Author__ the __Text__ component
    1. Edit the Text component by tapping the Text component, and tapping the __wrench__ icon
    1. Add the following text:  
        + _Right now, you can get 15% on all 1-week adventures, and 20% off on all adventures that are 2 weeks or longer! At checkout, add the campaign code SUMMERISCOMING to get your discounts!_
    1. Tap __Done__

1. Your components are now authored, but stack vertically. 

    ![Authored components](./assets/spa-container-component/authored-components.png)

   Use AEM's Layout Mode to allow us to adjust the size and layout of the components.
    
1. Switch to __Layout Mode__ using the mode-selector in the top-right
1. __Resize__ the Image and Text components, such that  they are side by side
    + __Image__ component should be __8 columns wide__
    + __Text__ component should be __3 columns wide__

    ![Layout components](./assets/spa-container-component/layout-components.png)

1. __Preview__ your changes in AEM Page Editor
1. Refresh the WKND App running locally on [http://localhost:3000](http://localhost:3000) to see the authored changes!

    ![Container component in SPA](./assets/spa-container-component/localhost-final.png)


## Congratulations!

You've added a container component that allows for editable components to be added by authors to the WKND App! You now know how to:

+ Use the AEM React Editable Component's ResponsiveGrid component in the SPA
+ Register AEM React Core Components (Text and Image) for use in the SPA via the container component
+ Configure the Remote SPA Page template to allow the SPA-enabled Core Components
+ Add editable components to the container component
+ Author and layout components in SPA Editor

## Next Steps

The next step will be using this same technique to [add an editable component to an Adventure Details route](./spa-dynamic-routes.md) in the SPA.
