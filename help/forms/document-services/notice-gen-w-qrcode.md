---
title: Dynamic QR Code within PDF Notice Generation
description: Providing unique QR codes with personalized notice generation.
feature: Barcoded Forms
version: Experience Manager 6.5
topic: Development
role: Developer
level: Intermediate
exl-id: 
last-substantial-update: 
duration: 115
TQID: https://experienceleague.adobe.com/zz2pYLxLcsWiGsL2pOZ-etEl-9CM6gdOTwuD8sDxpp0
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
---
# Dynamic QR Code within PDF Notice Generation{#notice-gen-w-qrcode}

This article will demonstrate the ability to provide a dynamic QR code within a personalized PDF notice. The use case is as follows:

1. The author creates an XDP file with designated location of QR code among additional personalized data fields
2. XDP file is uploaded to AEM and is used as a template for Interactive Communication
3. Case Worker or batch processing provides dynamic data to merge with XDP template
4. Generated PDF is created with personalized data including unique QR code URL value provided
5. Notice recipient receives personalized notice on paper which includes unique QR code where recipient may be directed to provide additional information for specific need


First step is to create the XDP template using Forms Designer. Below see the highlighted objects: the placed QRCode object as well as a hidden text field which will be used as the source value to trigger the QR code generation. Also note the Javascript code that indicates the population of the QRCode object to be that of the hidden field. 




The following code is part of the client library that is referenced by Adaptive Form. When a user adds the attachment to the adaptive form, this code is triggered. The code makes a GET call to the servlet with the path of the attachment passed in the request parameter. The data received from the servlet call is then used to populate the adaptive form.

```javascript
$(document).ready(function()
   {
       guideBridge.on("elementValueChanged",function(event,data){
             if(data.target.name=="fileAttachment")
         {
             window.guideBridge.getFileAttachmentsInfo({
        success:function(list) 
                 {
                     console.log(list[0].name + " "+ list[0].path);
                      const getFormNames = '/bin/decodebarcode?pdfPath='+list[0].path;
      $.getJSON(getFormNames, function (data) {
                            console.log(data);
                            var nameField = window.guideBridge.resolveNode("guide[0].guide1[0].guideRootPanel[0].Name[0]");
                            nameField.value = data.name;
                            var addressField = window.guideBridge.resolveNode("guide[0].guide1[0].guideRootPanel[0].Address[0]");
                            addressField.value = data.address;
                            var cityField = window.guideBridge.resolveNode("guide[0].guide1[0].guideRootPanel[0].City[0]");
                            cityField.value = data.city;
                            var stateField = window.guideBridge.resolveNode("guide[0].guide1[0].guideRootPanel[0].State[0]");
                            stateField.value = data.state;
                             var zipField = window.guideBridge.resolveNode("guide[0].guide1[0].guideRootPanel[0].Zip[0]");
                            zipField.value = data.zipCode;
                            var countryField = window.guideBridge.resolveNode("guide[0].guide1[0].guideRootPanel[0].Country[0]");
                            countryField.value = data.country;
                        });
                        }
                  });
             }
         });
        });

```

>[!NOTE]
>
>The Adaptive Form included with this package was built using AEM Forms 6.4. If you intend to use this package in AEM Forms 6.3 environment, please create the Adaptive Form in AEM Form 6.3

Line 12 - Custom code to get service resolver. This bundle is included as part of this articles assets.

Line 23 - Call the DocumentServices extractBarCode method to get the JSON object populated with decoded data

To get this running on your system, please follow the following steps:

1. [Download BarcodeService.zip](assets/barcodeservice.zip) and import into AEM using the package manager
1. [Download and install the Custom DocumentServices Bundle](/help/forms/assets/common-osgi-bundles/AEMFormsDocumentServices.core-1.0-SNAPSHOT.jar)
1. [Download and install the DevelopingWithServiceUser Bundle](/help/forms/assets/common-osgi-bundles/DevelopingWithServiceUser.jar)
 1. [Download the sample PDF Form](assets/barcode.pdf)
1. Point your browser to the [sample adaptive form](http://localhost:4502/content/dam/formsanddocuments/barcodedemo/jcr:content?wcmmode=disabled)
1. Upload the sample PDF provided
1. You should see the forms populated with the data
