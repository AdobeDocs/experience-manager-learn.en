---
title: Closed User Groups in AEM Assets
description: Closed User Groups (CUGs) is a feature used to restrict access to content to a select group of users on a published site. This video shows how Closed User Groups can be used with Adobe Experience Manager Assets to restrict access to a specific folder of assets.
version:  6.4, 6.5, Cloud Service
topic: Administration, Security
feature: User and Groups
role: Admin
level: Intermediate
kt: 649
thumbnail: 22155.jpg
last-substantial-update: 2022-06-06
exl-id: a2bf8a82-15ee-478c-b7c3-de8a991dfeb8
---
# Closed User Groups{#using-closed-user-groups-with-aem-assets}

Closed User Groups (CUGs) is a feature used to restrict access to content to a select group of users on a published site. This video shows how Closed User Groups can be used with Adobe Experience Manager Assets to restrict access to a specific folder of assets. Support for Closed User Groups with AEM Assets was first introduced in AEM 6.4.

>[!VIDEO](https://video.tv.adobe.com/v/22155?quality=12&learn=on)

## Closed User Group (CUG) with AEM Assets

* Designed to restrict access to assets on an AEM Publish instance.
* Grants read access to a set of users/groups.
* CUG can only be configured at a folder level. CUG cannot be set on individual assets.
* CUG policies are automatically inherited by any sub-folders and applied assets.
* CUG policies can be overridden by sub-folders by setting a new CUG policy. This should be used sparingly and is not considered a best practice.

## Closed User Groups vs. Access Control Lists {#closed-user-groups-vs-access-control-lists}

Both Closed User Groups (CUG) and Access Control Lists (ACL) are used to control access to content in AEM and based on AEM Security users and groups. However the application and implementation of these features is very different. The following table summarizes the distinctions between the two features.

|                   | ACL                                                                                                                              | CUG                                                                                                                           |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Intended Use      | Configure and apply permissions for content on the **current** AEM instance.                                                     | Configure CUG policies for content on AEM **author** instance. Apply CUG policies for content on AEM **publish** instance(s). |
| Permission Levels | Defines granted/denied permissions for users/groups for all levels: Read, Modify, Create, Delete, Read ACL, Edit ACL, Replicate. | Grants read access to a set of users/groups. Denies read access to *all other* users/groups.                                    |
| Publication       | ACLs are *not* published with content.                                                                                            | CUG policies *are* published with content.                                                                                     |

## Supporting Links {#supporting-links}

* [Managing Assets and Closed User Groups](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html?lang=en#closed-user-group)
* [Creating a Closed User Group](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html)
* [Oak Closed User Group Documentation](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html)
