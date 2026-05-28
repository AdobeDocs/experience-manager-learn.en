---
title: Build, Deploy and Test the countries component
description: Build,Deploy and Test
solution: Experience Manager, Experience Manager Forms
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
topic: Development
feature: Adaptive Forms
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
jira: KT-16517
exl-id: ab9bd406-e25e-4e3c-9f67-ad440a8db57e
TQID: https://experienceleague.adobe.com/mltgOQQ3Et-TA3-Y-jBJuhFMl6lE58fFOlzqk8N8JBQ
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
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
# Build, Deploy and Test the countries component

To build all the modules and deploy the `all` package to a local instance of AEM, run in the project root directory the following command:

```
mvn clean install -PautoInstallSinglePackage
```

## Test the component

To integrate the Countries component into your AEM Forms Cloud Ready instance and configure it, follow these steps:

* Extract the contents of the [countries](assets/countries.zip) zip file. Each file should contain the data for a specific continent. 
* Upload the json files under content/dam/corecomponent.This is the location the code looks for the json files.If you want to store the JSON files in a different location, you will need to update the Java code in the CountriesDropDownImpl class. Specifically, update the path in the init() method where the JSON files are loaded.For example, if you want to store the JSON files in content/dam/mydata/, update the path like this

```java
String jsonPath = "/content/dam/mydata/" + getContinent() + ".json"; // Update path accordingly
```

* Login to Your AEM Forms Cloud Ready Instance
* Create an Adaptive Form and drop the Countries component on to the form
* Configure the Countries component using the dialog editor and set the various properties including the continent
![Countries component](assets/select-continent.png)
* Preview the form and ensure the countries drop down works as expected
