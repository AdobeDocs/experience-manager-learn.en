---
title: Closed User Groups in AEM Assets
description: Closed User Groups (CUGs) is a feature used to restrict access to content to a select group of users on a published site. This video shows how Closed User Groups can be used with Adobe Experience Manager Assets to restrict access to a specific folder of assets.
version: Experience Manager 6.4, Experience Manager 6.5, Experience Manager as a Cloud Service
topic: Administration, Security
feature: User and Groups
role: Admin
level: Intermediate
jira: KT-649
thumbnail: 22155.jpg
last-substantial-update: 2026-08-27
doc-type: Feature Video
exl-id: a2bf8a82-15ee-478c-b7c3-de8a991dfeb8
duration: 321
TQID: https://experienceleague.adobe.com/mQ4O5-6QMPLqL0x5ywUZ13r1SmI9Putz-spFelrFJ7E
product_v2:
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: cda65036-5305-4f01-89da-9b3506ae8c50
    internal-label: Administration
  - id: da0dfbce-df02-4f8b-b32d-a4e3b1d05085
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# Closed user groups {#using-closed-user-groups-with-aem-assets}

Closed User Groups (CUGs) restrict access to content to a select group of users on a published site. Support for CUGs with AEM Assets was first introduced in AEM 6.4.

>[!BEGINTABS]

>[!TAB Admin view]

>[!VIDEO](https://video.tv.adobe.com/v/22155?quality=12&learn=on)

## Closed user group (CUG) with AEM Assets

* Designed to restrict access to assets on an AEM Publish instance.
* Grants read access to a set of users/groups.
* CUG can only be configured at a folder level. CUG cannot be set on individual assets.
* CUG policies are automatically inherited by any sub-folders and applied assets.
* CUG policies can be overridden by sub-folders by setting a new CUG policy. This should be used sparingly and is not considered a best practice.
* Changes to a folder's CUG policy take effect only after you publish the folder.
* You can require authentication on a folder and set a login page, so an unauthenticated user who tries to access a restricted asset directly lands there instead of a 404 error.

>[!CAUTION]
>
>Configure your dispatcher so it doesn't cache restricted content. Otherwise, an anonymous user could receive a cached copy of a page or asset that should require authentication.

## Closed user groups vs. access control lists {#closed-user-groups-vs-access-control-lists}

Both Closed User Groups (CUG) and Access Control Lists (ACL) are used to control access to content in AEM and based on AEM Security users and groups. However the application and implementation of these features is very different. The following table summarizes the distinctions between the two features.

|                   | ACL                                                                                                                              | CUG                                                                                                                           |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Intended Use      | Configure and apply permissions for content on the **current** AEM instance.                                                     | Configure CUG policies for content on AEM **author** instance. Apply CUG policies for content on AEM **publish** instance(s). |
| Permission Levels | Defines granted/denied permissions for users/groups for all levels: Read, Modify, Create, Delete, Read ACL, Edit ACL, Replicate. | Grants read access to a set of users/groups. Denies read access to *all other* users/groups.                                    |
| Publication       | ACLs are *not* published with content.                                                                                            | CUG policies *are* published with content.                                                                                     |

## Supporting links {#supporting-links}

* [Managing Assets and Closed User Groups](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/managing/manage-assets#closed-user-group)
* [Creating a Closed User Group](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/cug)
* [Oak Closed User Group Documentation](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html)

>[!ENDTABS]
