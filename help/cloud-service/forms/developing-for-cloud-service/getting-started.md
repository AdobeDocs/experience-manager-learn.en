---
title: Installing the pre-requisites
description: Install the necessary software to setup your development environment
solution: Experience Manager
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
topic: Development
jira: KT-8842
exl-id: 274018b9-91fe-45ad-80f2-e7826fddb37e
duration: 44
TQID: https://experienceleague.adobe.com/A62LozEol5TpitGp51anglzIaQILhKfX2XHiudSK-Xc
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
# Installing the required software

This tutorial will guide you through the steps needed to create an AEM Forms project,synchronize the AEM Forms project with your local AEM instance using IntelliJ and repo tool. You will also learn how to add your project to the local git repository and push the local git repository to the cloud manager repository.





This tutorial will refer to this folder structure going forward.

* [Install JDK 21](https://www.oracle.com/java/technologies/downloads/#java21).
* [Maven](https://maven.apache.org/guides/getting-started/windows-prerequisites.html).For example if you have installed Maven in c:\maven folder, you will need to create an environment variable called M2_HOME with value C:\maven\apache-maven-3.6.0. Then add M2_HOME\bin to the path and save your setting.

## Create Maven project using AEM Project Archetype
 
* Create a folder called **cloudmanager**(you can give it any name) in your c drive
* Open your command prompt window and navigate to **c:\cloudmanager**
* Execute the following command. You may have to change the DarchetypeVersion=56 depending on the [latest version](https://github.com/adobe/aem-project-archetype/releases). The latest version was 56 at the time of writing this article. 

```bash
mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.3.1:generate -D archetypeGroupId=com.adobe.aem -D archetypeArtifactId=aem-project-archetype -D archetypeVersion="56" -D appTitle=BankingApplication -D appId=bankingapplication -D groupId=com.aem.bankingapplication -D includeFormsenrollment="y" -D aemVersion="cloud" -DartifactId="aem-banking-application"
```

* Execute the command by hitting enter key.If everything goes correctly you should see build success message.

## Next Steps

[Installing IntelliJ](./intellij-set-up.md)