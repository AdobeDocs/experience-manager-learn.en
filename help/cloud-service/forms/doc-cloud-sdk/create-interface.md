---
title: Create service interface
description: Define the methods in the interface that you want to expose
solution: Experience Manager
type: Documentation
role: Developer
level: Beginner, Intermediate
version: cloud-service
topic: Development
thumbnail: 7825.jpg
kt: 7825

---
# Interface

Create a interface with the following 2 method definitions.

```java
package com.aemforms.doccloud.core;

import java.io.InputStream;

import com.adobe.aemfd.docmanager.Document;

public interface DocumentCloudSDKService {
	
	public Document getPDF(String location,String accessToken,String fileName);
	public Document createPDFFromInputStream(InputStream is,String fileName);

}


}

```
