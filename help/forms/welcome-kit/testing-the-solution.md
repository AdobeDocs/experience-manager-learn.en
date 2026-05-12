---
title: Testing the welcome kit solution
description: Deploying the solution assets to test the solution
feature: Adaptive Forms
version: Experience Manager 6.5
topic: Development
role: Developer
level: Beginner
last-substantial-update: 2022-12-14T00:00:00.000Z
exl-id: 07a1a9fc-7224-4e2d-8b6d-d935b1125653
duration: 29
TQID: https://experienceleague.adobe.com/tM2KthMtyuggyk4jfchpJgtIJTQOzfJvdv-7Tdt8AQA
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
# Deploy and test the sample assets

[Install the welcome kit package](assets/welcomekit.zip). This package contains the page template,custom component to list the assets,sample workflow,email template and sample pdf documents to include in the welcome kit.
[Install the welcome-kit bundle](assets/welcomekit.core-1.0.0-SNAPSHOT.jar). This bundle contains the code to create the page and the java class to return the assets to be displayed in the web page.
[Install the sample adaptive form](assets/account-openeing-form.zip)
Configure the Day CQ Mail Service. The worklow sends the welcome kit link to the form submitter which needs SMTP configured correctly.
Configure the Send Email component of the workflow as per your requirements
[Preview the form](http://localhost:4502/content/dam/formsanddocuments/co-operators/accountopeningform/jcr:content?wcmmode=disabled)
Enter your details and select one or more mutual funds and submit the form
You should get a email with a link to the welcome kit
