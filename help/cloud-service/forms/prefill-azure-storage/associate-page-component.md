---
title: Associate page component with the new adaptive form template
description: Create a new page component
feature: Adaptive Forms
type: Documentation
role: Developer
level: Beginner
version: Cloud Service
topic: Integrations
exl-id: 7b2b1e1c-820f-4387-a78b-5d889c31eec0
duration: 35
---
# Associate the page component with the template

The next step is to asscociate the page component with the new adaptive form template. This ensures the code in the page component will be executed every time an adaptive form based on the new template is rendered. For the purpose of this tutorial a new adaptive form template called **StoreAndRestoreFromAzure** was created in the **AzurePortalStorage** folder.
Navigate to /conf/AzurePortalStorage/settings/wcm/templates/storeandrestorefromazure/initial/jcr:content node, add the following property and save the changes.

| **Property Name**  | **Property Type** | **Property Value**                                    |
|--------------------|-------------------|-------------------------------------------------------|
| sling:resourceType | String            | azureportalpagecomponent/component/page/storeandfetch |

Navigate to /conf/AzurePortalStorage/settings/wcm/templates/storeandrestorefromazure/structure/jcr:content node,add the following property and save the changes.
| **Property Name**  | **Property Type** | **Property Value**                                    |
|--------------------|-------------------|-------------------------------------------------------|
| sling:resourceType | String            | azureportalpagecomponent/component/page/storeandfetch |


## Next Steps

[Create integration with Azure Storage](./create-fdm.md)
