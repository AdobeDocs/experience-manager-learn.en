---
title: Installing IntelliJ community edition
description: Install and  import the AEM project into IntelliJ
solution: Experience Manager
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
topic: Development
jira: KT-8843
exl-id: 34840d28-ad47-4a69-b15d-cd9593626527
duration: 43
TQID: https://experienceleague.adobe.com/jUCktQTHjcExAFWtZEa27mpIgJ9-5js-yx1Z-mzZkCs
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Installing IntelliJ

Install [IntelliJ community edition](https://www.jetbrains.com/idea/download/#section=windows). You can accept the default settings while suggested during the installation.

## Import the AEM Project

* Launch IntelliJ
* Import the AEM project you created in the earlier step. After project is imported your screen should look something like this ![aem-banking-app](assets/aem-banking-app.png). You will typically work with core,ui.apps,ui.config and ui.content sub projects.
* If you do not see the maven and terminal window, please go to view->Tools Window and select Maven and Terminal

## Add the fonts module

If you want to make use of custom fonts in your PDF file, you will need to push the custom fonts to the AEM Forms CS instance. Please follow the following steps

* Create a folder called **fonts** in C:\CloudManager\aem-banking-application
* Extract the contents of [font.zip](assets/fonts.zip) into the newly created fonts folder
* Included in the fonts module are some custom fonts.You can add your organization's custom fonts to the C:\CloudManager\aem-banking-application\fonts\src\main\resources folder of the fonts module
* Open the C:\CloudManager\aem-banking-application\pom.xml file
* Add the following line  ```<module>fonts</module>``` in the modules section of the pom.xml
* Save your pom.xml
* Refresh the aem-banking-application project in IntelliJ

Project structure with fonts module
![fonts-module](assets/fonts-module.png)

Fonts module included in the projects POM
![fonts-pom](assets/fonts-module-pom.png)

## Next Steps

[Setup Git](./setup-git.md)
