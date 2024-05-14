---
title: Create custom submit to handle core component based form submission
description: Create custom submit to store the form data with attachments in Azure
feature: Adaptive Forms
type: Documentation
role: Developer
level: Beginner
version: 6.5
topic: Integrations
jira: KT-14794
exl-id: c4257567-76bd-417e-a1a2-38a0647767d9
duration: 147
---
# Create custom submit to handle the form submission

To satisfy the use case, a custom submit service was created to store the submitted data and attachments in Azure. When core component based form is submitted, the data is in the following format

```json
{
    "Name": "Gloria Rios",
    "EmailID": "grios@email.com",
    "ExistingCustomer": [
        "Yes"
    ],
    "PhoneNumber": "1234567890",
    "Solution": "Forms",
    "contractcopy": {
        "name": "annualcontract.pdf",
        "size": 80194,
        "mediaType": "application/pdf",
        "data": "[object File]"
    },
    "Message": "We would like to renew our annual contract "
}
```

The element _**contractcopy**_ represents a file attachment component and is used to capture attachments submitted with the form.
To be able to prefill adaptive form with the data and its attachments, the attachments submitted will be saved in Azure portal and the data element of the contractcopy object in the submitted data will be updated with the url of the saved attachment.
The custom submit service extracts and stores the attachments in Azure portal.  The updated submitted data will look like this


```json
{
    "Name": "Gloria Rios",
    "EmailID": "grios@email.com",
    "ExistingCustomer": [
        "Yes"
    ],
    "PhoneNumber": "1234567890",
    "Solution": "Forms",
    "contractcopy": {
        "name": "annualcontract.pdf",
        "size": 80194,
        "mediaType": "application/pdf",
        "data": "https://aemformstutorial.blob.core.windows.net/benefiitsenrollment/69d5a2?sv=2022-11-02&ss=bfqt&srt=KiHs0%3D"
    },
    "Message": "We would like to renew our annual contract "
}
``


```


[The sample custom submit handler for core components based adaptive form is available here](https://github.com/adobe/aem-core-forms-components/blob/master/it/core/src/main/java/com/adobe/cq/forms/core/components/it/service/CustomAFSubmitService.java#L56). The following custom submit was written to handle the form submission

```java
package com.azuredemo.core;
import com.adobe.aemds.guide.common.GuideValidationResult;
import com.adobe.aemds.guide.model.FormSubmitInfo;
import com.adobe.aemds.guide.service.FormSubmitActionService;
import com.adobe.aemds.guide.utils.GuideConstants;
import com.adobe.forms.common.service.FileAttachmentWrapper;
import com.azuredemo.core.SaveAndFetchFromAzure.StoreAndFetchDataFromAzureStorage;
import com.google.gson.Gson;
import com.google.gson.JsonObject;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import java.util.HashMap;
import java.util.Map;
import java.util.UUID;

@Component(
    service = FormSubmitActionService.class,
    immediate = true
)
public class StoreFormDataWithAttachments implements FormSubmitActionService {
    private static final String serviceName = "Store Submitted Form Data in Azure";
    private static transient Logger logger = LoggerFactory.getLogger(StoreFormDataWithAttachments.class);

    @Reference
    DataManager dataManager;
    @Reference
    StoreAndFetchDataFromAzureStorage storeAndFetchDataFromAzureStorage;

    @Override
    public String getServiceName() {
        return serviceName;
    }

    @Override
    public Map < String, Object > submit(FormSubmitInfo formSubmitInfo) {
        logger.debug("@@@@in my custom submit!!!");
        Map < String, Object > result = new HashMap < > ();
        result.put(GuideConstants.FORM_SUBMISSION_COMPLETE, Boolean.FALSE);
        try {

            String guideContainerPath = formSubmitInfo.getFormContainerPath();

            String submittedFormName = formSubmitInfo.getFormContainerResource().getParent().getParent().getName();
            logger.debug("The submitted form name is " + submittedFormName);
            String data = formSubmitInfo.getData();
            logger.debug("The submitted data is " + data);
            JsonObject jsonData = new Gson().fromJson(data, JsonObject.class);
            if (formSubmitInfo.getFileAttachments() != null && formSubmitInfo.getFileAttachments().size() > 0) {
                logger.debug("#####The form submitted has file attachments");
                for (int i = 0; i < formSubmitInfo.getFileAttachments().size(); i++) {
                    FileAttachmentWrapper fileAttachment = formSubmitInfo.getFileAttachments().get(i);

                    logger.debug("The url of the file attachment is " + fileAttachment.getUri());
                    logger.debug("The data ref of the file attachment is " + fileAttachment.getDataRef());
                    String fileName = fileAttachment.getFileName();
                    logger.debug("The fileName is  " + fileName);
                    logger.debug("#### Writing  " + fileName + " to azure");


                    String dataUrl = storeAndFetchDataFromAzureStorage.saveFormAttachmentinAzure(fileAttachment.getInputStream(), fileName, fileAttachment.getContentType());
                    jsonData.getAsJsonObject(fileAttachment.getDataRef()).addProperty("data", dataUrl);
                    logger.debug(jsonData.toString());

                }
            }


            String uniqueID = UUID.randomUUID().toString();

            logger.debug(storeAndFetchDataFromAzureStorage.saveFormDatainAzure(jsonData.toString(), "text/plain"));

            if (dataManager != null) {
                dataManager.put(uniqueID, data);

            }
            logger.info("AF Submission successful using custom submit service for: {}", guideContainerPath);
            result.put(GuideConstants.FORM_SUBMISSION_COMPLETE, Boolean.TRUE);
            result.put(DataManager.UNIQUE_ID, uniqueID);
            // adding id here so that this available in redirect parameters in final thank you page
            Map < String, Object > redirectParamMap = new HashMap < String, Object > () {
                {
                    put(DataManager.UNIQUE_ID, uniqueID);
                }
            };
            
            result.put("fd:redirectParameters", redirectParamMap);
        } catch (Exception ex) {
            logger.error("Error while using the AF Submit service", ex);
            GuideValidationResult guideValidationResult = new GuideValidationResult();
            guideValidationResult.setOriginCode("500");
            guideValidationResult.setErrorMessage("Internal server error");
            result.put(GuideConstants.FORM_SUBMISSION_ERROR, guideValidationResult);
        }
        return result;
    }

}

```

## Save Form Attachments in Azure

``` java
@Override
// Save the submitted form attachment in azure and return its url
public String saveFormAttachmentinAzure(InputStream attachmentStream, String fileName, String contentType) {
    logger.debug("Saving " + fileName + "  form attachment in azure  ");
    String sasToken = azurePortalConfigurationService.getSASToken();
    String storageURI = azurePortalConfigurationService.getStorageURI();
    logger.debug("The SAS Token is " + sasToken);
    logger.debug("The Storage URL is " + storageURI);

    int timeout = 5;
    RequestConfig config = RequestConfig.custom()
        .setConnectTimeout(timeout * 1000)
        .setConnectionRequestTimeout(timeout)
        .setSocketTimeout(timeout * 1000).build();
    org.apache.http.impl.client.CloseableHttpClient httpClient = HttpClientBuilder.create().setDefaultRequestConfig(config).build();
    UUID uuid = UUID.randomUUID();
    String putRequestURL = storageURI + uuid.toString();
    putRequestURL = putRequestURL + sasToken;
    System.out.println("The put Request " + putRequestURL);
    HttpPut httpPut = new HttpPut(putRequestURL);
    httpPut.addHeader("x-ms-blob-type", "BlockBlob");

    try {

        InputStreamEntity ies = new InputStreamEntity(attachmentStream, attachmentStream.available());

        httpPut.setEntity(ies);

        CloseableHttpResponse response = httpClient.execute(httpPut);
        logger.debug("Response code    " + response.getStatusLine().getStatusCode());
        logger.debug("Added file attachment  " + response.getStatusLine().getStatusCode() + "  uuid " + uuid.toString() + "   " + response.getStatusLine().getReasonPhrase());
        if (response.getStatusLine().getStatusCode() == 201) {
            return putRequestURL;
        }
    } catch (Exception e) {

        logger.error("Error: " + e.getMessage());
        throw new RuntimeException(e);
    }
    return null;
}

```

## Save Form Data in Azure

```java
@Override
 public String saveFormDatainAzure(String formData, String contentType) {
     String sasToken = azurePortalConfigurationService.getSASToken();
     String storageURI = azurePortalConfigurationService.getStorageURI();
     logger.debug("The SAS Token is " + sasToken);
     logger.debug("The Storage URL is " + storageURI);
     logger.debug("The form data is " + formData);
     int timeout = 5;
     RequestConfig config = RequestConfig.custom()
         .setConnectTimeout(timeout * 1000)
         .setConnectionRequestTimeout(timeout)
         .setSocketTimeout(timeout * 1000).build();
     org.apache.http.impl.client.CloseableHttpClient httpClient = HttpClientBuilder.create().setDefaultRequestConfig(config).build();
     UUID uuid = UUID.randomUUID();
     String putRequestURL = storageURI + uuid.toString();
     putRequestURL = putRequestURL + sasToken;
     logger.debug("The put Request " + putRequestURL);
     HttpPut httpPut = new HttpPut(putRequestURL);
     httpPut.addHeader("x-ms-blob-type", "BlockBlob");
     httpPut.addHeader("Content-Type", contentType);
     try {
         httpPut.setEntity(new StringEntity(formData));
         CloseableHttpResponse response = httpClient.execute(httpPut);
         logger.debug("Response code " + response.getStatusLine().getStatusCode());
         System.out.println("The response code is " + response.getStatusLine().getStatusCode() + "uuid " + uuid.toString());
         if (response.getStatusLine().getStatusCode() == 201) {
             return uuid.toString();
         }
     } catch (IOException e) {
         logger.error("Error: " + e.getMessage());
         throw new RuntimeException(e);
     }
     return null;

 }
```

## Next Steps

[Write OSGi configuration](./create-osgi-configuration.md)
