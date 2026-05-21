---
title: Create the MyAccountForm
description: Create the myaccount form to retrieve the partially completed form on succesful verification of application id and telephone number.
feature: Adaptive Forms
type: Tutorial
version: Experience Manager 6.4, Experience Manager 6.5
jira: KT-6599
thumbnail: 6599.jpg
topic: Development
role: User
level: Beginner
exl-id: 1ecd8bc0-068f-4557-bce4-85347c295ce0
duration: 53
TQID: https://experienceleague.adobe.com/C4m1N6IbRX44ZN2qq4JgSztKmKotwC3Kkb9d7kWCG-g
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Create the MyAccountForm

The form **MyAccountForm** is used to retrieve the partially completed adaptive form after the user has verified the application id and the mobile number associated with the application id.

![my account form](assets/6599.JPG)

When the user enters the application id and clicks the **FetchApplication** button, the mobile number associated with the application id is fetched from the database using the Get operation of the form data model.

This form makes use of the POST invocation of the Form Data Model to verify the mobile number using OTP. The form's submit action is triggered on successful verification of the mobile number using the following code. We are triggering the click event of the submit button named **submitForm**.

>[!NOTE]
> You will need to provide the API Key and the API Secret values specific to your [Nexmo](https://dashboard.nexmo.com/) account in the appropriate fields of the MyAccountForm

![trigger-submit](assets/trigger-submit.JPG)



This form is associated with custom submit action that forwards the form submission to the servlet mounted on **/bin/renderaf**

``` java
com.adobe.aemds.guide.utils.GuideSubmitUtils.setForwardPath(slingRequest,"/bin/renderaf",null,null);

```

The code in the servlet mounted on **/bin/renderaf** forwards the request to render the storeafwithattachments adaptive form prepopulated with the saved data.


* The MyAccountForm can be [downloaded from here](assets/my-account-form.zip)

* Sample forms are based on [custom adaptive form template](assets/custom-template-with-page-component.zip) that needs to be imported into AEM for the sample forms to render correctly.

* [Custom submit handler](assets/custom-submit-my-account-form.zip) associated with the MyAccountForm submission needs to be imported into AEM.

## Next Steps

[Test the solution by deploying the sample assets](./deploy-this-sample.md)
