---
title: Style the left navigation tabs with icons
description: Add icons to indicate active and completed tabs
feature: Adaptive Forms
type: Tutorial
version: Experience Manager 6.5
topic: Development
role: Developer
level: Beginner
jira: KT-9359
exl-id: f7c1f991-0486-4355-8502-cd5b038537e3
last-substantial-update: 2019-07-07T00:00:00.000Z
duration: 68
TQID: https://experienceleague.adobe.com/b5B1PtYOm-0--YRWkkapT2sOrm3FXgNL835vToir4vA
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
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
