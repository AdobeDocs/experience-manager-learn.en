---
title: Associate page component with the new adaptive form template
description: Create a new page component
feature: Adaptive Forms
type: Documentation
role: Developer
level: Beginner
version: Experience Manager as a Cloud Service
topic: Integrations
exl-id: 7b2b1e1c-820f-4387-a78b-5d889c31eec0
duration: 25
TQID: https://experienceleague.adobe.com/i-9g9OftLo9-BQ6pIxQi5oWZRAl6yJOVmSqfg2nHK74
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ae478996-b206-4712-9b0c-dc78a2644453
    internal-label: Integrations
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
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
