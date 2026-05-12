---
title: Populate Adaptive Form Table
description: Populate Adaptive Form table with the results from Form Data Model Service Invocations
feature: Adaptive Forms
version: Experience Manager 6.4, Experience Manager 6.5
topic: Development
role: User
level: Intermediate
exl-id: 6e4b901a-6534-4c34-b315-2f2620b74247
last-substantial-update: 2019-06-09T00:00:00.000Z
duration: 45
TQID: https://experienceleague.adobe.com/3i6Nor82jaUOA6761rjPXO07GPNummdnIAAvfSa7OM0
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
---
# Populate Adaptive Form Table with the results of Form Data Model Service Invocation

[Live form is hosted here](https://forms.enablementadobe.com/content/dam/formsanddocuments/amortization/jcr:content?wcmmode=disabled)
In this article we take a look at populating adaptive forms table by fetching data from form data model service invocation. We are going to create an amortization schedule in a table that lists each regular payment on a mortgage over time. The amortization results are returned by our Form Data Model. The Form Data Model's service is invoked on the click event of calculate button as shown in the screenshot. The input and the output parameters of the service invocation are mapped appropriately as shown in the screen shot. The output is mapped to the columns of Row1
![clickevent](assets/amortization.PNG) 

Row1 is configured to be grow depending on the data returned by the service call. Notice the repeat settings that are specified here. A value of -1 indicates unlimited number of rows in the table
![Row1](assets/rowconfiguration.PNG)

## Deploy this on your server

[Install Tomcat as specified here](/help/forms/ic-print-channel-tutorial/set-up-tomcat.md)
[Deploy the SampleRest.war file contained in this zip file in your Tomcat](assets/sample-rest.zip)
[Install the assets ](assets/amortizationschedule.zip) using AEM package manager
[Open the Amortization Schedule Form](http://localhost:4502/content/dam/formsanddocuments/amortization/jcr:content?wcmmode=disabled)
Enter the appropriate value and click on calculate
Amortization Schedule should get populated in your form
