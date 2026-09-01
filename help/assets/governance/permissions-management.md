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
duration: 1049
team: TM
last-substantial-update: 2026-08-27
jira: TODO
product_v2:
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: a45b1e7f-e65f-4cd3-be86-5cec5d9449ef
    internal-label: Content management
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

AEM Assets controls access to assets through group-based permissions, whether you manage them in the Assets view or the Admin view.

>[!BEGINTABS]

>[!TAB Assets view]

## Manage permissions

Set up administrators and user groups in the Adobe Admin Console, then apply **Can view** or **Can edit** permission to a folder for a specific group, or assign a user as a folder's owner. This video shows the whole flow, including how a deny rule at one folder limits what you can grant beneath it.

>[!VIDEO](https://video.tv.adobe.com/v/342113?quality=12&learn=on)

>[!TAB Admin view]

## Manage permissions

Create a custom user group for each role and make it a member of an AEM-provided group, such as **Contributors**, **DAM users**, or **Workflow users**, so it inherits a baseline set of permissions instead of a rebuild from scratch. Then layer access control lists (ACLs) on top for specific folders. This video walks through a worked example, configured from **Tools > Security**: deny a creatives group write access at the root, then grant it in one subfolder.

>[!VIDEO](https://video.tv.adobe.com/v/37696?quality=12&learn=on)

>[!ENDTABS]
