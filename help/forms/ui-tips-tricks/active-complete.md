---
title: Style the left navigation tabs with icons
description: Add icons to indicate active and completed tabs
feature: Adaptive Forms
type: Tutorial
version: 6.5
topic: Development
role: Developer
level: Beginner
jira: KT-9359
exl-id: f7c1f991-0486-4355-8502-cd5b038537e3
last-substantial-update: 2019-07-07
duration: 115
---
# Add icons to indicate active and completed tabs

When you have adaptive form with left tab navigation, you may want to display icons to indicate the status of the tab. For example, you want to show an icon to indicate active tab and icon to indicate completed tab as shown in the screenshot below.

![toolbar-spacing](assets/active-completed.png)

## Create an Adaptive Form

A simple Adaptive Form based on the Basic template and Canvas 3.0 theme was used to create the sample form.
The [icons used in this article](assets/icons.zip) can be downloaded from here.


## Style the Default State

Open the form in edit mode
Make sure you are in the style layer and select any tab(For example General tab).
You are in the default state when you open the style editor for the tab as shown in the screen shot below
![navigation-tab](assets/navigation-tab.png)

Set the CSS properties for the default state as shown below
| Category | Property Name  |  Property Value |
|:---|:---|:---|
| Dimensions and Position | Width | 50px |
| Text | Font Weight| Bold |
| Text | Color | #FFF |
|Text | Line Height| 3 |
|Text  | Text Align | Left | 
|Background| Color | #056dae |

Save your changes

## Style the Active State

Make sure you are in the Active state and style the following CSS properties

|  Category | Property Name  |  Property Value |
|:---|:---|:---|
| Dimensions and Position | Width | 50px |
| Text | Font Weight| Bold |
| Text | Color | #FFF |
|Text | Line Height| 3 |
|Text  | Text Align | Left | 
|Background| Color | #056dae |

Style the background image as shown in the screen shot below

Save your changes.



![active-state](assets/active-state.png)

## Style the Visited State

Make sure you are in the visited state and style the following properties

|  Category | Property Name  |  Property Value |
|:---|:---|:---|
| Dimensions and Position | Width | 50px |
| Text | Font Weight| Bold |
| Text | Color | #FFF |
|Text | Line Height| 3 |
|Text  | Text Align | Left | 
|Background| Color | #056dae |

Style the background image as shown in the screen shot below


![visited-state](assets/visited-state.png)

Save your changes

Preview the form and test the icons are working as expected.
