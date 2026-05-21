---
title: Customizing Component Icons in Adobe Experience Manager Sites
description: Component Icons allow authors to quickly identify a component with icons or meaningful abbreviations. Authors can now find locate the Components required to build out their Web experiences faster than ever.
version: Experience Manager 6.4, Experience Manager 6.5
feature: Core Components
topic: Development
role: User
level: Intermediate
doc-type: Technical Video
exl-id: 37dc26aa-0773-4749-8c8b-4544bd4d5e5f
duration: 379
TQID: https://experienceleague.adobe.com/k6Jkuua2O9x1F-fnOtTAAVzENwA4K3MHRptUNQAc8Uo
product_v2:
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: eb3ad9f8-54a2-45f3-abb1-d3976415a718
    internal-label: Personalization
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: e9001ce2-5245-4a8e-8601-dd958009072f
    internal-label: Web experience
---
# Customizing Component Icons {#developing-component-icons-in-aem-sites}

Component Icons allow authors to quickly identify a component with icons or meaningful abbreviations. Authors can now find locate the Components required to build out their Web experiences faster than ever.

>[!VIDEO](https://video.tv.adobe.com/v/16778?quality=12&learn=on)

The Component browser now displays in a consistent grey theme, displaying the:

* **[!UICONTROL Component Group]**
* **[!UICONTROL Component Title]**
* **[!UICONTROL Component Description]**
* **[!UICONTROL Component Icon]**
  * The first two letters of the Component Title *(default)*
  * Custom PNG image *(configured by a developer)*
  * Custom SVG image *(configured by a developer)*
  * CoralUI icon *(configured by a developer)*

## Component icon configuration options {#component-icon-configuration-options}

### Abbreviations {#abbreviations}

By default, the first 2 characters of component title (**[cq:Component]@jcr:title**) are used as the abbreviation. For example, if **[cq:Component]@jcr:title=Article List** the abbreviation would display as "**Ar**".

The abbreviation can be customized via the **[cq:Component]@abbreviation** property. While this value can accept more than 2 characters, it is recommended to limit the abbreviation to 2 characters to avoid any visual disturbance.

```plain

/apps/.../components/content/my-component
  - jcr:primaryType = "cq:Component"
  - abbreviation = "AL"

```

### CoralUI Icons {#coralui-icons}

CoralUI icons, provided by AEM, can be used for component icons. To configure a CoralUI icon, set a **[cq:Component]@cq:icon** property to the desired CoralUI icon's HTML icon attribute value (enumerated in the [CoralUI documentation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html).

```plain

/apps/.../components/content/my-component
  - jcr:primaryType = "cq:Component"
  - cq:icon = "documentFragment"

```

### PNG Images {#png-images}

PNG images can be used for component icons. To configure a PNG image as a component icon, add the desired image as a **nt:file** named **cq:icon.png** under the **[cq:Component]**.

The PNG should have a transparent background, or a background color set to **#707070**.

The PNG images are scaled to **20px by 20px**. However to accommodate retina displays **40px** by **40px** might be preferable.

```plain

/apps/.../components/content/my-component
  - jcr:primaryType = "cq:Component"
  + cq:icon.png
     - jcr:primaryType = "nt:file"

```

### SVG Images {#svg-images}

SVG images (vector-based) can be used for component icons. To configure a SVG image as a component icon, add the desired SVG as a **nt:file** named **cq:icon.svg** under the **[cq:Component]**.

SVG images should have a background color set to **#707070** and a size of **20px by 20px.**

```plain

/apps/.../components/content/my-component
  - jcr:primaryType = "cq:Component"
  + cq:icon.svg
     - jcr:primaryType = "nt:file"

```

## Additional Resources {#additional-resources}

* [Available CoralUI Icons](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html)
