---
title: Understanding Multitenancy and Concurrent Development
description: Learn about the benefits, challenges, and techniques to manage a multi-tenant implementation with Adobe Experience Manager Assets.
feature: Connected Assets
version: 6.5
topic: Development
role: Developer
level: Intermediate
exl-id: c9ee29d4-a8a5-4e61-bc99-498674887da5
---
# Understanding Multitenancy and Concurrent Development {#understanding-multitenancy-and-concurrent-development}

## Introduction {#introduction}

When multiple teams are deploying their code to the same AEM environments, there are practices they should follow to ensure that teams can work as independently as possible, without stepping on other teams’ toes. Although they can never be fully eliminated, these techniques will minimize cross-team dependencies. For a concurrent development model to be successful, good communication between the development teams is critical.

Additionally, when multiple development teams work on the same AEM environment, there is likely some degree of multi-tenancy at play. Much has been written on the practical considerations of attempting to support multiple tenants in an AEM environment, especially around the challenges faced when managing governance, operations, and development. This paper explores some of the technical challenges around implementing AEM in a multi-tenant environment, but many of these recommendations will apply to any organization with multiple development teams.

It is important to note up front that while AEM can support multiple sites and even multiple brands being deployed on a single environment, it does not offer true multi-tenancy. Some environment configurations and systems resources will always be shared across all sites that are deployed on an environment. This paper provides guidance for minimizing the impacts of these shared resources and offers suggestions to streamline communication and collaboration in these areas.

## Benefits and Challenges {#benefits-and-challenges}

There are many challenges to implementing a multi-tenant environment.

These include:

* Additional technical complexity
* Increased development overhead
* Cross-organization dependencies on shared resource
* Increased operational complexity

Despite the challenges faced, running a multi-tenant application does have benefits, such as:

* Reduced hardware costs
* Reduced time to market for future sites
* Lower implementation costs for future tenants
* Standard architecture and development practices across the business
* A common codebase

If the business requires true multi-tenancy, with zero knowledge of other tenants and no shared code, content, or common authors, then separate author instances are the only viable option. Overall increase in development effort should be compared against the savings in infrastructure and license costs to determine if this approach is the best fit.

## Development Techniques {#development-techniques}

### Managing Dependencies {#managing-dependencies}

When managing Maven project dependencies, it is important that all teams use the same version of a given OSGi bundle on the server. To illustrate what can go wrong when Maven projects are mismanaged, we present an example:

Project A depends on version 1.0 of the library, foo; foo version 1.0 is embedded in their deployment to the server. Project B depends on version 1.1 of the library, foo; foo version 1.1 is embedded in their deployment.

Furthermore, let’s assume that an API has changed in this library between versions 1.0 and 1.1. At this point, one of these two projects will no longer work properly.

To address this concern, we recommend making all Maven projects children of one parent reactor project. This reactor project serves two purposes: it allows for the building and deployment of all projects together if so desired, and it contains the dependency declarations for all the child projects. The parent project defines the dependencies and their versions while the child projects only declare the dependencies that they require, inheriting the version from the parent project.

In this scenario, if the team working on Project B requires functionality in version 1.1 of foo, it will quickly become apparent in the development environment that this change will break Project A. At this point the teams can discuss this change and either make Project A compatible with the new version or look for an alternative solution for Project B.

Note that this does not eliminate the need for these teams to share this dependency-it just highlights issues quickly and early so that teams can discuss any risks and agree on a solution.

### Preventing Code Duplication {#preventing-code-duplication-nbsp-br}

When working on multiple projects, it is important to ensure that code is not duplicated. Code duplication increases the likelihood of defect occurrences, the cost of changes to the system, and overall rigidity in the code base. To prevent duplication, refactor common logic into reusable libraries that can be used across multiple projects.

To support this need, we recommend the development and maintenance of a core project that all teams can depend on and contribute to. When doing so, it is important to ensure that this core project does not, in turn, depend on any of the individual teams’ projects; this allows for independent deployability while still promoting code reuse.

Some examples of code that commonly in a core module include:

* System-wide configurations such as:
  * OSGi configurations
  * Servlet filters
  * ResourceResolver mappings
  * Sling Transformer pipelines
  * Error Handlers (or use the ACS AEM Commons Error Page Handler1)
  * Authorization servlets for permission-sensitive caching
* Utility classes
* Core business logic
* Third-party integration logic
* Authoring UI overlays
* Other customizations required for authoring, such as custom widgets 
* Workflow launchers
* Common design elements that are used across sites

*Modular Project Architecture*

This does not eliminate the need for multiple teams to depend on and potentially update the same set of code. By creating a core project, we have decreased the size of the codebase that is shared between teams-decreasing but not eliminating the need for shared resources.

To ensure that the changes made to this core package do not disrupt the functionality of the system, we recommend that a senior developer or team of developers maintain oversight. One option is to have a single team that manages all the changes to this package; another is to have teams submit pull requests that are reviewed and merged by these resources. It is important that a governance model is designed and agreed to by the teams and that developers follow it.

## Managing Deployment Scope&nbsp {#managing-deployment-scope}

As different teams deploy their code to the same repository, it is important that they do not overwrite each other’s changes. AEM has a mechanism to control this when deploying content packages, the filter. xml file. It is important that there is no overlap between filter.  xml files, otherwise one team’s deployment could potentially erase another team’s previous deployment. To illustrate this point, see the following examples of well-crafted vs. problematic filter files:

/apps/my-company vs. /apps/my-company/my-site

/etc/clientlibs/my-company vs. /etc/clientlibs/my-company/my-site

/etc/designs/my-company vs. /etc/designs/my-company/my-site

If each team explicitly configures their filter file down to the site(s) that they are working on, each team can deploy their components, client libraries, and site designs independently without erasing each other’s changes.

Because it is a global system path and not specific to one site, the following servlet should be included in the core project, as changes made here could potentially impact any team:

/apps/sling/servlet/errorhandler

### Overlays {#overlays}

Overlays are frequently used to extend or replace out of the box AEM functionality, but using an overlay affects the entire AEM application (that is, any functionality changes will be available for all tenants). This would be further complicated if tenants had different requirements for the overlay. Ideally, business groups should work together to agree on the functionality and appearance of AEM’s administrative consoles.

If consensus cannot be reached amongst the various business units, a possible solution would be to simply not use overlays. Instead, create a custom copy of the functionality and expose it via a different path for each tenant. This allows each tenant to have a completely different user experience, but this approach increases the cost of implementation and subsequent upgrade efforts as well.

### Workflow Launchers {#workflow-launchers}

AEM uses workflow launchers to automatically trigger workflow execution when specified changes are made in the repository. AEM provides several launchers out of the box, for example, to execute rendition generation and metadata extraction processes on new and updated assets. While it is possible to leave these launchers as-is, in a multitenant environment, if tenants have different launcher and/or workflow model requirements, then it is likely that individual launchers will need to be created and maintained for each tenant. These launchers will need to be configured to execute on their tenant’s updates while leaving content from other tenants untouched. Easily accomplish this is by applying launchers to specified repository paths that are tenant-specific.

### Vanity URLs {#vanity-urls}

AEM provides vanity URL functionality that can be set on a per-page basis. The concern with this approach in a multi-tenant scenario is that AEM does not ensure uniqueness between the vanity URLs configured in this manner. If two different users configure the same vanity path for different pages, unexpected behavior can be encountered. For this reason, we recommend using mod_rewrite rules in the Apache dispatcher instances, which allow for a central point of configuration in concert with outbound-only Resource Resolver rules.

### Component Groups {#component-groups}

When developing components and templates for multiple authoring groups, it is important to make effective use of componentGroup and allowedPaths properties. By leveraging these effectively with site designs, we can ensure that authors from Brand A only see components and templates that have been created for their site while authors from Brand B only see theirs.

### Testing {#testing}

While a good architecture and open communication channels can help prevent the introduction of defects into unexpected areas of the site, these approaches are not foolproof. For this reason, it is important to fully test what is being deployed on the platform before releasing anything into production. This requires coordination between teams on their release cycles and reinforces the need for a suite of automated tests that cover as much functionality as possible. Additionally, because one system will be shared by multiple teams, performance, security, and load testing become more important than ever.

## Operational Considerations {#operational-considerations}

### Shared Resources {#shared-resources}

AEM runs within a single JVM; any deployed AEM applications inherently share resources with each other, on top of resources already consumed in the normal running of AEM. Within the JVM space itself, there will be no logical separation of threads, and the finite resources available to AEM, such as memory, CPU, and disk i/o will also be shared. Any tenant consuming resources will inevitably affect other system tenants.

### Performance {#performance}

If not following AEM best practices, it is possible to develop applications that consume resources beyond what is considered normal. Examples of this are triggering many heavy workflow operations (such as DAM Update Asset), using MSM push-on-modify operations over many nodes, or using expensive JCR queries to render content in real-time. These will inevitably have an impact on the  performance of other tenant applications.

### Logging {#logging}

AEM provides out of the box interfaces for robust logger configuration that can be used to our advantage in shared development scenarios. By specifying separate loggers for each brand, by package name, we can achieve some degree of log separation. While system-wide operations like replication and authentication will still be logged to a central location, non-shared custom code can be logged separately, easing monitoring and debugging efforts for each brand’s technical team.

### Backup and Restore {#backup-and-restore}

Due to the nature of the JCR repository, traditional backups work across the entire repository, rather than on an individual content path. It is therefore not possible to easily separate backups on a per-tenant basis. Conversely, restoring from a backup will rollback content and repository nodes for all tenants on the system. While it is possible to perform targeted content backups, using tools such as VLT, or to cherry pick content to restore by building a package in a separate environment, these  
approaches do not easily encompass configuration settings or application logic and can be cumbersome to manage.

## Security Considerations {#security-considerations}

### ACLs {#acls}

It is, of course, possible to use Access Control Lists (ACLs) to control who has access to view, create, and delete content based on content paths, which requires the creation and management of user groups. The difficulty in maintaining the ACLs and groups depends on the emphasis on ensuring each tenant has zero knowledge of others and whether the deployed applications rely on shared resources. To ensure efficient ACL, user, and group administration, we recommend having a centralized group with the necessary oversight to ensure that these access controls and principals overlap (or do not overlap) in a way that promotes efficiency and security.
