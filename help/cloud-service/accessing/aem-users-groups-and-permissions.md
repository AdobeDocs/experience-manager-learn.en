---
title: AEM users, groups and permissions
description: Adobe Experience Manager builds on Adobe IMS users, user groups, and product profiles in order to provide users customizable access to AEM. Learn how to define AEM groups and permissions and how they work in concert with Adobe IMS abstractions to provide seamless and customizable access to AEM.
version: Experience Manager as a Cloud Service
topic: Administration, Security
feature: User and Groups
role: Admin
level: Beginner
jira: KT-6060
thumbnail: 39151.jpg
exl-id: 7d7942ae-7e38-4abd-9900-5b8e3542f5e1
duration: 315
TQID: https://experienceleague.adobe.com/2XlS8qaJu34pMH5h9IcDWmOn2GEMN-fpntt37eIpWus
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# AEM users, groups and permissions {#aem-users-groups-and-permissions}

>[!CONTEXTUALHELP]
>id="aemcloud_adobeims_aem_users_groups"
>title="AEM Users, Groups & Permissions"
>abstract="Adobe Experience Manager builds on Adobe IMS users, user groups, and product profiles in order to provide users customizable access to AEM. Learn how to define AEM groups and permissions and how they work in concert with Adobe IMS abstractions to provide seamless and customizable access to AEM."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=en" text="IMS Support for Adobe Experience Manager as a Cloud Service"
>additional-url="https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.html" text="AEM-provided user groups and their permissions"

Adobe Experience Manager builds on Adobe IMS users, user groups, and product profiles in order to provide users customizable access to AEM. Learn how to define AEM groups and permissions, that build upon [AEM's provided user groups](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/security#built-in-users-and-groups),  and how they work in concert with Adobe IMS abstractions to provide seamless and customizable access to AEM.

>[!VIDEO](https://video.tv.adobe.com/v/39151?quality=12&learn=on)


## AEM Assets permissions and access control {#assets-permissions-and-access-control}

Access to Adobe Experience Manager (AEM) Assets is controlled by two independent layers that must be configured correctly:

1. **[!UICONTROL Adobe Admin Console product]** profiles: grants the technical entitlement to reach an AEM environment, for example, Power User, Collaborator, Limited User, and Administrators.
2. **[!UICONTROL AEM-local group membership and ACLs]**: controls what you can actually do once inside that environment, for example, upload, edit, delete, approve, and configure.

Assigning a product profile in Admin Console is necessary but not sufficient: a user can be a fully licensed Power User in Admin Console and still be blocked from every asset operation if they are not also placed in the correct AEM-local group. Conversely, correct AEM-local group membership has no effect if the user was never granted an Admin Console product profile for the environment.

### Permissions required for common operations {#permissions-required-for-common-operations}

| Operation | Required permission or group | Notes |
| -------- | -------- | -------- |
| Upload an asset to **[!UICONTROL /content/dam]** | **[!UICONTROL rep:write]** on the **[!UICONTROL target /content/dam path]** | Group membership alone does not guarantee that this is inherited at the user level. If uploads fail for specific users while others in the same group succeed, verify **[!UICONTROL rep:write]** is actually present on the user's effective ACL and not just assumed from group membership. |
| Search or view assets in the Digital Asset Management (DAM) UI | Read access to **[!UICONTROL /content/dam]** (typically through dam-users) and **[!UICONTROL jcr:read]** on **[!UICONTROL /conf/global/settings/dam/adminui-extension/metadataschema]**. | The Assets UI resolves the metadata schema definitions from **[!UICONTROL /conf]** to render results. If a group has full **[!UICONTROL /content/dam]** access but no read access to the schema configuration path, the UI throws a **[!UICONTROL NullPointerException]** and **[!UICONTROL search/browse]** silently fails. This is not a **[!UICONTROL /content/dam]** permission problem even though it looks like one. |
| Create or edit a Folder Profile | Membership in the local administrators group. | An Admin Console **[!UICONTROL Administrator]** assignment is not the same thing, the **[!UICONTROL Create]** button for folder profiles is only rendered for accounts that are also members of AEM's local administrators group. |
| Create or edit a custom metadata schema | Recursive **[!UICONTROL jcr:read]** on **[!UICONTROL /conf]**, **[!UICONTROL /conf/global/settings/dam/adminui-extension/metadataschema]**, and **[!UICONTROL jcr:write]** on **[!UICONTROL /conf/global/settings/dam/adminui-extension]** and its metadataschema subnode. | Write access to the metadataschema node alone is not enough; the schema editor also needs to read the parent **[!UICONTROL /conf]** tree to render correctly. |
| Edit asset metadata fields (for example, review status on Content Hub-ingested assets) | **[!UICONTROL dam-users]** group membership. | Applies even to assets ingested through Content Hub. The underlying edit permission is still AEM's standard DAM group model. |
| Use **[!UICONTROL Share Link]** action | **[!UICONTROL jcr:modifyAccessControl]** on the folder, and the group must not be excluded from **[!UICONTROL Allow only for groups]** | Configured under **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Assets Configurations]** > **[!UICONTROL Link Share]**. This has been observed to differ between environments (for example, it is present in the dev server, but missing in the production server) even with identical code, so you must check both the ACL and this configuration screen per environment. |
| License and save an Adobe Stock asset | Membership in both the Stock licensing group and the base DAM authoring group (for example, **[!UICONTROL dam-users]**) | Membership in the Stock group alone is not sufficient for the **[!UICONTROL License & Save]** workflow to complete. |
| View Bandwidth and Storage in Dynamic Media Classic | System administrator privileges. | Insufficient privileges surface as Scene7 error **[!UICONTROL #2046]** rather than a standard permission-denied message. |
| API access through a JSON Web Token (JWT) bearer token or technical account | The technical account's underlying AEM user must be explicitly added to the required AEM group (for example, a **[!UICONTROL view-only]** group). | Provisioning a product profile or service in the administrator console creates the technical account user. This does not automatically grant it every AEM group needed for complete API responses, for example, full rendition lists. The account's AEM group membership still needs separate configuration. |

### Group inheritance and permission evaluation {#group-inheritance-and-permission-evaluation}

* Permissions applied to a parent folder cascade to the child folders and assets by default.
* Explicit deny rules take precedence over allow rules. You can be a member of a group that has allowed access, but if you (directly or through another group) are also subject to a **[!UICONTROL jcr:read]** (or other) deny rule on that path or an ancestor path, the deny wins — even when both the cases appear to have identical group memberships in the administrator console.
* When two users with seemingly identical permissions behave differently, compare their effective ACLs (**[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Permissions]**, or the Repository Browser), not just their group membership lists. You must look specifically for deny rules scoped to one of the groups.

### Distinguishing group types {#distinguishing-group-types}

AEM does not visually separate group types in **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Groups]**, which makes large permission audits difficult. Use these rules to classify a group:

* **[!UICONTROL Out-of-the-box (OOTB)]** groups have fixed, well-known group IDs, for example, administrators, dam-users, and content-authors.
* **[!UICONTROL IMS-synced]** groups that are created automatically from the administrator console user groups carry a **[!UICONTROL rep:externalId]** property ending in **[!UICONTROL ;ims]**.
* Custom groups created directly in AEM have no **[!UICONTROL rep:externalId]** property.

Adobe's guidance is to treat OOTB and custom local groups as the primary building blocks for permissions, and treat IMS-synced groups purely as entry points that map administrator console assignments into AEM, not as a place to layer additional ad hoc ACLs.

### Content Hub and Brand Portal specific behavior {#content-hub-brand-portal-specific-behavior}

* Content Hub access is not controlled by dedicated Content Hub groups. It is controlled by environment-specific administrator console product profiles, typically named **[!UICONTROL AEM Assets Limited Users - delivery - Program <programId> - Environment <environmentId>]**.
* ContentHub access is granted only through the **[!UICONTROL Limited User]** product profile. The **[!UICONTROL Power User]** profile does not grant ContentHub access on its own. Assigning both the **[!UICONTROL Power User]** and **[!UICONTROL Limited User]** to the same account does not double-consume licenses.
* Content Hub administrator rights require membership in specific product profiles (**[!UICONTROL AEM Assets Limited Users – delivery and AEM Administrators – production author]**). The visibility of the **[!UICONTROL Admin]** tab in the UI is not itself proof of administrator rights.
* Attribute-Based Access Control (ABAC) rules, when enabled, are configured self-service through the AI assistant or governance agent inside Content Hub; there is no separate dedicated ABAC permissions screen. If specific groups cannot see any assets in Content Hub despite correct-looking group or profile assignments, check whether ABAC policies are enabled and whether user attributes or asset metadata satisfy those policies before assuming a group misconfiguration.
* Changes made to users or groups in the administrator console are not reflected in Brand Portal in real time. A background synchronization job runs roughly every 8 hours, so allow 5–10 hours before troubleshooting a **[!UICONTROL changes not appearing report]** report as a bug.
* A collection marked public in Brand Portal is still inaccessible to the guest users if the underlying Digital Asset Management (DAM) folder is not public and the assets are not published from AEM Assets. Collection-level visibility does not override the folder-level visibility.
* A Closed User Group (CUG) applied to a DAM path can block publisher-side visibility per environment even after a successful replication. A missing **[!UICONTROL cq:lastReplicated]** property is a useful diagnostic signal that the asset was never actually published (as distinct from being blocked by CUG after publishing).

### Troubleshooting permission-denied errors {#troubleshooting-permission-denied-errors}

1. Confirm the administrator console product profile assignment for the correct environment (author versus delivery or Content Hub instance are configured separately; the **[!UICONTROL Limited Users]** profile in particular lives under a separate **[!UICONTROL delivery]** instance, not the main author instance).
2. Confirm the corresponding AEM-local group membership, not just the administrator console profile since both are required.
3. Check whether you are logging in with your organization or company Adobe account rather than a personal Adobe ID; access assigned to the organization account does not appear if you are signed in personally. [Whitelisting](https://experience.adobe.com) may also be required.
4. Inspect the effective ACL on the specific path in the repository browser or Security or Permissions UI for deny rules that override an otherwise-correct group's allow rule.
5. For DAM search or browse failures with what looks like correct **[!UICONTROL /content/dam]** access, check the read access to **[!UICONTROL /conf/global/settings/dam/adminui-extension/metadataschema]** specifically. This is a common, non-obvious blocker.
6. For folder profile or metadata-schema editing failures, confirm the local administrators group membership (folder profiles) or the full **[!UICONTROL /conf]** recursive read and write combination. Narrower grants that **[!UICONTROL look right]** are frequently incomplete.
7. Administrator console assignment alone never grants in-application capabilities, always verify the matching AEM-local group or ACL exists.


## Additional resources

+ [IMS Support for Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)
+ [AEM-provided user groups and their permissions](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/security.html)
