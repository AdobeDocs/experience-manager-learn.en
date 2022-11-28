---
title: Prefill Service in Adaptive Forms
description: Pre-populate adaptive forms by fetching data from backend data sources.
feature: Adaptive Forms
version: 6.4,6.5
topic: Development
role: Developer
level: Intermediate
exl-id: f2c324a3-cbfa-4942-b3bd-dc47d8a3f7b5
last-substantial-update: 2021-11-27
---
# UsingPrefill Service in Adaptive Forms

You can prefill the fields of an Adaptive form using existing data. When a user opens a form, the values for those fields are prefilled. There are multiple ways to prefill adaptive forms fields. In this article, we will look at prefilling adaptive form using AEM Forms prefill service.

To learn more about various methods to pre-populate adaptive forms, [please follow this documentation](https://helpx.adobe.com/experience-manager/6-4/forms/using/prepopulate-adaptive-form-fields.html#AEMFormsprefillservice)

To prefill an adaptive form using the prefill service, you must create a class that implements the `com.adobe.forms.common.service.DataXMLProvider` interface. The method `getDataXMLForDataRef` will have the logic to build and return data that the adaptive form will consume to prepopulate the fields. In this method, you can fetch the data from any source and return the input stream of data document. The following sample code fetches the user profile information of the logged-in user and constructs an XML document whose input stream is returned to be consumed by the adaptive forms.

In the code snippet below we have a class which implements DataXMLProvider interface. We get access to the logged in user, and then fetch the logged in user's profile information. We then create XML document with a root node element called "data" and append appropriate elements to this data node. Once the XML document is constructed, the input stream of the XML document is returned.

This class is then made into OSGi bundle and deployed into AEM. Once the bundle is deployed, this prefill service is then available to be used as prefill service of your Adaptive Form.

```java
package com.aem.prefill.core;
import com.adobe.forms.common.service.DataXMLOptions;
import com.adobe.forms.common.service.DataXMLProvider;
import com.adobe.forms.common.service.FormsException;
import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
import javax.jcr.Session;
import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.transform.Transformer;
import javax.xml.transform.TransformerFactory;
import javax.xml.transform.dom.DOMSource;
import javax.xml.transform.stream.StreamResult;
import org.apache.jackrabbit.api.JackrabbitSession;
import org.apache.jackrabbit.api.security.user.Authorizable;
import org.apache.jackrabbit.api.security.user.UserManager;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.osgi.service.component.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.w3c.dom.Document;
import org.w3c.dom.Element;

@Component
public class PrefillAdaptiveForm implements DataXMLProvider {
  private static final Logger log = LoggerFactory.getLogger(PrefillAdaptiveForm.class);

  @Override
  public String getServiceDescription() {

    return "Custom AEM Forms PreFill Service";
  }

  @Override
  public String getServiceName() {

    return "CustomAemFormsPrefillService";
  }

  @Override
  public InputStream getDataXMLForDataRef(DataXMLOptions dataXmlOptions) throws FormsException {
    InputStream xmlDataStream = null;
    Resource aemFormContainer = dataXmlOptions.getFormResource();
    ResourceResolver resolver = aemFormContainer.getResourceResolver();
    Session session = (Session) resolver.adaptTo(Session.class);
    try {
      UserManager um = ((JackrabbitSession) session).getUserManager();
      Authorizable loggedinUser = um.getAuthorizable(session.getUserID());
      log.debug("The path of the user is" + loggedinUser.getPath());
      DocumentBuilderFactory docFactory = DocumentBuilderFactory.newInstance();
      DocumentBuilder docBuilder = docFactory.newDocumentBuilder();
      Document doc = docBuilder.newDocument();
      Element rootElement = doc.createElement("data");
      doc.appendChild(rootElement);

      if (loggedinUser.hasProperty("profile/givenName")) {
        Element firstNameElement = doc.createElement("fname");
        firstNameElement.setTextContent(loggedinUser.getProperty("profile/givenName")[0].getString());
        rootElement.appendChild(firstNameElement);
        log.debug("Created firstName Element");
      }

      if (loggedinUser.hasProperty("profile/familyName")) {
        Element lastNameElement = doc.createElement("lname");
        lastNameElement.setTextContent(loggedinUser.getProperty("profile/familyName")[0].getString());
        rootElement.appendChild(lastNameElement);
        log.debug("Created lastName Element");

      }
      if (loggedinUser.hasProperty("profile/email")) {
        Element emailElement = doc.createElement("email");
        emailElement.setTextContent(loggedinUser.getProperty("profile/email")[0].getString());
        rootElement.appendChild(emailElement);
        log.debug("Created email Element");

      }

      TransformerFactory transformerFactory = TransformerFactory.newInstance();
      ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
      Transformer transformer = transformerFactory.newTransformer();
      DOMSource source = new DOMSource(doc);
      StreamResult outputTarget = new StreamResult(outputStream);
      TransformerFactory.newInstance().newTransformer().transform(source, outputTarget);
      if (log.isDebugEnabled()) {
        FileOutputStream output = new FileOutputStream("afdata.xml");
        StreamResult result = new StreamResult(output);
        transformer.transform(source, result);
      }

      xmlDataStream = new ByteArrayInputStream(outputStream.toByteArray());
      return xmlDataStream;
    } catch (Exception e) {
      log.error("The error message is " + e.getMessage());
    }
    return null;

  }

}

```

To test this capability on your server, please perform the following

* Make sure the logged in [user's profile](http://localhost:4502/security/users.html) information is filled out. The sample looks for FirstName,LastName and Email properties of the logged in user.
* [Download and extract the contents of the zip file on to your computer](assets/prefillservice.zip)
* Deploy the prefill.core-1.0.0-SNAPSHOT bundle using the [AEM web console](http://localhost:4502/system/console/bundles)
* Import the adaptive form using the Create | File Upload from the [FormsAndDocuments section](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments)
* Make sure the [form](http://localhost:4502/editor.html/content/forms/af/prefill.html) is using **"Custom AEM Forms PreFill Service"** as the prefill service. This can be verified from the configuration properties of the **Form Container** section.
* [Preview the form](http://localhost:4502/content/dam/formsanddocuments/prefill/jcr:content?wcmmode=disabled). You should see the form populated with the correct values.

>[!NOTE]
>
>If you have enabled debugging for the com.aem.prefill.core.PrefillAdaptiveForm, the generated xml data file in written to your AEM server install folder.

