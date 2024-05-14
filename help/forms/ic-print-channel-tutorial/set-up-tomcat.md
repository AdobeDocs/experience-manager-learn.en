---
title: Install and Configure Tomcat video
description: This is part 1 of multistep tutorial for creating your first interactive communications document.
feature: Interactive Communication
doc-type: Tutorial
version: 6.4,6.5
thumbnail: 37815.jpg
discoiquuid: 5f68be3d-aa35-4a3f-aaea-b8ee213c87ae
topic: Development
role: Developer
level: Beginner
exl-id: faa9ca2d-6cfa-4abf-be5e-3e549202853a
duration: 237
---
# Install and Configure Tomcat {#install-and-configure-tomcat}

In this part, we install TOMCAT and deploy the sampleRest.war file in TOMCAT. The REST endpoint exposed by this WAR file is the basis for our Data Source and Form Data Model.

>[!VIDEO](https://video.tv.adobe.com/v/37815?quality=12&learn=on)

To set up tomcat, please follow the following instructions:

1. Download and install JDK1.8.
2. Set JAVA_HOME to point to JDK1.8.
3. Download [tomcat](https://tomcat.apache.org/). This war file has been tested with Tomcat version 8.5.x and 9.0.x.
4. Download the tomcat version of your preference. You can download the 64-bit windows zip under the core section.
5. Unzip the contents to your c:\tomcat.
6. You should see something like this in your c drive **c:\tomcat\apache-tomcat-8.5.27** depending on the version of your tomcat
7. Create an environment variable called "CATALINA_HOME" and set its value to the tomcat install folder example c:\tomcat\apache- tomcat-8.5.27
8. Copy the SampleRest.war file into the webapps  folder of your Tomcat installation
9. Start new command prompt window.
10. Navigate to &lt;tomcat install folder&gt;\bin and run the startup.bat
11. Once your tomcat has started, test the endpoint exposed by WAR File by [clicking here](http://localhost:8080/SampleRest/webapi/getStatement/9586)
12. You should get sample data as the result of this call.

Congratulations !!!. You have setup tomcat and deployed the SampleRest.war file.

The following video explains the deployment of sample application in Tomcat
>[!VIDEO](https://video.tv.adobe.com/v/37815?quality=12&learn=on)

## Next Steps

[Create RESTful data source](./create-data-source.md)