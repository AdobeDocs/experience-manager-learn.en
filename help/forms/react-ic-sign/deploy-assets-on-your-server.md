---
title: Deploy the sample assets on your server
description: Get the use case working on your local server
feature: Adaptive Forms,Acrobat Sign
version: 6.4,6.5
topic: Development
role: Developer
level: Beginner
jira: KT-13099
last-substantial-update: 2023-04-13
exl-id: f12f83fa-673a-454c-aa52-6ea769a182b7
duration: 36
---
# Deploy the assets

The following assets/configurations were deployed on a AEM Forms publish server.

* [Adobe Sign Wrapper Bundle](assets/AcrobatSign.core-1.0.0-SNAPSHOT.jar)

* [Sample Interactive Communication Template](assets/waiver-interactive-communication.zip)
* [Deploy the DevelopingWithServiceUser bundle](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/developingwithserviceuser.zip)
* Add the following entry in the Apache Sling Service User Mapper Service using the OSGi configMgr 
**DevelopingWithServiceUser.core:getformsresourceresolver=fd-service**

## Deploy the sample react app

* [Download the sample react app](assets/mult-step-form1.zip)
* Unzip the contents of the react app in a new folder
* Navigate to the folder and run the following commands

``` java
npm install
npm start
```

Open the EmergencyContact.js file and change the URL in the fetch method to match your environment.


```javascript
 const getWebForm=async()=>
     {
        setSpinner(true)
        console.log("inside widgetURL function emergency contact");
        // NOTE: replace the `aemforms.azure.com:4503` with your AEM FORM server
        let res = await fetch("http://aemforms.azure.com:4503/bin/getwidgeturl",
          {
            method: "POST",
            body: JSON.stringify({"icTemplate":"/content/forms/af/waiver/waiver/channels/print","waiver":formData})
                     
         })
 
```

To enable making POST calls to the AEM endpoint from your REACT app, you will need to specify the appropriate entires in the Allowed Origins field in Adobe Granite Cross-Origin Resource Sharing Policy configuration.

![cors-setting](assets/cors-settings.png)

See [understanding CORS with AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html) for more details on CORS configuration options.
