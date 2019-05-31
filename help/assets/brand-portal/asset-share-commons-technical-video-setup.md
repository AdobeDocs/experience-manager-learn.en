---
title: Introduction to Theming in Asset Share Commons
seo-title: Introduction to Theming in Asset Share Commons
description: Materials for both the functional and technical understanding Assets Share Commons
seo-description: Materials for both the functional and technical understanding Assets Share Commons
uuid: 68aceee7-92b5-4c43-ba4d-8ba0a8b0b292
contentOwner: dgonzale
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
products: SG_EXPERIENCEMANAGER/6.2/ASSETS
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
products: SG_EXPERIENCEMANAGER/Brand_Portal
discoiquuid: 328a24c7-7a4e-4e68-89c0-8e268fe53f0b
targetaudience: target-audience advance
---

# Introduction to Theming in Asset Share Commons {#asset-share-commons-theme}

A brief introduction to theming in Asset Share Commons. The video walks through the process of creating a new theme with a custom color scheme.

>[!VIDEO](https://video.tv.adobe.com/v/20572/?quality=9)

AIn this video a new theme will be created based on the Asset Share Commons Dark theme. The color scheme will match a custom logo to give the site a consistent look and feel.

## Theme Variables

``` java
/*******************************
         Theme Variables
*******************************/
 
/* Below is a condensed list of variables for easy updating of the theme */
 
/* Color Palette */
@primaryColor      : #560a63;
@secondaryColor    : #fc3096;
 
/* Text */
@fontName          : 'LatoWeb';
@fontSmoothing     : antialiased;
@headerFont        : @fontName, 'Helvetica Neue', Arial, Helvetica, sans-serif;
@pageFont          : @fontName, 'Helvetica Neue', Arial, Helvetica, sans-serif;
@textColor         : #D0D0D0;
 
 
/* Backgrounds */
@pageBackground      : #3C3C3C;
@sideBarBackground   : #363636;
 
/* Links */
@linkColor           : #FFFFFF;
@linkHoverColor      : @secondaryColor;
 
/* Buttons */
@buttonPrimaryColor      : #560a63; /* must be a value to prevent variable recursion*/
@buttonPrimaryColorHover : saturate(darken(@buttonPrimaryColor, 5), 10, relative);
 
/* Filters (Checkboxes,radio buttons, toggle, slider, dropdown, accordion colors)*/
@filterPrimaryColor      : @secondaryColor;
@filterPrimaryColorFocus : saturate(darken(@filterPrimaryColor, 5), 10, relative);
 
/* Label */
@labelPrimaryColor       : @primaryColor;
@labelPrimaryColorHover  : saturate(darken(@labelPrimaryColor, 5), 10, relative);
 
/* Menu */
@menuPrimaryColor        : @primaryColor;
 
/* Message */
@msgPositiveBackgroundColor : @secondaryColor;
@msgNegativeBackgroundColor : @red;
@msgInfoBackgroundColor: @midBlack;
@msgWarningBackgroundColor: @yellow;
```

Download [Custom Client Library Theme](assets/asc-theme-demo.zip)

## Additional Resources{#additional-resources}

* [Asset Share Commons release downloads](https://github.com/Adobe-Marketing-Cloud/asset-share-commons/releases)
* [ACS AEM Commons 3.11.0+ release downloads](https://github.com/Adobe-Consulting-Services/acs-aem-commons/releases)