---
title: Simplified Steps for Installing AEM Forms on Windows
description: Quick and easy steps to install AEM Forms on windows
feature: Adaptive Forms
type: Tutorial
version: 6.5
topic: Development
role: Admin
level: Beginner
exl-id: 80288765-0b51-44a9-95d3-3bdb2da38615
last-substantial-update: 2020-06-09
duration: 113
---
# Simplified Steps for Installing AEM Forms on Windows

>[!NOTE]
>
>Never double click the AEM Quick Start jar, if you intend to use AEM Forms.
>
>Also, make sure there are no spaces in the AEM Forms Installation folder path.
>
>For Example do not install AEM Forms in c:\jack and jill\AEM Forms folder

>[!NOTE]
>
>If you are installing AEM Forms 6.5, Please make sure you have installed the following 32 bit Microsoft Visual C++ redistributables.
>
>* Microsoft Visual C++ 2008 redistributable
>* Microsoft Visual C++ 2010 redistributable
>* Microsoft Visual C++ 2012 redistributable
>* Microsoft Visual C++ 2013 redistributable (as of 6.5)

Although we recommend following the [official documentation](https://helpx.adobe.com/experience-manager/6-3/forms/using/installing-configuring-aem-forms-osgi.html) for installing AEM Forms. The following steps can be followed to install and configure AEM Forms on Windows environment:

* Make sure you have the appropriate JDK installed
   * AEM 6.2 you need: Oracle SE 8 JDK 1.8.x (64bit)
   * AEM 6.3 and AEM 6.4 you need: Oracle SE 8 JDK 1.8.x (64bit)
   * AEM 6.5 you need JDK 8 or JDK 11
   * [Official JDK Requirements](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/introduction/technical-requirements.html?lang=en) are listed here
* Make sure the JAVA_HOME is set to point to the JDK you have installed.
   * To create the JAVA_HOME variable in windows follow the steps below:
      * Right-click My Computer and select Properties
      * On the Advanced tab, select Environment Variables and create a new system variable called JAVA_HOME.
      * Set the variable value to point to JDK installed on your system. For example c:\program files\java\jdk1.8.0_25

* Create a folder called AEMForms on your C drive
* Locate the AEMQuickStart.Jar and move it into AEMForms folder
* Copy the license.properties file into this AEMForms folder
* Create a batch file called "StartAemForms.bat" with the following content:
   * `java -d64 -Xmx2048M -jar AEM_6.5_Quickstart.jar -gui`
      * Here AEM_6.5_Quickstart.jar is the name of my AEM quickstart jar.
   * You can rename your jar to any name, but please make sure that name is reflected in the batch file. Save the batch file in the AEMForms Folder.

* Open a new command prompt, and navigate to _c:\aemforms_.

* Execute the StartAemForms.bat file from the command prompt.

* You should get a small dialog box indicating the progress of the startup.

* Once the startup is complete, open the sling.properties file. This is located in c:\AEMForms\crx-quickstart\conf folder.

* Copy the following 2 lines towards the bottom of the file
   * **sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.&#42;** **sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.&#42;**
* These two properties are required for document services to work
* Save the sling.properties file
* [Download the appropriate forms addon package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en)
* Install the forms add on package using [package manager](http://localhost:4502/crx/packmgr/index.jsp).
* After you have installed add on package the following steps need to be followed

   * **Make sure all the bundles are in active state. (Except for AEMFD Signatures bundle).**
   * **It would typically take 5 or more minutes for all the bundles to get to active state.**

   * **Once all the bundles are active (Except the AEMFD Signatures bundle), restart your system to complete the AEM Forms installation**

## sun.util.calendar package to the allowed list

1. Open Felix web console in your [browser window](http://localhost:4502/system/console/configMgr)
1. Search and open Deserialization Firewall Configuration: `com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`
1. Add `sun.util.calendar` as a new entry under `com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.firewall.deserialization.whitelist.name`
1. Save the changes.

Congratulations!!! You have now installed and configured AEM Forms on your system.
Depending on your needs you can configure  [Reader Extensions](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/configuring-reader-extension-osgi.html) or [ PDFG](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/osgi-installation/install-configure-document-services.html) on your server
