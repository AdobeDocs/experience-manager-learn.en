---
title: Getting Started with AEM Sites Chapter 2 - Pages and Templates
seo-title: Getting Started with AEM Sites Chapter 2 - Pages and Templates
description: Understand the relationship between a base page component and editable templates. Understand how Core Components are proxied into a project. Two different templates are created. Core Components of Text, Image, and Title are used to author an initial page.
seo-description: Understand the relationship between a base page component and editable templates. Understand how Core Components are proxied into a project. Two different templates are created. Core Components of Text, Image, and Title are used to author an initial page.
uuid: 6a7e43fc-faf6-4e9c-95ee-09ec0d23956a
products: SG_EXPERIENCEMANAGER/6.4/SITES
products: SG_EXPERIENCEMANAGER/6.3/SITES
discoiquuid: 00822ac4-842f-4b36-a142-5da73303e094
targetaudience: target-audience new

---

# Chapter 2 - Pages and Templates {#creating-a-base-page-and-template}

Understand the relationship between a base page component and editable templates. Understand how Core Components are proxied into a project. Two different templates are created. Core Components of Text, Image, and Title are used to author an initial page.

## Prerequisites {#prerequisites}

This is Chapter 2 of the multi-part tutorial. **[Chapter 1 can be found here](chapter-1.md)** and an [overview can be found here](getting-started-wknd-tutorial-develop.md).

>[!NOTE]
>
> Note you will need Eclipse or an IDE setup. In this chapter and in the following chapter the Eclipse IDE with AEM Developer tool plugin will be used. **Follow the instructions here [to set up an integrated development environment](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/local-aem-dev-environment-article-setup.html#setup-integrated-env).** 

You can view Chapter 1 on [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-guides-wknd/tree/chapter-1/project-setup) or you can download the solution package: TBD

## Objective

1. Understand the underlying code that generates a page in AEM.
2. Add a custom Header to extend the page component.
3. Learn how to leverage Editable Templates.

## Inspect Base Page Component {#base-page}

The archetype has created a **component** to be used as a base for all Pages created. The base page is responsible for ensuring that global areas of the site are consistent. This includes loading of global CSS and Javascript, as well as the inclusion of code that will ensure the page can be edited using AEM authoring tools.

In Eclipse (or in the IDE of your choice) you will be viewing nodes beneath `/apps/wknd` in the **ui.apps** project.

1. View the folder beneath `/apps/wknd/components/structure` named **page**.

   The AEM project archetype creates a component named **page**. [Editable templates](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/page-templates-editable.html) will be used for the WKND site. The name **structure** matches a specific mode of Editable template and is the common convention when using Editable templates. Any component added into the structure folder indicates that the component is meant to be used when constructing a template, and not to be used when authoring a page.

   ![asset base page](assets/chapter-2/base-page.png)

2. View the properties of the **page** component:

   ![page component properties](assets/chapter-2/base-pageprops.png)

   |Name|Value|Description|
   |--- |--- |--- |
   |componentGroup|.hidden|indicates that this is not an author-able component|
   |jcr:title|WKND Site Page|title|
   |sling:resourceSuperType|core/wcm/components/page/v2/page|will inherit functionality from the Core Page component|
   |jcr:primaryType|cq:Component|primary node type (read-only)|

   The **sling:resourceSuperType** property is critical in that it allows the WKND's page component to inherit all of the functionality of the Core Component page component. This is the first example of something called the [Proxy Component Pattern](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/guidelines.html#ProxyComponentPattern). More information can be found [here.](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/guidelines.html)

## Create Header Component {#header-nav}

Next a Header component will be created to be integrated into the Base page. The goal is just to establish a basic structure, so the code will be minimal. In later tutorials this component will be built in full.

1. Create a node named **header** with node type of **cq:Component** beneath `/apps/wknd/components/structure`:

   ![create header component](assets/chapter-2/header-cmp.gif)

2. You may see an error like the following: ***Unable to validate node types since project aem-guides-wknd.ui.apps is not associated with a server or the server is not started***.

   ![unable to validate node type error](assets/chapter-2/unable-validate-error.png)

   Double check and ensure that the **aem-guides-wknd.ui.apps** project is associated with an AEM eclipse server and that the server is started.

   If you continue to encounter the error:

    1. Right+Click the **aem-guides-wknd.ui.apps** project in the [!UICONTROL **Project explorer**]
    2. Open [!UICONTROL **Properties**] `->` [!UICONTROL **Project Facets**]
    3. Uncheck [!UICONTROL **Dynamic Web Module**]

   This should resolve the error and you should then get a drop down of node types when creating new nodes.

   ![uncheck Dynamic Web Module](assets/chapter-2/uncheck-dynamic-web-module.png)

   Also ensure that the content sync root directory beneath the AEM tab is pointed to the jcr_root folder:

   ![jcr sync folder](assets/chapter-2/jcr-sync-folder.png)

3. Update the **header** component with additional JCR properties. Select the **header** component and then Right+Click in the JCR Properties panel to add new properties.

   Add the following properties to the header component.

   |Name|Type|Value|Tutorial Description (don't copy, info only)|
   |--- |--- |--- |--- |
   |componentGroup|String|WKND.Structure|All components meant for the structure of Templates will use this group.|
   |jcr:description|String|Page Header with navigation|description of component|
   |jcr:title|String|WKND Page Header|title|
   |jcr:primaryType|Name|cq:Component|primary node type|

    ![header properties](assets/chapter-2/header-props.png)

   >[!NOTE]
   >
   >**Pro Tip!**
   >
   >
   >You can Double+Click the component in the Project Explorer and edit the XML configuration directly. This is preferable when many edits must be made, but it can be error prone.

   ```xml

   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
    jcr:primaryType="cq:Component"
    componentGroup="WKND.Structure"
    jcr:description="Page Header with navigation"
    jcr:title="WKND Page Header"/>

   ```

4. Add a node named **cq:dialog** of type **nt:unstructured** beneath the **header** component:

   ![create node named cq:dialog](assets/chapter-2/create-dialog-node.png)

   ![cq:dialog created](assets/chapter-2/cq-dialog-created.png)

   Dialogs are the mechanism that allows content authors to update properties/logic of a component through a UI dialog. The full dialog and fields will be defined in later parts of the tutorial. In order to support baseline author functionality at a minimum a dialog placeholder is needed.

5. Add a **file** named **header.html** beneath the **header** component

   ![header.html file](assets/chapter-2/header-html-file.png)

   This file is is actually an [HTL](https://docs.adobe.com/docs/en/htl/docs/getting-started.html) script. There are a set of [global objects](https://docs.adobe.com/docs/en/htl/docs/global-objects.html) that are always available to HTL scripts within a component. **currentPage** represents the current content page. Using the dot notation .title a method named .getTitle() is called. This will print the current page's title. Conditional logic can be used to print out 'header' if the page title can't be found. The name of the file **header**.html is important for Sling resource resolution, as it matches the name of the component. More information about Sling resource resolution can be found [here](https://sling.apache.org/documentation/the-sling-engine/url-to-script-resolution.html).

   Add the following contents to the header.html file:

   ```html

   <!--/* Header Component for WKND Site */-->
   <header class="wknd-header">
    <div class="container">
     <a class="wknd-header-logo" href="#">WKND</a>
     <h1>${currentPage.title ? currentPage.title : 'header'}</h1>
    </div>
   </header>

   ```

6. Its a good idea to periodically publish to AEM to verify/test your code changes. With Eclipse AEM dev tools you can publish the **ui.apps** project from within Eclipse.

   You can also always publish using Maven. It is a good idea deploy using Maven as well since this will ultimately be how you deploy to a Dev/Production environment and Maven will also run through unit tests and other code style checks prior to installing.

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage -Padobe-public clean install
   [INFO] ------------------------------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ------------------------------------------------------------------------
   [INFO] Total time: 8.391 s
   [INFO] Finished at: 2019-03-19T12:00:47-07:00
   [INFO] Final Memory: 38M/568M
   [INFO] ------------------------------------------------------------------------

   ```

7. View the **header** node in CRXDE Lite after deploying code changes

   In [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp) verify that the header component has been pushed to your local AEM instance.

   ![page in CRXDE Lite](assets/chapter-2/crx-de.png)

## Inspect Proxy Components {#proxy-components}

AEM [Core Components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components) provide several basic building blocks for creating content. This includes Text, Image and Title and several other components. The AEM project archetype includes these in the WKND project automatically. 

Each component added has a **sling:resourceSuperType** property to point to the Core Component. This is known as [creating proxy components](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/using.html#create-proxy-components) and is the recommended way of using Core Components in your project.

1. Notice that several Core Components have already been included in the project in the **ui.apps** module beneath `/apps/wknd/components/content`. 

   Each component included will have a **sling:resourceSuperType** property that points to the equivalent Core Component. The exception is the **helloworld** component which is a sample component.

   ![Breadcrumb Component](assets/chapter-2/breadcrumb-component.png)
   *Breadcrumb Component for creating navigation breadcrumbs.*

   Notice the property **componentGroup** that is set to **WKND.Content**. **componentGroup** will be used by a template policy to determine if the component can be added to a page. More on this later in the chapter.

2. View the node beneath the `/components/content/image` component named **cq:editConfig** with a type of **cq:EditConfig**.

   The **cq:editConfig** defines various behavior including Drag+Drop functionality from the Asset Finder in the Sites Editor. It is a required configuration for the Image component.

   Notice the `cq:dropTargets/image/parameters` node. This tells AEM what component resource type to use when dragging an Image on to the page. If you are extending the Image component for custom component it will be important to update the **cq:editConfig**.

   ![image edit config](assets/chapter-2/image-edit-config.png)

3. Core Components also include a set of components for building HTML forms. These components are also proxied into the project, like the components under `/content`. Notice also that these components have a unique componentGroup.

   ![button component](assets/chapter-2/button-component.png)
   *Button form component*

## Update Empty Page Template Type {#template-type}

[Template Types](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/page-templates-editable.html#TemplateType) are effectively a template for a template. They are necessary in order to take advantage of AEM's Editable Template feature. Templates and Template Types are stored beneath **/conf**. The AEM project archetype creates a template type to get started with. Nodes in **/conf** can be updated in AEM directly via the UI. Thus any template related nodes are stored in the **ui.content** project.

There are 3 main areas of Editable Templates:

1. **Structure** - defines components that are a part of the template. These will not be editable by content authors.
2. **Initial Content** - defines components that the template will start with, these can be edited and/or deleted by content authors
3. **Policies** - defines configurations on how components will behave and what options authors will have available.

   Since Template Types can be thought of as a template of a template you will find the same structure for the template type. Examples of template type structures can be found beneath: **/libs/settings/wcm/template-types/**.

The AEM Project archetype creates an Empty Page Template Type to start with. We will update a few areas of the **Empty Page Template Type** in the **ui.content** module.

1. In the **ui.content** module view the **Empty Page Template Type** under: `/conf/wknd/settings/wcm/template-types/empty-page`.

2. Expand the **structure** node and select the **jcr:content** node.

   Note on the **jcr:content** node that the **sling:resourceType** points to the base page component (viewed earlier in the **ui.apps** module).

   ![empty page jcr:content properties](assets/chapter-2/empty-page-template-props.png)

3. Beneath `/conf/wknd/settings/wcm/template-types/empty-page/structure/jcr:content/cq:responsive/breakpoints` are nodes for Tablet and Phone breakpoints. These breakpoints will be used in conjunction with AEM's Responsive Grid feature in the next chapter. The default Tablet breakpoint is **1200**.

4. Update the Phone breakpoint from **650** to **768**:

   ![updated phone breakpoint](assets/chapter-2/phone-breakpoint.png)

5. Inspect the **jcr:content** node beneath `template-types/empty-page/initial`. Notice that the **jcr:content** node beneath the **initial** page also points back to the base page component inspected earlier.

   ![initial sling resource type](assets/chapter-2/template-initial-content.png)

6. Inspect the nodes beneath `template-types/empty-page/policies`. The policies node defines how policies will be mapped to various components. This structure is standard across template types and not unique to the wknd's empty page template type.

7. **(Optional)** Add a thumbnail for the Empty Page Template Type.

   Thumbnails are great! This thumbnail will show up for users in the AEM author environment in order to easily identify the Template Type. Recommended dimensions are 460 x 460.

   ![Sample thumbnail to use](assets/chapter-2/empty-page-thumbnail.png)

   1. Create a file named **thumbnail.png** (or save the above image and rename to **thumbnail.png**).
   2. Add the **thumbnail.png** file beneath `/conf/wknd/settings/wcm/template-types/empty-page`:

      ![thumbnail location](assets/chapter-2/template-thumbnail-location.png)

   3. Deploy the **ui.content** module to your local AEM instance using AEM Dev tools or your Maven skills.

8. The next part of the tutorial will take place within AEM.

## Create Article and Landing Page Templates {#article-template}

The AEM project archetype pre-created a sample Content Template. The next few steps will detail creating 2 new templates:

1. **Article Page Template**
2. **Landing Page Template**

This will take place in AEM. The short video below details the steps.

>[!NOTE]
>
> Note the role of creating a template being done as a development task. However once the implementation reaches a level of maturity, additional templates may be created by a select group of "power-users".

>[!VIDEO](https://video.tv.adobe.com/v/22102?quality=9)

Landing Page Template Thumbnail

![landing page template thumbnail](assets/chapter-2/landing-page-thumbnail.png)

### High-level instructions

Use the above video to complete the following tasks:

1. **Create Article Page Template and Landing Page Template**

   Each of these templates include a fixed **Header** component and an unlocked Layout Container. The Layout Container is configured with the following allowed components:

    * **Breadcrumb**
    * **Image**
    * **List**
    * **Text**
    * **Title**
    * **Layout Container**

   Reuse the Layout Container Policy from the Article Page Template on the Landing Page Template.

   ![article and landing page templates](assets/templates.png)

2. **Create the Home Page**

   The Home page should be created at `/content/wknd/en` (or the language locale of your choice). It should be created using the **Landing Page Template**.

   ![home page site admin](assets/chapter-2/home-page-siteadmin.png)

3. The First Article page should be created beneath the Home Page at `/content/wknd/en/first-article`. It should be created using the **Article Page Template**.

   ![site admin first article](assets/chapter-2/first-article-siteadmin.png)

4. In order to re-deploy these templates to other environments it is possible to make them part of source control. Use the Eclipse Dev Tools, as outlined in the video, to import the templates created in AEM into the **ui.content** module.

   ![eclipse import template](assets/chapter-2/eclipseimport-template.png)

## Inspect Content Root {#content-root}

The AEM project archetype created a content root for the WKND site automatically at **/content/wknd**. The content root defines the allowed templates for the site and is used to set other global configurations. By convention the content root is not intended to be the Home page for the site and instead will redirect to the true home page. It is a good idea to understand the properties on the content root.

1. View the following properties on the **jcr:content** node at `/content/wknd/jcr:content`:

|Name  |Type  |Value  |Description|
|---   |---   |---    |---        |
|cq:allowedTemplates | String[] | `/conf/wknd/settings/wcm/templates/.*` | Will allow any templates created under the WKND folder to be used |
|jcr:title | String | Wknd Site | Title |
| jcr:primaryType | Name | *cq:pageContent* | Primary node type |
| redirectTarget | String | `/content/wknd/en` | Redirect target |
| sling:redirectStatus | Long | 302 | HTTP Status code |
| sling:resourceType | String | `foundation/components/redirect` | Use foundation component for redirect |

   As you can see some of the properties such as **allowedTemplates** on the Content Root are critical to the behavior of the site. In many implementations root configurations such as this are saved into SCM to provide some baseline content structure. In other cases offline content packages are created and provide a similar role.

1. Using Eclipse Dev Tools, in the **ui.content module** Right + Click `/content/wknd` page and [!UICONTROL **Import from server...**].

   ![eclipse import content](assets/chapter-2/eclipse-import-content.png)

## Next Steps {#next-steps}

Next part in the tutorial:

* **[Getting Started with AEM Sites Chapter 3 - Client-Side Libraries and Responsive Grid](chapter-3.md)**
* View the finished code on [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-guides-wknd) or download the solution package:

## Help! {#help}

If you get stuck or have additional questions make sure to check out the [Experience League forums for AEM](https://forums.adobe.com/community/experience-cloud/marketing-cloud/experience-manager) or view existing [GitHub issues](https://github.com/Adobe-Marketing-Cloud/aem-guides-wknd/issues).

Didn't find what you were looking for? Think you found an error? Please file a [GitHub issue for the WKND project](https://github.com/Adobe-Marketing-Cloud/aem-guides-wknd/issues).