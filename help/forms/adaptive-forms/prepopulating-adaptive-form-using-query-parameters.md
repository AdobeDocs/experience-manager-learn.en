---
title: Populate Adaptive Forms using query parameters.
description: Populate Adaptive Forms with data from query parameters.
feature: Adaptive Forms
version: 6.5
topic: Development
role: Developer
level: Experienced
jira: KT-11470
last-substantial-update: 2020-11-12
exl-id: 14ac6ff9-36b4-415e-a878-1b01ff9d3888
duration: 49
---
# PrePopulate Adaptive Forms using query parameters

One of our customers had the requirement to populate adaptive form using the query parameters. For example in the following url the FirstName and LastName fields in the adaptive form are set to John and Doe respectively

``` html

https://forms.enablementadobe.com/content/forms/af/testingxml.html?FirstName=John&LastName=Doe


```

To accomplish this use case a new adaptive form template was created and associated with a page component. In this page component we have a jsp to get hold of the query parameters and create an xml structure that can be used to populate the adaptive form.

The details on creating a new Adaptive Form template and page component are [explained in this video.](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/storing-and-retrieving-form-data/part5.html?lang=en)

The following is the code that was used in the jsp page

``` java
java.util.Enumeration enumeration = request.getParameterNames();
String dataXml = "<afData><afUnboundData><data>";
while (enumeration.hasMoreElements())
{
   String parameterName = (String) enumeration.nextElement();
   dataXml = dataXml + "<" + parameterName + ">" + request.getParameter(parameterName) + "</" + parameterName + ">";

}

dataXml = dataXml + "</data></afUnboundData></afData>";
//System.out.println("The data xml is "+dataXml);
slingRequest.setAttribute("data", dataXml);
```

>[!NOTE]
>
>If your form is using schema the structure of your xml will be different and you will have to build the xml accordingly. 


## Deploy the assets on your system

* [Download and install the Adaptive Form Template using the Package Manager](assets/populate-with-xml.zip)
* [Download and install the sample adaptive form](assets/populate-af-with-query-paramters-form.zip)

* [Preview the adaptive form](http://localhost:4502/content/dam/formsanddocuments/testingxml/jcr:content?wcmmode=disabled&FirstName=John&LastName=Doe)
You should see the adaptive form populated with the value John and Doe
