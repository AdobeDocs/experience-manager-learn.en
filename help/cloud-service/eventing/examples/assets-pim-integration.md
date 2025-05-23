---
title: AEM Assets events for PIM integration
description: Learn how to integrate AEM Assets and Product Information Management (PIM) systems for asset metadata updates.
version: Experience Manager as a Cloud Service
feature: Developing, App Builder
topic: Development, Architecture, Content Management
role: Architect, Developer
level: Beginner
doc-type: Tutorial
duration: 761
last-substantial-update: 2024-02-13
jira: KT-14901
thumbnail: KT-14901.jpeg
exl-id: 070cbe54-2379-448b-bb7d-3756a60b65f0
---
# AEM Assets events for PIM integration

>[!IMPORTANT]
>
>This tutorial uses OpenAPI-based AEM APIs. They are available as part of an early access program, if you are interested in accessing them, we encourage you to email [aem-apis@adobe.com](mailto:aem-apis@adobe.com) with a description of your use case.

Learn how to receive an AEM Event and act on it to update the content state in AEM using the OpenAPI-based Assets Author API.

How to process the received event depends on the business requirements. For example, the event data can be used to update the third-party system, or AEM, or both. 

This example demonstrates how a third-party system, such as a Product Information Management (PIM) system, can be integrated with AEM as a Cloud Service Assets. Upon receiving an AEM Assets event, it is processed to retrieve additional metadata from the PIM system and update the asset metadata in AEM. The updated asset metadata can include additional information like SKU, supplier name, or other product details.

To receive and process the AEM Assets event, the [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/guides/overview/what_is_runtime/), a serverless platform is used. However, other event processing systems like Webhook in your third-party system or Amazon EventBridge can also be used.

The high-level flow of the integration is as follows:

![AEM Assets events for PIM integration](../assets/examples/assets-pim-integration/aem-assets-pim-integration.png)

1. The AEM Author service triggers an _Asset Processing Completed_ event when an asset upload is completed and all asset processing activities are also completed. Waiting for asset processing to complete ensures that any out-of-the-box processing, such as metadata extraction, has been completed.
1. The event is sent to the [Adobe I/O Events](https://developer.adobe.com/events/) service.
1. The Adobe I/O Events service passes the event to the [Adobe I/O Runtime Action](https://developer.adobe.com/runtime/docs/guides/using/creating_actions/) for processing.
1. The Adobe I/O Runtime Action calls the API of the PIM system to retrieve additional metadata like SKU, supplier information, or other details.
1. The additional metadata retrieved from the PIM is then updated in AEM Assets using the OpenAPI-based [Assets Author API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/).

## Prerequisites

To complete this tutorial, you need:

- AEM as a Cloud Service environment with [AEM Eventing enabled](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/events/#enable-aem-events-on-your-aem-cloud-service-environment). Also, the sample [WKND Sites](https://github.com/adobe/aem-guides-wknd?#aem-wknd-sites-project) project must be deployed on to it.

- Access to the [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started).

- [Adobe Developer CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/) installed on your local machine.

## Development steps

The high-level development steps are:

1. [Modernization of AEM as a Cloud Service environment](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis#modernization-of-aem-as-a-cloud-service-environment)
1. [Enable AEM APIs access](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis#enable-aem-apis-access)
1. [Create a project in the Adobe Developer Console (ADC)](./runtime-action.md#Create-project-in-Adobe-Developer-Console)
1. [Initialize the project for local development](./runtime-action.md#initialize-project-for-local-development)
1. Configure the project in ADC
1. Configure the AEM Author service to enable ADC project communication
1. Develop a runtime action to orchestrate
    1. metadata retrieval from the PIM system
    1. metadata update in AEM Assets using the Assets Author API
1. Create and apply asset metadata schema
1. Verification of asset upload and metadata update

For details on steps 1-2, refer to the [Invoke OpenAPI-based AEM APIs](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) guide and for steps 3-4 refer to the [Adobe I/O Runtime Action and AEM Events](./runtime-action.md#) example. For steps 5-9, refer to the following sections.

### Configure the project in Adobe Developer Console (ADC)

To receive AEM Assets Events and execute the Adobe I/O Runtime Action created in the previous step, configure the project in ADC.

- In ADC, navigate to the [project](https://developer.adobe.com/console/projects) that you created in step-3. From that project, select the `Stage` workspace here the runtime action is deployed when you run `aio app deploy` as part of the step-4 instructions.

- Click the **Add Service** button and select the **Event** option. In the **Add Events** dialog, select **Experience Cloud** > **AEM Assets**, and click **Next**. 
    ![AEM Assets Event - add event](../assets/examples/assets-pim-integration/add-aem-assets-event.png)

- In the **Configure event registration** step, select the desired AEMCS instance, then _Asset Processing Completed_ event, and the OAuth Server-to-Server authentication type. 
  
    ![AEM Assets Event - configure event](../assets/examples/assets-pim-integration/configure-aem-assets-event.png)

- Finally, in the **How to receive events** step, expand the **Runtime action** option and select the _generic_ action created in the previous step. Click **Save configured events**.

    ![AEM Assets Event - receive event](../assets/examples/assets-pim-integration/receive-aem-assets-event.png)

- Likewise, click the **Add Service** button and select the **API** option. In the **Add an API** modal, select **Experience Cloud** > **AEM Assets Author API** and click **Next**. 

    ![Add AEM Assets Author API - Configure project](../assets/examples/assets-pim-integration/add-aem-api.png)

- Then select **OAuth Server-to-Server** for authentication type and click **Next**.

- Then select the correct **Product Profile** that is associated with the AEM Assets environment from which the event is being produced and have sufficient access to update assets there. Finally, click the **Save configured API** button.

    ![Add AEM Assets Author API - Configure project](../assets/examples/assets-pim-integration/add-aem-api-product-profile-select.png)
 
  In my case the _AEM Administrators - author - Program XXX - Environment YYY_ product profile is selected, it has **AEM Assets API Users** service enabled.

    ![Add AEM Assets Author API - Example Product Profile](../assets/examples/assets-pim-integration/aem-api-product-profile.png)

## Configure AEM instance to enable ADC Project communication

To enable the ADC Project's OAuth Server-to-Server credential ClientID to communication with the AEM instance, you need to configure the AEM instance.

It is done by defining the configuration in the `api.yaml` file in the AEM Project. Then, deploy the `api.yaml` file using the Config Pipeline in the Cloud Manager.

- In AEM Project, locate or create the `api.yaml` file from the `config` folder.

    ![Locate API YAML](../assets/examples/assets-pim-integration/locate-api-yaml.png)

- Add the following configuration to the `api.yaml` file.

    ```yaml
    kind: "API"
    version: "1.0"
    metadata: 
        envTypes: ["dev", "stage", "prod"]
    data:
        allowedClientIDs:
            author:
            - "<ADC Project's OAuth Server-to-Server credential ClientID>"
    ```

    Replace `<ADC Project's OAuth Server-to-Server credential ClientID>` with the actual ClientID of the ADC Project's OAuth Server-to-Server credential.

  >[!CAUTION]
  >
  > For demo purposes, the same ClientID is used for all environments. It is recommended to use separate ClientID per environment (dev, stage, prod) for better security and control.


- Commit the config changes to the Git repository and push the changes to the remote repository.

- Deploy the above changes using the Config Pipeline in the Cloud Manager. Note that the `api.yaml` file can also be installed in an RDE, using command line tooling.

    ![Deploy API YAML](../assets/examples/assets-pim-integration/config-pipeline.png)

### Develop runtime action

To perform the metadata retrieval and update, start by updating the auto created _generic_ action code in `src/dx-excshell-1/actions/generic` folder. 

Refer to the attached [WKND-Assets-PIM-Integration.zip](../assets/examples/assets-pim-integration/WKND-Assets-PIM-Integration.zip) file for the complete code, and the below section highlights the key files.

- The `src/dx-excshell-1/actions/generic/mockPIMCommunicator.js` file mocks the PIM API call to retrieve additional metadata like SKU and supplier name. This file is used for demo purposes. Once you have the end-to-end flow working, replace this function with a call to your real PIM system to retrieve metadata for the asset.

    ```javascript
    /**
     * Mock PIM API to get the product data such as SKU, Supplier, etc.
     *
     * In a real-world scenario, this function would call the PIM API to get the product data.
     * For this example, we are returning mock data.
     *
     * @param {string} assetId - The assetId to get the product data.
     */
    module.exports = {
        async getPIMData(assetId) {
            if (!assetId) {
            throw new Error('Invalid assetId');
            }
            // Mock response data for demo purposes
            const data = {
            SKUID: 'MockSKU 123',
            SupplierName: 'mock-supplier',
            // ... other product data
            };
            return data;
        },
    };
    ```

- The `src/dx-excshell-1/actions/generic/aemCommunicator.js` file updates the asset metadata in AEM using the [Assets Author API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/).

    ```javascript
    const fetch = require('node-fetch');
    ...
    /**
    *  Get IMS Access Token using Client Credentials Flow
    *
    * @param {*} clientId - IMS Client ID from ADC project's OAuth Server-to-Server Integration
    * @param {*} clientSecret - IMS Client Secret from ADC project's OAuth Server-to-Server Integration
    * @param {*} scopes - IMS Meta Scopes from ADC project's OAuth Server-to-Server Integration as comma separated strings
    * @returns {string} - Returns the IMS Access Token
    */
    async function getIMSAccessToken(clientId, clientSecret, scopes) {
      const adobeIMSV3TokenEndpointURL = 'https://ims-na1.adobelogin.com/ims/token/v3';
      const options = {
        method: 'POST',
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded',
        },
        body: `grant_type=client_credentials&client_id=${clientId}&client_secret=${clientSecret}&scope=${scopes}`,
      };
      const response = await fetch(adobeIMSV3TokenEndpointURL, options);
      const responseJSON = await response.json();
      return responseJSON.access_token;
    }    
    async function updateAEMAssetMetadata(metadataDetails, aemAssetEvent, params) {
      ...
      // Transform the metadata details to JSON Patch format,
      // see https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/#operation/patchAssetMetadata
      const transformedMetadata = Object.keys(metadataDetails).map((key) => ({
        op: 'add',
        path: `wknd-${key.toLowerCase()}`,
        value: metadataDetails[key],
      }));
      ...
      // Get ADC project's OAuth Server-to-Server Integration credentials
      const clientId = params.ADC_CECREDENTIALS_CLIENTID;
      const clientSecret = params.ADC_CECREDENTIALS_CLIENTSECRET;
      const scopes = params.ADC_CECREDENTIALS_METASCOPES;
      // Get IMS Access Token using Client Credentials Flow
      const access_token = await getIMSAccessToken(clientId, clientSecret, scopes);
      // Call AEM Author service to update the metadata using Assets Author API
      // See https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/
      const res = await fetch(`${aemAuthorHost}/adobe/assets/${assetId}/metadata`, {
        method: 'PATCH',
        headers: {
          'Content-Type': 'application/json-patch+json',
          'If-Match': '*',
          'X-Adobe-Accept-Experimental': '1',
          'X-Api-Key': '12345676', // Use the `ClientID` value from the ADC Project's credentials section
          Authorization: `Bearer ${access_token}`,
        },
        body: JSON.stringify(transformedMetadata),
      });
      ...
    }
    module.exports = { updateAEMAssetMetadata };
    ```

    The `.env` file stores the ADC Project's OAuth Server-to-Server credentials details, and they are passed as parameters to the action using `ext.config.yaml` file. Refer to the [App Builder Configuration Files](https://developer.adobe.com/app-builder/docs/guides/configuration/) for managing secrets and action parameters.
- The `src/dx-excshell-1/actions/model` folder contains `aemAssetEvent.js` and `errors.js` files, which are used by the action to parse the received event and handle errors respectively.
- The `src/dx-excshell-1/actions/generic/index.js` file uses the above mentioned modules to orchestrate the metadata retrieval and update.

    ```javascript
    ...
    let responseMsg;
    // handle the challenge probe request, they are sent by I/O to verify the action is valid
    if (params.challenge) {
      logger.info('Challenge probe request detected');
      responseMsg = JSON.stringify({ challenge: params.challenge });
    } else {
      logger.info('AEM Asset Event request received');
      // create AEM Asset Event object from request parameters
      const aemAssetEvent = new AEMAssetEvent(params);
      // Call mock PIM API to get the product data such as SKU, Supplier, etc.
      const mockPIMData = await mockPIMAPI.getPIMData(
        aemAssetEvent.getAssetName(),
      );
      logger.info('Mock PIM API response', mockPIMData);
      // Update PIM received data in AEM as Asset metadata
      const aemUpdateStatus = await updateAEMAssetMetadata(
        mockPIMData,
        aemAssetEvent,
        params,
      );
      logger.info('AEM Asset metadata update status', aemUpdateStatus);
      if (aemUpdateStatus) {
        // create response message
        responseMsg = JSON.stringify({
          message:
            'AEM Asset Event processed successfully, updated the asset metadata with PIM data.',
          assetdata: {
            assetName: aemAssetEvent.getAssetName(),
            assetPath: aemAssetEvent.getAssetPath(),
            assetId: aemAssetEvent.getAssetId(),
            aemHost: aemAssetEvent.getAEMHost(),
            pimdata: mockPIMData,
          },
        });
      } 
      // response object
      const response = {
        statusCode: 200,
        body: responseMsg,
      };
      // Return the response to the caller
      return response;
      ...
    }
    ```

- Deploy the updated action to Adobe I/O Runtime using the following command:

  ```bash
  $ aio app deploy
  ```

### Create and apply asset metadata schema

By default, the WKND Sites project does not have the asset metadata schema to display the PIM specific metadata like SKU, Supplier Name, etc. Let's create and apply the asset metadata schema to an asset folder in the AEM instance.

1. Log in to the AEM as a Cloud Service Asset instance and be in the [Asset view](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/authoring/switch-views).

    ![AEM Assets view](../assets/examples/assets-pim-integration/aem-assets-view.png)

1. Navigate to the **Settings** > **Metadata Forms** option from the left rail and click the **Create** button. In the **Create Metadata Form** dialog, enter the following details and click **Create**.
    - Name: `PIM`
    - Use existing form structure as template: `Check`
    - Choose from: `default`

    ![Create Metadata Form](../assets/examples/assets-pim-integration/create-metadata-form.png)

1. Click the **+** icon to add a new **PIM** tab and add **Single Line Text** components to it.     

    ![Add PIM Tab](../assets/examples/assets-pim-integration/add-pim-tab.png)

    The following table lists the metadata properties and their corresponding fields.

    | Label | Placeholder | Metadata property |
    | --- | --- | --- |
    | SKU | Auto populated via AEM Eventing integration | `wknd-skuid` |
    | Supplier Name | Auto populated via AEM Eventing integration | `wknd-suppliername` |

1. Click **Save** and **Close** to save the metadata form.

1. Finally, apply the **PIM** metadata schema to the **PIM** folder.

    ![Apply Metadata Schema](../assets/examples/assets-pim-integration/apply-metadata-schema.png)

With the above steps, the assets from the **Adventures** folder are ready to display the PIM specific metadata like SKU, Supplier Name, etc.

### Asset upload and metadata verification

To verify the AEM Assets and PIM integration, upload an asset to the **Adventures** folder in AEM Assets. The PIM tab in the asset details page should display the SKU and Supplier Name metadata.

  ![AEM Assets upload](../assets/examples/assets-pim-integration/aem-assets-metadata-update.png)

## Concept and key takeaways

The asset metadata synchronization between AEM and other systems like PIM are often required in the enterprise. Using AEM Eventing such requirements can be achieved. 

- The asset metadata retrieval code is executed outside of AEM, avoiding the load on the AEM Author service, thus an event-driven architecture that scales independently.
- The newly introduced Assets Author API is used to update the asset metadata in AEM.
- The API authentication uses OAuth server-to-server (aka client credentials flow), see [OAuth Server-to-Server credential implementation guide](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation).
- Instead of Adobe I/O Runtime Actions, other webhooks or Amazon EventBridge can be used to receive the AEM Assets event and process the metadata update.
- Asset Events via AEM Eventing empower businesses to automate and streamline critical processes, fostering efficiency and coherence across the content ecosystem.
