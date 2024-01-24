---
title: Using items load path to populate drop down list
description: Configure and populate a drop down list to read values from a crx node
feature: Adaptive Forms
version: 6.4,6.5
jira: KT-10961
topic: Development
role: Developer
level: Beginner
last-substantial-update: 2022-09-20
thumbnail: item-load.jpg
exl-id: 89c486c8-95c3-4cd4-bf8e-a1b3558f17d6
duration: 36
---
# Item Load Property in AEM Forms

Configure and populate drop down list using the item load path property.
The Item Load Path field allow an author to provide a url from which it loads the options available in a dropdown list.
To create such a node in crx please follow the steps mentioned below:
* Login to crx
* Create a node called assets(you can name this node as per your requirement) type sling:folder under content.
* Save
* Click on the newly created assets node and set its properties as shown below
* You will need to create a property of type String called assettypes(you can name it as per your requirement).Make sure the property is a multivalue. Provide the values that you want and save.
![item-load-path](assets/item-load-path-crx.png)

To load these values in your drop down list, provide the following path in the item load path property  **/content/assets/assettypes**

The sample package can be [downloaded from here](assets/item-load-path-package.zip)
