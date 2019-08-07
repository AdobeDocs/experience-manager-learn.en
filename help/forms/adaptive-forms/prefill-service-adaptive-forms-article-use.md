---
title: Prefill Service in Adaptive Forms
seo-title: Prefill Service in Adaptive Forms
description: Pre-populate adaptive forms by fetching data from backend data sources.
seo-description: Pre-populate adaptive forms by fetching data from backend data sources.
sub-product: forms
feature: adaptive-forms
topics: integrations
audience: developer
doc-type: article
activity: implement
version: 6.4,6.5
uuid: 26a8cba3-7921-4cbb-a182-216064e98054
discoiquuid: 936ea5e9-f5f0-496a-9188-1a8ffd235ee5
---

# UsingPrefill Service in Adaptive Forms

You can prefill the fields of an Adaptive form using existing data. When a user opens a form, the values for those fields are prefilled. There are multiple ways to prefill adaptive forms fields. In this article, we will look at prefilling adaptive form using AEM Forms prefill service.

To learn more about various methods to pre-populate adaptive forms, [please follow this documentation](https://helpx.adobe.com/experience-manager/6-4/forms/using/prepopulate-adaptive-form-fields.html#AEMFormsprefillservice)

To prefill adaptive form using the prefill service, you will have to create a class which implements the DataProvider interface. The method getPrefillData will have the logic to build and return data that adaptive form will consume to prepopulate the fields. In this method, you can fetch the data from any source and return input stream of data document. The following sample code fetches the user profile information of the logged in user and constructs an XML document whose input stream is returned to be consumed by the adaptive forms.

In the code snippet below we have a class which implements DataProvider interface. We get access to the logged in user, and then fetch the logged in user's profile information. We then create XML document with a root node element called "data" and append appropriate elements to this data node. Once the XML document is constructed, the input stream of the XML document is returned.

This class is then made into OSGi bundle and deployed into AEM. Once the bundle is deployed, this prefill service is then available to be used as prefill service of your Adaptive Form.

```java
public class PrefillAdaptiveForm implements DataProvider {
 private Logger logger = LoggerFactory.getLogger(PrefillAdaptiveForm.class);

 public String getServiceName() {
  return "Default Prefill Service";
 }
 
 public String getServiceDescription() {
  return "This is default prefill service to prefill adaptive form with user data";
 }
 
 public PrefillData getPrefillData(final DataOptions dataOptions) throws FormsException {
  PrefillData prefillData = new PrefillData() {
   public InputStream getInputStream() {
    return getData(dataOptions);
   }
   
   public ContentType getContentType() {
    return ContentType.XML;
   }
  };
  return prefillData;
 }

 private InputStream getData(DataOptions dataOptions) throws FormsException {  
  try {
   Resource aemFormContainer = dataOptions.getFormResource();
   ResourceResolver resolver = aemFormContainer.getResourceResolver();
   Session session = resolver.adaptTo(Session.class);
   UserManager um = ((JackrabbitSession) session).getUserManager();
   Authorizable loggedinUser = um.getAuthorizable(session.getUserID());
   DocumentBuilderFactory docFactory = DocumentBuilderFactory.newInstance();
   DocumentBuilder docBuilder = docFactory.newDocumentBuilder();
   Document doc = docBuilder.newDocument();
   Element rootElement = doc.createElement("data");
   doc.appendChild(rootElement);
   Element firstNameElement = doc.createElement("fname");
   firstNameElement.setTextContent(loggedinUser.getProperty("profile/givenName")[0].getString());
     .
     .
     .
   InputStream inputStream = new ByteArrayInputStream(rootElement.getTextContent().getBytes());
   return inputStream;
  } catch (Exception e) {
   logger.error("Error while creating prefill data", e);
   throw new FormsException(e);
  }
 }
}
```

To test this capability on your server, please perform the following

* [Download and extract the contents of the zip file on to your computer](assets/prefillservice.zip)
* Make sure the logged in [user's profile](http://localhost:4502/libs/granite/security/content/useradmin) information is filled out completely. This is a required for the sample to work. The sample does not have any error checking for missing user profile properties.
* Deploy the bundle using the [AEM web console](http://localhost:4502/system/console/bundles)
* Create Adaptive Form using the XSD
* Associate "Custom Aem Form Pre Fill Service" as the prefill service for your adaptive form
* Drag and drop schema elements on to the form
* Preview the form

>[!NOTE]
>
>If the adaptive form is based on XSD, make sure the XML document returned by the prefill service matches to the XSD your adaptive form is based on.
>
>If the adaptive form is not based on XSD, then you will have to manually bind the fields. For example to bind an adaptive form field to  fname  element in the XML data you will use `/data/fname`  in the Bind reference of the adaptive form field.

