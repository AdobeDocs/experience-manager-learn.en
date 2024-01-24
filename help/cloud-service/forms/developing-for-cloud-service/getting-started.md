---
title: Installing the pre-requisites
description: Install the necessary software to setup your development environment
solution: Experience Manager
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Cloud Service
topic: Development
jira: KT-8842
exl-id: 274018b9-91fe-45ad-80f2-e7826fddb37e
duration: 48
---
# Installing the required software

This tutorial will guide you through the steps needed to create an AEM Forms project,synchronize the AEM Forms project with your local AEM instance using IntelliJ and repo tool. You will also learn how to add your project to the local git repository and push the local git repository to the cloud manager repository.





This tutorial will refer to this folder structure going forward.

* [Install JDK 11](https://www.oracle.com/java/technologies/downloads/#java11-windows). I have downloaded jdk-11.0.6_windows-x64_bin.zip
* [Maven](https://maven.apache.org/guides/getting-started/windows-prerequisites.html).For example if you have installed Maven in c:\maven folder, you will need to create an environment variable called M2_HOME with value C:\maven\apache-maven-3.6.0. Then add M2_HOME\bin to the path and save your setting.

## Create Maven project using AEM Project Archetype
 
* Create a folder called **cloudmanager**(you can give it any name) in your c drive
* Open your command prompt window and navigate to **c:\cloudmanager**
* Copy and paste the content of the [text file](assets/creating-maven-project.txt) in your command prompt window. You may have to change the DarchetypeVersion=30 depending on the [latest version](https://github.com/adobe/aem-project-archetype/releases). The latest version was 30 at the time of writing this article. 
* Execute the command by hitting enter key.If everything goes correctly you should see build success message.

## Next Steps

[Installing IntelliJ](./intellij-set-up.md)