---
title: Store form submission in Azure Storage
description: Store form data in Azure Storage using REST API
feature: Adaptive Forms
version: 6.5
topic: Development
role: Developer
level: Beginner
last-substantial-update: 2023-10-23
jira: KT-14238
duration: 108
exl-id: 77f93aad-0cab-4e52-b0fd-ae5af23a13d0
---
# Fetch data from Azure storage

This article shows you how to populate an adaptive form with the data stored in Azure storage.
It is assumed that you have stored the adaptive form data in Azure storage and now want to prepopulate your adaptive form with that data.

## Create GET request

The next step is to write the code to fetch the data from the Azure Storage using the blobID. The following code was written to fetch the data. The url was constructed using the sasToken and storageURI values from the OSGi configuration and the blobID passed to the getBlobData function 

``` java
 @Override
public String getBlobData(String blobID) {
    String sasToken = azurePortalConfigurationService.getSASToken();
    String storageURI = azurePortalConfigurationService.getStorageURI();
    log.debug("The SAS Token is " + sasToken);
    log.debug("The Storage URL is " + storageURI);
    String httpGetURL = storageURI + blobID;
    httpGetURL = httpGetURL + sasToken;
    HttpGet httpGet = new HttpGet(httpGetURL);

    org.apache.http.impl.client.CloseableHttpClient httpClient = HttpClientBuilder.create().build();
    CloseableHttpResponse httpResponse = null;
    try {
        httpResponse = httpClient.execute(httpGet);
        HttpEntity httpEntity = httpResponse.getEntity();
        String blobData = EntityUtils.toString(httpEntity);
        log.debug("The blob data I got was " + blobData);
        return blobData;

    } catch (ClientProtocolException e) {

        log.debug("Got Client Protocol Exception " + e.getMessage());
    } catch (IOException e) {

        log.debug("Got IOEXception " + e.getMessage());
    }

    return null;
}
```

When an adaptive form is rendered with a guid parameter in the url, the custom page component associated with the template fetches and populates the adaptive form with the data from Azure storage.
The following is the code in the jsp of the page component asscoiated with the template

```java
com.aemforms.saveandfetchfromazure.StoreAndFetchDataFromAzureStorage azureStorage = sling.getService(com.aemforms.saveandfetchfromazure.StoreAndFetchDataFromAzureStorage.class);


String guid = request.getParameter("guid");

if(guid!=null&&!guid.isEmpty())
{
    String dataXml = azureStorage.getBlobData(guid);
    slingRequest.setAttribute("data",dataXml);

}

``` 

## Test the solution

* [Deploy the custom OSGi bundle](./assets/SaveAndFetchFromAzure.core-1.0.0-SNAPSHOT.jar)

* [Import the custom adaptive form template and the page component associated with the template](./assets/store-and-fetch-from-azure.zip)

* [Import the sample adaptive form](./assets/bank-account-sample-form.zip)

* Specify the appropriate values in the Azure Portal Configuration using the OSGi configuration console.

* [Preview and submit the BankAccount form](http://localhost:4502/content/dam/formsanddocuments/azureportalstorage/bankaccount/jcr:content?wcmmode=disabled)

* Verify the data is stored in the Azure storage container of your choice. Copy the Blob ID.

* [Preview the BankAccount form](http://localhost:4502/content/dam/formsanddocuments/azureportalstorage/bankaccount/jcr:content?wcmmode=disabled&guid=dba8ac0b-8be6-41f2-9929-54f627a649f6) and specify the Blob ID as a guid parameter in the URL for the form to be prepopulated with the data from Azure storage
