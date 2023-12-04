---
title: Accelerate content velocity with AEM style systems
description: Learn how to use AEM Style Systems to empower designers, content authors, and developers in your organization to create and deliver experiences at the speed and scale that your customers expect.
solution: Experience Manager
exl-id: 449cd133-6ab6-456e-a0ad-30e3dea9b75b
duration: 230
---
# Accelerate content velocity with AEM style systems

In this article, you learn how to use AEM-style systems to empower designers, content authors, and developers in your organization to create and deliver experiences at the speed and scale that your customers expect.

## Overview

AEM Style Systems have four key benefits:

* Template authors can define style classes in the content policy of a component or page
* Content authors are able to select styles to apply to an entire page or when editing a component on a page
* Components and templates are made more flexible by empowering authors to render alternative visual variations
* The need to develop a custom component and/or complex dialogs to present component variations is reduced or eliminated completely

## Initial setup and use

The 5-step setup is very similar to a standard component development workflow.

| **Leadership** | **Designer** | **Developer / Architect** | **Template Author** | **Content Author** |
| --- | --- | --- | --- | --- |
| Determines content and objectives for that component | Determines visual and experiential presentation of content | Develops CSS and JS to support experience; defines and provides class names to be used | Configures template policies for styled components by adding CSS class names defined by developers. User-friendly names should be leveraged for each style. | While authoring pages, applies styles as needed to achieve desired look and feel |

While this is the initial setup, many of our customers have achieved additional agility by streamlining this process, for example uploading their CSS into the DAM, which allows updates to styles without the need for deployment. Other customers have a fully featured set of utility classes, which allows them to develop components and styles that can then be leveraged without deployment or development.

Style systems come in a few different flavors:

1. Layout Styles

   * Multifaceted changes to design and layout

   * Used for well-defined and identifiable rendition

1. Display Styles
   * Minor variations that do not change the fundamental nature of the style

   * For example, changing color scheme, font, image orientation, etc.

1. Informational Styles

   * Show / hide fields

>[!NOTE]
>
>For a demo of these features, we recommend watching our [Customer Success webinar](https://adobecustomersuccess.adobeconnect.com/pob610c9mffjmp4/) with Will Brisbane and Joseph Van Buskirk.

## Best practices

* Solidify default style first
  * Layout and display of component when dropped on page prior to application of style systems
  * This should be the most used rendition
* Try to only show style options that have an effect when possible
  * If ineffective combinations are exposed, ensure they don&#39;t cause negative effects
  * E.g. A layout style that dictates image position and is accompanied by ineffective display style that control image position
* Opt for layout styles over combined display styles
  * Reduces number of permutations that must be quality checked
  * Ensures brand standards are adhered to
  * Simplifies authoring for content authors
  * Helps to create consistent site brand identity
* Be conservative with combined styles
  * Both across and within categories
* Allocate proper time to thoroughly test combined styles
  * Helps to avoid undesirable effects
* Minimize the number of style options and permutations
  * Too many options can lead to a lack of brand consistency for look and feel
  * Can cause confusion for content authors on which combinations are needed to achieve desired effect
  * Increases the permutations that must be quality checked
* Use business user-friendly style labels and categories
  * &quot;Blue&quot; and &quot;Red&quot; instead of &quot;Primary&quot; and &quot;Secondary
  * &quot;Card&quot; and &quot;Hero&quot; instead of &quot;Variation A&quot; and &quot;Variation B&quot;
  * This may be more of a generality for some customers; the design team, business team, and content team are very familiar with what their primary and secondary colors are or what variations they are testing. But for flexibility and any potential for future changes, using specific terms may be more efficient.

## Key takeaways

Style Systems reduce the need for complex dialogs but they are not a dialog replacement. They help simplify things but there may be some cases where you want to use component properties or dialog rather than creating a style system for it.

They can streamline processes from a development perspective. You can achieve multiple looks of the same content with one style system. Similarly, from an authoring perspective, rather than training authors, and authors having to remember which component to use in which palace, you can expedite the authoring velocity.

Things are simply cleaner. The HTML within the core components is highly verbose. Doing all of this at the CSS level makes the component builds quicker and the code is cleaner as well.

Finally, the use of Style Systems is more art than science. As we discussed, there are a number of best practices, but you will have flexibility in how customize your organization&#39;s setup.

For more information, check out our [Customer Success Webinar](https://adobecustomersuccess.adobeconnect.com/pob610c9mffjmp4/) with Will Brisbane and Joseph Van Buskirk.

Learn more about strategy and thought leadership at the [Customer Success](https://experienceleague.adobe.com/docs/customer-success/customer-success/overview.html) hub.
