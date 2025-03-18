---
title: Author a block
description: Author a Edge Delivery Services block with Universal Editor.
version: Cloud Service
feature: Edge Delivery Services
topic: Development
role: Developer
level: Beginner
doc-type: Tutorial
jira: KT-15832
duration: 500
exl-id: ca356d38-262d-4c30-83a0-01c8a1381ee6
---
# Author a block

After pushing the [teaser block's JSON](./5-new-block.md) to the `teaser` branch, the block becomes editable in the AEM Universal Editor.

Authoring a block in development is important for several reasons:

1. It verifies that the block's definition and model are accurate.
1. It allows developers to review the block's semantic HTML, which serves as the foundation for development.
1. It enables deployment of both the content and semantic HTML to the preview environment, supporting faster block development.
   
## Open Universal Editor using code from the `teaser` branch

1. Log in to AEM Author.
2. Navigate to **Sites** and select the site (WKND (Universal Editor)) created in the [previous chapter](./2-new-aem-site.md).

    ![AEM Sites](./assets/6-author-block/open-new-site.png)

3. Create or edit a page to add the new block, ensuring the context is available to support local development. While pages can be created anywhere within the site, it's often best to create discrete pages for each new body of work. Create a new "folder" page named **Branches**. Each sub-page is used to support the development of the same-named Git branch.

    ![AEM Sites - Create Branches page](./assets/6-author-block/branches-page-3.png)

4. Under the **Branches** page, create a new page titled **Teaser**, matching the development branch name, and click **Open** to edit the page.

    ![AEM Sites - Create Teaser page](./assets/6-author-block/teaser-page-3.png)

5. Update the Universal Editor to load the code from the `teaser` branch by adding `?ref=teaser` to the URL. Make sure to add the query parameter **BEFORE** the `#` symbol.

    ![Universal Editor - Select teaser branch](./assets/6-author-block/select-branch.png)

6. Select the first section under **Main**, click the **add** button, and choose the **Teaser** block.

    ![Universal Editor - Add Block](./assets/6-author-block/add-teaser-2.png)

7. On the canvas, select the newly added teaser and author the fields on the right, or via the inline editing capability.

    ![Universal Editor - Author Block](./assets/6-author-block/author-block.png)

8. After completing authoring, select the **Publish** button in the top right of Universal Editor, choose publish to **Preview**, and publish the changes to the preview environment. The changes are then published to the `aem.page` domain for the website.
    ![AEM Sites - Publish or Preview](./assets/6-author-block/publish-to-preview.png)

9. Wait for the changes to publish to preview, then open the webpage via the [AEM CLI](./3-local-development-environment.md#install-the-aem-cli) at [http://localhost:3000/branches/teaser](http://localhost:3000/branches/teaser).

    ![Local Site - Refresh](./assets/6-author-block/preview.png)

Now, the authored teaser block's content and semantic HTML are available on the preview website, ready for development using the AEM CLI in the local development environment.
