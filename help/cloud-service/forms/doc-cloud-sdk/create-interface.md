---
title: Create service interface
description: Define the methods in the interface that you want to expose
solution: Experience Manager
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
topic: Development
thumbnail: 7825.jpg
jira: KT-7825
exl-id: f262013b-aaf1-43d1-84b8-6173942c3415
duration: 7
TQID: 'https://experienceleague.adobe.com/8oqNxQ5HgeSF8Wqy3NEu1srAyebmShMGR4o9qy-lCAU'
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
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
```
