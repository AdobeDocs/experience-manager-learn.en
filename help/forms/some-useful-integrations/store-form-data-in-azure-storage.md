---
title: Store form submission in Azure Storage
description: Store form data in Azure Storage using REST API
feature: Adaptive Forms
version: 6.5
topic: Development
role: Developer
level: Beginner
last-substantial-update: 2023-08-14
kt: 13781
exl-id: 2bec5953-2e0c-4ae6-ae98-34492d4cfbe4
---
# Store form submissions in Azure Storage

This article shows you how to make REST calls to store submitted AEM Forms data in Azure Storage.
To be able to store submitted form data in Azure Storage, the following steps must be followed.

## Create Azure Storage account

[Login to your Azure portal account and create a storage account](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-create?tabs=azure-portal#create-a-storage-account-1). Provide a meaningful name to your storage account, click Review and then click Create. This creates your storage account with all the default values. For the purpose of this article we have named our storage account `aemformstutorial`.

## Create shared access

We'll be making us of the Shared Access Signature or SAS Method of authorization to interact with the Azure Storage container.
From the storage account page in the portal click Shared Access Signature
 menu item on the left to open the new shared access signature key settings page. Make sure you specify the settings and the appropriate End date as shown in the screenshot below and click on Generate SAS and connection string button. Copy the Blob Service SAS url. We will be using this URL to make our HTTP calls
 ![shared-access-keys](./assets/shared-access-signature.png)

## Create container

The next thing we need to do is to create a container to store the data from form submissions.
From the storage account page, click on the Containers menu item on the left and create a container called `formssubmissions`. Make sure the public access level is set to private
![container](./assets/new-container.png)

## Create PUT request

The next step is to create a PUT request to store the submitted form data in Azure Storage. We will have to modify the Blob Service SAS url to include the container name and the BLOB ID in the URL. Every form submission needs to be identified by a unique BLOB ID. The unique BLOB ID is typically created in your code and inserted in the url of the PUT request.
The following is the partial URL of the PUT request. The `aemformstutorial` is the name of the storage account, formsubmissions is the container in which the data will be stored with unique BLOB ID. The rest of the url will be remain the same. 
https://aemformstutorial.blob.core.windows.net/formsubmissions/00cb1a0c-a891-4dd7-9bd2-67a22bef3b8b?...............

The following is function written to store the submitted form data in Azure Storage using a PUT request. Notice the use of container name and the uuid in the url. You can create an OSGi service or a sling servlet using the sample code listed below and store the form submissions in Azure Storage.

``` java
 public String saveFormDatainAzure(String formData) {
        System.out.println("in SaveFormData!!!!!"+formData);
        org.apache.http.impl.client.CloseableHttpClient httpClient = HttpClientBuilder.create().build();
        UUID uuid = UUID.randomUUID();
        
        String url = "https://aemformstutorial.blob.core.windows.net/formsubmissions/"+uuid.toString();
        url = url+"?sv=2022-11-02&ss=bf&srt=o&sp=rwdlaciytfx&se=2024-06-28T00:42:59Z&st=2023-06-27T16:42:59Z&spr=https&sig=v1MR%2FJuhEledioturDFRTd9e2fIDVSGJuAiUt6wNlkLA%3D";
        HttpPut httpPut = new HttpPut(url);
        httpPut.addHeader("x-ms-blob-type","BlockBlob");
        httpPut.addHeader("Content-Type","text/plain");
        try {
            httpPut.setEntity(new StringEntity(formData));
            CloseableHttpResponse response = httpClient.execute(httpPut);
            log.debug("Response code "+response.getStatusLine().getStatusCode());
        } catch (IOException e) {
            log.error("Error: "+e.getMessage());
            throw new RuntimeException(e);
        }
        return uuid.toString();


    }

```

## Verify stored data in the container

![form-data-in-container](./assets/form-data-in-container.png)
