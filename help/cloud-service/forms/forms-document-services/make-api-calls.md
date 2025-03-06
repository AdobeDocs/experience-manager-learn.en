---
title: Using usagerights API
description: Sample code to Apply Usage Rights to the supplied PDF
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Cloud Service
feature: Document Services
topic: Development
jira: KT-17479
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
exl-id: a4e2132b-3cfd-4377-8998-6944365edec5
---
# Make API Call

## Apply Usage Rights

Once you have the access token, the next step is to make an API request to apply usage rights to the specified PDF. This involves including the access token in the request header to authenticate the call, ensuring secure and authorized processing of the document.

The following function applies the usage rights

``` java
public void applyUsageRights(String accessToken,String endPoint) {

            String host = "https://" + BUCKET + ".adobeaemcloud.com";
            String url = host + endPoint;
            String usageRights = "{\"comments\":true,\"embeddedFiles\":true,\"formFillIn\":true,\"formDataExport\":true}";

            logger.info("Request URL: {}", url);
            logger.info("Access Token: {}", accessToken);

            ClassLoader classLoader = DocumentGeneration.class.getClassLoader();
            URL pdfFile = classLoader.getResource("pdffiles/withoutusagerights.pdf");

            if (pdfFile == null) {
                logger.error("PDF file not found!");
                return;
            }

            File fileToApplyRights = new File(pdfFile.getPath());
            CloseableHttpClient httpClient = null;
            CloseableHttpResponse response = null;
            InputStream generatedPDF = null;
            FileOutputStream outputStream = null;
            
            try {
                httpClient = HttpClients.createDefault();
                byte[] fileContent = FileUtils.readFileToByteArray(fileToApplyRights);
                MultipartEntityBuilder builder = MultipartEntityBuilder.create();
                builder.addBinaryBody("document", fileContent, ContentType.create("application/pdf"),fileToApplyRights.getName());
                builder.addTextBody("usageRights", usageRights, ContentType.APPLICATION_JSON);
                
                HttpPost httpPost = new HttpPost(url);
                httpPost.addHeader("Authorization", "Bearer " + accessToken);
                httpPost.addHeader("X-Adobe-Accept-Experimental", "1");
                httpPost.setEntity(builder.build());
                
                response = httpClient.execute(httpPost);
                generatedPDF = response.getEntity().getContent();
                byte[] bytes = IOUtils.toByteArray(generatedPDF);

                outputStream = new FileOutputStream(SAVE_LOCATION + File.separator + "ReaderExtended.pdf");
                outputStream.write(bytes);
                logger.info("ReaderExtended File is  saved at "+SAVE_LOCATION);
            } catch (IOException e) {
                logger.error("Error applying usage rights", e);
            } finally {
                try {
                    if (generatedPDF != null) generatedPDF.close();
                    if (response != null) response.close();
                    if (httpClient != null) httpClient.close();
                    if (outputStream != null) outputStream.close();
                } catch (IOException e) {
                    logger.error("Error closing resources", e);
                }
            }
        }

```

## Function Breakdown:



*   **Setup API Endpoint & Payload**  
    *   Constructs the API URL using the provided `endPoint` and a predefined `BUCKET`.  
    *   Defines a JSON string (`usageRights`) specifying the rights to be applied, such as:
        * Comments  
        * Embedded files  
        * Form fill-in  
        * Form data export  

*   **Load the PDF File**  
    * Retrieves the `withoutusagerights.pdf` file from the `pdffiles` directory.  
    * Logs an error and exits if the file is not found.  

*   **Prepare the HTTP Request**  
    *   Reads the PDF file into a byte array.  
    *   Uses `MultipartEntityBuilder` to create a multi-part request containing:
        * The PDF file as a binary body.  
        * The `usageRights` JSON as a text body.  
    *   Sets up an HTTP `POST` request with headers:
        * `Authorization: Bearer <accessToken>` for authentication.  
        * `X-Adobe-Accept-Experimental: 1` (possibly required for API compatibility).  

*   **Send the Request & Handle Response**  
    * Executes the HTTP request using `httpClient.execute(httpPost)`.  
    * Reads the response (expected to be the updated PDF with usage rights applied).  
    * Writes the received PDF content to **"ReaderExtended.pdf"** at `SAVE_LOCATION`.  

*   **Error Handling & Cleanup**  
    * Catches and logs any `IOException` errors.  
    * Ensures all resources (streams, HTTP client, response) are closed properly in the `finally` block.  

The following is the main.java code which invokes the applyUsageRights function

```java
package com.aemformscs.communicationapi;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class Main {
    private static final Logger logger = LoggerFactory.getLogger(Main.class);

    public static void main(String[] args) {
        try {
            String accessToken = new AccessTokenService().getAccessToken();
            DocumentGeneration docGen = new DocumentGeneration();

            docGen.applyUsageRights(accessToken, "/adobe/document/assure/usagerights");

            // Uncomment as needed
            // docGen.extractPDFProperties(accessToken, "/adobe/document/extract/pdfproperties");
            // docGen.mergeDataWithXdpTemplate(accessToken, "/adobe/document/generate/pdfform");

        } catch (Exception e) {
            logger.error("Error occurred: {}", e.getMessage(), e);
        }
    }
}

```

The `main` method initializes by calling `getAccessToken()` from `AccessTokenService`, which is expected to return a valid token.

*   It then calls `applyUsageRights()` from the `DocumentGeneration` class, passing in:
    * The retrieved `accessToken`
    * The API endpoint for applying usage rights.


## Next Steps

[Deploy the sample project](sample-project.md)
