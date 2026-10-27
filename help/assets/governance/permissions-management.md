---
title: Permissions Management
description: Learn how to manage folder and asset permissions in AEM Assets with groups and access control lists, in both the Assets view and Admin view.
solution: Experience Manager, Experience Manager Assets
sub-product: Experience Manager Assets
version: Experience Manager as a Cloud Service
feature-set: Experience Manager Assets
feature: Asset Management
topic: Content Management
role: Admin, User
level: Beginner, Intermediate
doc-type: Feature Video
duration: 840
team: TM
last-substantial-update: 2026-10-20T00:00:00.000Z
jira: TODO
TQID: 'https://experienceleague.adobe.com/6x5uJAM--jYZXONv56q85iZjBVFw--bif-LfMJCQpO0'
product_v2:
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a45b1e7f-e65f-4cd3-be86-5cec5d9449ef
    internal-label: Content management
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: f6a6f91a-8819-530a-8e7b-c50884a25aef
    internal-label: Workflow
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
    internal-label: Governance
  - id: f8667931-f646-4dd3-af2a-b9d0cb8098ad
    internal-label: Taxonomy
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
---

# Permissions management {#permissions-management}

Every organization needs to control who can view, edit, or delete assets, especially as more teams and outside partners request access. AEM Assets manages this through group-based permissions, so you assign access by role, not one user at a time. Group-based permissions in the Assets view and the Admin view keep sensitive content secure while the right people still work fast.

>[!BEGINTABS]

>[!TAB Assets view]

Learn how to manage folder permissions in the Assets view so the right users and groups can view, edit, or manage your assets. Before you begin, [set up users and user groups in the Adobe Admin Console](./grant-access.md), then sign in to AEM Assets as an administrator.

Select a folder, open **More options**, and choose **Manage permissions**. This video shows how to:

* Assign **Can view** or **Can edit** permissions to user groups.
* Give a group view access to a parent folder and edit access to a specific subfolder.
* Assign **Owner** permission to an individual user so they can manage permissions within a folder tree without being a full administrator.
* Apply **Deny access** to **All authenticated users** to restrict a folder to the groups you explicitly grant access to, and acknowledge the warning that this change may affect your own permissions.

Manage permissions at the group level rather than for individual users, except when assigning a folder owner. Permissions apply to both browsing and search results, so users only see assets they have permission to access.

>[!VIDEO](https://video.tv.adobe.com/v/3504763?quality=12&learn=on)

>[!TAB Admin view]

In the Admin view, you create a custom user group for each role and make it a member of an AEM-provided group, such as **Contributors**, **DAM users**, or **Workflow users**, so it inherits a baseline set of permissions instead of a rebuild from scratch. Then you layer access control lists (ACLs) on top for specific folders. This video walks through a worked example, configured from **Tools > Security**: deny a creatives group write access at the root, then grant it in one subfolder.

>[!VIDEO](https://video.tv.adobe.com/v/37696?quality=12&learn=on)

>[!ENDTABS]
