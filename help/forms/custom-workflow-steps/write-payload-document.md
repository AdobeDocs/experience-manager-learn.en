---
title: Write the payload document to file system
description: Custom process step to add write document residing under the payload folder to the file system
feature: Adaptive Forms
version: Experience Manager 6.5
topic: Development
role: Developer
level: Beginner
kt: kt-9859
exl-id: bab7c403-ba42-4a91-8c86-90b43ca6026c
last-substantial-update: 2020-07-07T00:00:00.000Z
duration: 27
TQID: https://experienceleague.adobe.com/UF6Fo-AZzkwS-7u4zXn5AikOZ6gy3jLTBBH-xBXfUF0
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Write the document to the file system

Common use case is to write the generated documents in the workflow to the file system.
This custom workflow process step makes it easy to write the workflow documents to file system.
The custom process takes the following comma separated arguments

``` java
ChangeBeneficiary.pdf,c:\confirmation
```

The first argument is the name of the document that you want to save to the file system. The second argument is the folder location you want to save the document. For example in the above use case the document is written to `c:\confirmation\ChangeBeneficiary.pdf`

The following screen shot shows you the arguments that you need to pass to the custom process step
![write-payload-file-system](assets/write-payload-file-system.png)

[Custom bundle can be downloaded from here](/help/forms/assets/common-osgi-bundles/SetValueApp.core-1.0-SNAPSHOT.jar)
