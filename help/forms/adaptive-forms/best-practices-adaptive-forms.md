---
title: Naming conventions and best practices to be followed when creating adaptive forms
description: Naming conventions and best practices to be followed when creating adaptive forms
feature: Adaptive Forms
version: 6.4,6.5
topic: Development
role: Developer
level: Beginner
exl-id: fbfc74d7-ba7c-495a-9e3b-63166a3025ab
last-substantial-update: 2020-09-10
duration: 74
---
# Best Practices

Adobe Experience Manager (AEM) forms can help you transform complex transactions into simple, delightful digital experiences. The following document describes some additional best practices that need to be followed when developing Adaptive Forms. This document is meant to be used in conjunction with [this document](https://helpx.adobe.com/experience-manager/6-3/forms/using/adaptive-forms-best-practices.html#Overview)

## Naming Conventions

* **Panels**
  * Panel names are camel case starting with an upper case character.

* **Form Fields**
  * Field names are camel case starting with a lower case character.
  * Do not start field names with numbers
  * Do not include dashes "-" in your names. These will equate to a minus sign in your code and will act as operators in your code.
  * Names can contain letters, digits, underscores, and dollar signs.
  * Names must begin with a letter
  * Names are case-sensitive
  * Reserved words (like JavaScript keywords) cannot be used as names. Watch out for other AF-specific reserved words such   as "panel","name".
  * Do not include dashes "-" in your names
* **Developing Forms**
  * Form fragments should be considered when developing large forms. Enable lazy loading of form fragments for faster load   times
  * **DataModel**
    * Associating Adaptive Form with appropriate data model is recommended

  * **Object Events**
    * Code related to the visibility of an object should always be placed in the visibility event of said object.
  * **Script**
    * If the code you are writing inside an Adaptive Form extends past 5 visible lines, you must move your code to a Client Library. Ideally, add your function to the client library and then add the appropriate jsdoc tags to allow the function to be visible in the Adaptive Form rule editor.
