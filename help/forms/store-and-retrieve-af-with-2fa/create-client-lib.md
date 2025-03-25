---
title: Create client libraries
description: Create client library to handle the click event of the "Save and Exit" button
feature: Adaptive Forms
type: Tutorial
version: Experience Manager 6.4, Experience Manager 6.5
jira: KT-6597
thumbnail: 6597.pg
topic: Development
role: Developer
level: Intermediate
exl-id: c90eea73-bd44-40af-aa98-d766aa572415
duration: 42
---
# Create client lib

Create [client lib](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html) which will include the code to invoke the method `doAjaxSubmitWithFileAttachment` of the `guideBridge` API on the click event of the button identified by the CSS class **save button**.  We pass the adaptive form data, `fileMap`, and the `mobileNumber` to the endpoint listening at `**/bin/storeafdatawithattachments`

After the form data is saved a unique application id is generated and presented to the user in a dialog box. On dismissing the dialog box the user is taken to the form which allows them to retrieve the saved adaptive form using the unique application id. 

```java

$(document).ready(function () {
  
  $(".savebutton").click(function () {
    var tel = guideBridge.resolveNode(
      "guide[0].guide1[0].guideRootPanel[0].contactInformation[0].basicContact[0].telephoneNumber[0]"
    );
    var telephoneNumber = tel.value;
    guideBridge.getFormDataString({
      success: function (data) {
        var map = guideBridge._getFileAttachmentMapForSubmit();
        guideBridge.doAjaxSubmitWithFileAttachment(
          "/bin/storeafdatawithattachments",
          {
            data: data.data,
            fileMap: map,
            mobileNumber: telephoneNumber,
          },
          {
            success: function (x) {
              bootbox.alert(
                "This is your reference number.<br>" +
                  x.data.applicationID +
                  " <br>You will need this to retrieve your application",
                function () {
                  console.log(
                    "This was logged in the callback! After the ok button was pressed"
                  );
                  window.location.href =
                    "http://localhost:4502/content/dam/formsanddocuments/myaccountform/jcr:content?wcmmode=disabled";
                }
              );
              console.log(x.data.path);
            },
          },
          guideBridge._getFileAttachmentsList()
        );
      },
    });
  });
});
```

>[!NOTE]
> We have used [bootbox JavaScript library](https://bootboxjs.com/examples.html) to display dialog box

The client libraries used in this sample can be [downloaded from here.](assets/store-af-with-attachments-client-lib.zip)

## Next Steps

[Verify users with OTP service](./verify-users-with-otp.md)
