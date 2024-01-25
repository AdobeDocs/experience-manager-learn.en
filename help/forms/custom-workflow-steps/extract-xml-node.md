---
title: Extract node from submitted data xml
description: Custom process step to add write document residing under the payload folder to the file system
feature: Adaptive Forms
version: 6.5
topic: Development
role: Developer
level: Beginner
kt: kt-9860
exl-id: 5282034f-275a-479d-aacb-fc5387da793d
last-substantial-update: 2020-07-07
duration: 44
---
# Extract node from submitted data xml

This custom process step is to create new xml document by extracting node from another xml document. You would need to use this when you want to merge the submitted data with xdp template to generate pdf. For example when you submit an adaptive form the data that you need to merge with the xdp template is inside the data element. In this case you would need to create another xml document by extracting the appropriate data element.

The following screen shot shows you the arguments that you need to pass to the custom process step
![process-step](assets/create-xml-process-step.png)
The following are the parameters
* Data.xml - The xml file from which you want to extract node
* datatomerge.xml - The new xml created with the extracted node
* /afData/afUnboundData/data - The node to extract


The following screen shot shows you the datamerge.xml being created under the payload folder
![create-xml](assets/create-xml.png)

[Custom bundle can be downloaded from here](/help/forms/assets/common-osgi-bundles/SetValueApp.core-1.0-SNAPSHOT.jar)
