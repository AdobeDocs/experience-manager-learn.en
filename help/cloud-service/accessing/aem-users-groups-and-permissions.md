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

Access to AEM Assets is controlled by two independent layers that must both be configured correctly:

1. Adobe Admin Console product profiles — grant the technical entitlement to reach an AEM environment at all (e.g., Power User, Collaborator, Limited User, Administrators).
2. AEM-local group membership and ACLs — control what a user can actually do once inside that environment (upload, edit, delete, approve, configure).

Assigning a product profile in Admin Console is necessary but not sufficient: a user can be a fully licensed Power User in Admin Console and still be blocked from every asset operation if they are not also placed in the correct AEM-local group. Conversely, correct AEM-local group membership has no effect if the user was never granted an Admin Console product profile for the environment.

### Permissions required for common operations {#permissions-required-for-common-operations}

| Operation | Required permission or group | Notes |
| -------- | -------- | -------- |
| Upload an asset to /content/dam  | rep:write on the target /content/dam path | Group membership alone does not guarantee this is inherited at the user level — if uploads fail for specific users while others in the same group succeed, verify rep:write is actually present on the user's effective ACL, not just assumed from group membership. |
| Search / view assets in the DAM UI | Read access to /content/dam (typically via dam-users) and jcr:read on /conf/global/settings/dam/adminui-extension/metadataschema | The Assets UI resolves metadata schema definitions from /conf to render results. If a group has full /content/dam access but no read access to the schema config path, the UI throws a NullPointerException and search/browse silently fails — this is not a /content/dam permission problem even though it looks like one. |
| Create or edit a Folder Profile | Membership in the local administrators group | An Admin Console "Administrator" assignment is not the same thing — the "Create" button for Folder Profiles is only rendered for accounts that are also members of AEM's local administrators group. |
| Create/edit a custom metadata schema | Recursive jcr:read on /conf and on /conf/global/settings/dam/adminui-extension/metadataschema, plus jcr:write on /conf/global/settings/dam/adminui-extension and its metadataschema subnode | Write access to the metadataschema node alone is not enough; the schema editor also needs to read the parent /conf tree to render correctly. |
| Edit asset metadata fields (e.g., Review Status on Content Hub-ingested assets) | dam-users group membership | Applies even to assets ingested through Content Hub — the underlying edit permission is still AEM's standard DAM group model. |
| Use "Share Link" action | jcr:modifyAccessControl on the folder, and the group must not be excluded from "Allow only for groups" | Configured under Tools > Assets > Assets Configurations > Link Share. This has been observed to differ between environments (e.g. present in Dev, missing in Prod) even with identical code, so check both the ACL and this configuration screen per environment. |
| License and save an Adobe Stock asset | Membership in both the Stock licensing group and the base DAM authoring group (e.g. dam-users) | Membership in the Stock group alone is not sufficient for the "License & Save" workflow to complete. |
| View Bandwidth & Storage in Dynamic Media Classic | System Administrator privileges | Insufficient privileges surface as Scene7 error #2046 rather than a standard permission-denied message. |
| API access via a JWT bearer token / technical account | The technical account's underlying AEM user must be explicitly added to the required AEM group (e.g. a "view-only" group) | Provisioning a Product Profile/Service in Admin Console creates the technical account user, but does not automatically grant it every AEM group needed for complete API responses (e.g. full rendition lists) — the account's AEM group membership still needs separate configuration. |

### Group inheritance and permission evaluation {#group-inheritance-and-permission-evaluation}

* Permissions applied to a parent folder cascade to child folders and assets by default.
* Explicit deny rules take precedence over allow rules. A user can be a member of a group that is allowed access, but if that same user (directly or via another group) is also subject to a jcr:read (or other) deny rule on that path or an ancestor path, the deny wins — even when two users appear to have "identical" group memberships in the Admin Console.
* When two users with seemingly identical permissions behave differently, compare their effective ACLs (Tools > Security > Permissions, or the Repository Browser), not just their group membership lists — look specifically for deny rules scoped to one of the groups.

### Distinguishing group types {#distinguishing-group-types}

AEM does not visually separate group types in Tools > Security > Groups, which makes large permission audits difficult. Use these rules to classify a group:

* Out-of-the-box (OOTB) groups have fixed, well-known group IDs (e.g. administrators, dam-users, content-authors).
* IMS-synced groups (created automatically from Admin Console user groups) carry a rep:externalId property ending in ;ims.
* Custom groups created directly in AEM have no rep:externalId property.

Adobe's guidance is to treat OOTB and custom local groups as the primary building blocks for permissions, and treat IMS-synced groups purely as entry points that map Admin Console assignments into AEM — not as a place to layer additional ad hoc ACLs.

### Content Hub and Brand Portal specific behavior {#content-hub-brand-portal-specific-behavior}

* Content Hub access is not controlled by dedicated "Content Hub" groups. It is controlled by environment-specific Admin Console product profiles, typically named AEM Assets Limited Users - delivery - Program <programId> - Environment <environmentId>.
* ContentHub access is granted only through the Limited User product profile — the Power User profile does not grant ContentHub access on its own, even though this was not always clear from documentation. Assigning both Power User and Limited User to the same account does not double-consume licenses.
* Content Hub admin rights require membership in specific product profiles (AEM Assets Limited Users – delivery and AEM Administrators – production author) — visibility of the Admin tab in the UI is not itself proof of admin rights.
* Attribute-Based Access Control (ABAC) rules, when enabled, are configured self-service through the AI Assistant / Governance Agent inside Content Hub (there is no separate dedicated ABAC permissions screen). If specific groups can't see any assets in Content Hub despite correct-looking group/profile assignments, check whether ABAC policies are enabled and whether user attributes or asset metadata satisfy those policies before assuming a group misconfiguration.
* Changes made to users/groups in Admin Console are not reflected in Brand Portal in real time — a background sync job runs roughly every 8 hours, so allow 5–10 hours before troubleshooting a "changes not appearing" report as a bug.
* A collection marked "public" in Brand Portal is still inaccessible to guest users if the underlying DAM folder is not also public and the assets are not published from AEM Assets — collection-level visibility does not override folder-level visibility.
* A Closed User Group (CUG) applied to a DAM path can block publisher-side visibility per environment even after a successful replication; a missing cq:lastReplicated property is a useful diagnostic signal that the asset was never actually published (as distinct from being blocked by CUG after publishing).

### Troubleshooting permission-denied errors {#troubleshooting-permission-denied-errors}

1. Confirm the Admin Console product profile assignment for the correct environment (author vs. delivery/Content Hub instance are configured separately — the "Limited Users" profile in particular lives under a separate "delivery" instance, not the main author instance).
2. Confirm the corresponding AEM-local group membership, not just the Admin Console profile — both are required.
3. Check whether the user is logging in with their organization/company Adobe account rather than a personal Adobe ID; access assigned to the organization account will not appear if the user is signed in personally. Whitelisting experience.adobe.com may also be required.
4. Inspect the effective ACL on the specific path in the Repository Browser or Security/Permissions UI for deny rules that override an otherwise-correct group's allow rule.
5. For DAM search/browse failures with what looks like correct /content/dam access, check read access to /conf/global/settings/dam/adminui-extension/metadataschema specifically — this is a common, non-obvious blocker.
6. For Folder Profile or metadata-schema editing failures, confirm local administrators group membership (Folder Profiles) or the full /conf recursive-read + write combination described above (schema editing) — narrower grants that "look right" are frequently incomplete.
7. Remember that Admin Console assignment alone never grants in-application capabilities — always verify the matching AEM-local group or ACL exists.


## Additional resources

+ [IMS Support for Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)
+ [AEM-provided user groups and their permissions](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/security.html)
