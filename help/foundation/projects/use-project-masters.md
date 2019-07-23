---
title: Use Project Masters
seo-title: Use Project Masters in AEM
description: Project Masters greatly simplifies user and team management with AEM Projects.
seo-description: Project Masters greatly simplifies user and team management with AEM Projects.
uuid: 40e85b7a-0790-47b0-ac82-b6e9f556b2b0
products: SG_EXPERIENCEMANAGER/6.3
topic-tags: projects
products: SG_EXPERIENCEMANAGER/6.4/SITES
discoiquuid: 62acd902-d635-4877-879f-f822d58ae91c
targetaudience: target-audience new;target-audience ongoing
index: y
internal: n
snippet: y
---

# Use Project Masters

Project Masters greatly simplifies user and team management with AEM Projects.

>[!VIDEO](https://video.tv.adobe.com/v/17740/?quality=9)

Administrators can now create a **Master Project** and assign users to roles/permissions as part of a Project Team. Projects can be created from a Master Project and will automatically inherit the Team membership. This offers several advantages:

* Re-use existing Teams across multiple projects
* Accelerates project creation as Teams do not have to be re-created by hand
* Manage Team membership from a central location and any updates to Teams are automatically inherited by Projects
* avoids creation of duplicate ACLs which can cause performance issues

Master Projects can be created under the Masters folder under AEM Projects. Once a Master Project is created it will show as an option alongside available templates in the wizard when new Projects are created.

Project Masters URL (local AEM instance): [http://localhost:4502/projects.html/content/projects/masters](http://localhost:4502/projects.html/content/projects/masters)

## Delete Project Masters

Deleting a master project results in unusable derived projects. 

Prior to deleting a master project, ensure all derived projects are finished and removed from AEM. Make sure to save any required project data before removing the derived projects. Once all derived projects are removed from AEM, the master project can safely be deleted.

## Mark Project Masters as Inactive

By changing the master project's status to inactive in the project's properties, the inactive master projects disappears from the master projects list. 

In order to show inactive master projects, toggle the "show active" filter button in the top bar (next to the list display toggle). To make the inactive project active again, simply select the inactive master project, edit project properties, and set it once again to be active.

## Understand Project Masters

![Project masters technical view](assets/use-project-masters/project-masters-architecture.png)

Project Masters work by defining a set of AEM user groups (owners, editor and observer) and allowing derived Projects to reference and reuse those centrally defined user groups.

This reduces the overall number of user groups required in AEM. Prior to Project Masters, each project created 3 user groups with the accompanying ACEs to enforce permission-ing, thus 100 projects yielded 300 user groups. Project Masters allows any number of Projects to re-use the same 3 groups, assuming the shared membership aligns to business requirements across the project.
