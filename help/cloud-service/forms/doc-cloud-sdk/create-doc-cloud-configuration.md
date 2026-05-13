---
title: Create custom OSGi Configuration
description: Custom OSGi configuration to capture document cloud specific details
solution: Experience Manager, Experience Manager Forms
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
topic: Development
thumbnail: 7818.jpg
jira: KT-7818
exl-id: 1f34c356-6c0c-46ff-9cea-7baacfc4bb7f
duration: 22
TQID: https://experienceleague.adobe.com/1rojRvNK4jgwSnuEM53HPJxl9kylZ3bzxL7CowJkLqA
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
# Introduction

Create custom OSGi configuration to capture the credentials of your document cloud account


To make a custom OSGi configuration, we need to first create an interface whose public methods will represent the fields in the configuration.

![doc-cloud-config](assets/doc-cloud-configuration.JPG)


Create an interface named DocumentCloudConfiguration and paste the following code in it.

```java
package com.aemforms.doccloud.core;

import org.osgi.service.metatype.annotations.AttributeDefinition;
import org.osgi.service.metatype.annotations.ObjectClassDefinition;

@ObjectClassDefinition(name="Document Cloud Service Configuration", description = "Connect AEM Forms With Document Cloud")
public @interface DocumentCloudConfiguration {
      @AttributeDefinition(name="Client ID", description="Client ID")
      String getClientID() default "";
      
      @AttributeDefinition(name="Client Secret", description="Client Secret")
      public String getClientSecret() default "26dc4de1-f7f0-46b6-9e8e-86270ad34f58";
      
      @AttributeDefinition(name="Technical Account ID", description="Technical Account ID")
      public String getTechnicalAccount() default "42FF05A7606F71BB0A495FBE@techacct.adobe.com";

      @AttributeDefinition(name="Organization ID", description="Organization ID")
      String getOrganizationID() default "299805FF5FC9199D0A495EBC@AdobeOrg";
      
      @AttributeDefinition(name="Metascope", description="Metascope")
      String getMetascope() default "ent_documentcloud_sdk";


}

```
