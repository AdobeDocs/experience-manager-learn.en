---
user-guide-title: Adobe Experience Manager as a Cloud Service Tutorials
user-guide-description: A collection of tutorials for Adobe Experience Manager as a Cloud Service.
breadcrumb-title: AEM as a Cloud Service Tutorials
sub-product: cloud-service
team: TM
---

# Adobe Experience Manager as a Cloud Service Tutorials {#cloud-service}

+ [Overview](./overview.md)
+ Introduction to AEM as a Cloud Service{#introduction}
  + [What is AEM as a Cloud Service?](./introduction/what-is-aem-as-a-cloud-service.md)
  + [Evolution](./introduction/evolution.md)
  + [Architecture](./introduction/architecture.md)
  + [Cloud Manager](./introduction/cloud-manager.md)
+ Underlying Technology {#underlying-technology}
  + [AEM Architecture](./underlying-technology/introduction-architecture.md)
  + [OSGi](./underlying-technology/introduction-osgi.md)
  + [Java Content Repository](./underlying-technology/introduction-jcr.md)
  + [Sling](./underlying-technology/introduction-sling.md)
  + [Author and Publish Services](./underlying-technology/introduction-author-publish.md)
  + [Dispatcher](./underlying-technology/introduction-dispatcher.md)
+ Cloud Manager {#cloud-manager}
  + [Programs](./cloud-manager/programs.md)
  + [Environments](./cloud-manager/environments.md)
  + [CI/CD Production Pipeline](./cloud-manager/cicd-production-pipeline.md)
  + [CI/CD Non-Production Pipeline](./cloud-manager/cicd-non-production-pipeline.md)
  + [Activity](./cloud-manager/activity.md)
  + Dev Ops{#devops}
    + [Deploying Code](./cloud-manager/devops/deploy-code.md)
    + [Merge Projects](./cloud-manager/devops/merge-projects.md)
    + [Configure Pipelines](./cloud-manager/devops/configure-pipelines.md)
    + [Continuous Integration](./cloud-manager/devops/continuous-integration.md)
    + [Analyze Test Results](./cloud-manager/devops/analyze-test-results.md)
    + [Dispatcher Configurations](./cloud-manager/devops/dispatcher-configurations.md)
    + [Cloud Manager APIs](./cloud-manager/devops/cloud-manager-apis.md)
+ Local Development Environment Setup {#local-development-environment-set-up}
  + [Overview](./local-development-environment/overview.md)
  + [Development Tools](./local-development-environment/development-tools.md)
  + [Local AEM Runtime](./local-development-environment/aem-runtime.md)
  + [Local Dispatcher Tools](./local-development-environment/dispatcher-tools.md)
+ Developing{#developing}
  + Development Basics{#basics}
    + [AEM SDK](./developing/basics/aem-sdk.md)
    + [Local Development Environment](./developing/basics/local-development-environment.md)
    + [AEM Project Archetype](./developing/basics/aem-project-archetype.md)
    + [AEM Project Structure](./developing/basics/project-structure.md)
    + [Mutable vs. Immutable Content](./developing/basics/mutable-immutable.md)
    + [Repository Structure Package](./developing/basics/repository-structure-package.md)
    + [Content Publishing](./developing/basics/content-publishing.md)
    + [OSGi Configurations](./developing/basics/osgi-configurations.md)
    + [Dispatcher Configuration Migration](./developing/basics/dispatcher-configuration.md)
  + AEM Projects{#aem-projects}
    + [AEM Maven Project](./developing/projects/maven-project-structure.md)
  + OSGi Services{#osgi-services}
    + [OSGi Service Basics](./developing/osgi-services/basics.md)
    + [OSGi Component Lifecycle](./developing/osgi-services/lifecycle.md)
    + [OSGi Configurations Basics](./developing/osgi-services/configurations.md)
    + [OSGi Configurations using OCD](./developing/osgi-services/configurations-ocd.md)
  + [AEM SDK API JavaDocs](https://javadoc.io/doc/com.adobe.aem/aem-sdk-api/latest/index.html)
+ Debugging AEM{#debugging}
  + Debugging the AEM SDK{#debugging-aem-sdk}
    + [Overview](./debugging/aem-sdk-local-quickstart/overview.md)
    + [Logs](./debugging/aem-sdk-local-quickstart/logs.md)
    + [Remote Debugging](./debugging/aem-sdk-local-quickstart/remote-debugging.md)
    + [OSGi web console](./debugging/aem-sdk-local-quickstart/osgi-web-consoles.md)
    + [Dispatcher Tools](./debugging/aem-sdk-local-quickstart/dispatcher-tools.md)
    + [Other tools](./debugging/aem-sdk-local-quickstart/other-tools.md)
  + Debugging AEM as a Cloud Service{#debugging-aem-as-a-cloud-service}
    + [Overview](./debugging/cloud-service/overview.md)
    + [Logs](./debugging/cloud-service/logs.md)
    + [Build and Deployment](./debugging/cloud-service/build-and-deployment.md)
    + [Developer Console](./debugging/cloud-service/developer-console.md)
    + [CRXDE Lite](./debugging/cloud-service/crxde-lite.md)
+ Accessing AEM{#accessing}    
  + [Overview](./accessing/overview.md)
  + [Adobe IMS users](./accessing/adobe-ims-users.md)
  + [Adobe IMS user groups](./accessing/adobe-ims-user-groups.md)
  + [Adobe IMS product profiles](./accessing/adobe-ims-product-profiles.md)
  + [AEM users, groups, and permissions](./accessing/aem-users-groups-and-permissions.md)
  + [Configuring access to AEM walk-through](./accessing/walk-through.md)
+ Migration {#migration}
  + [Content Transfer Tool](./migration/content-transfer-tool.md)
  + [Bulk Import of assets](./migration/bulk-import.md)

  + Moving to AEM as a Cloud Service {#moving-to-aem-as-a-cloud-service}
    + [Introduction](./migration/moving-to-aem-as-a-cloud-service/introduction.md)
    + [BPA and CAM](./migration/moving-to-aem-as-a-cloud-service/bpa-and-cam.md)
    + [AEM Modernization tools](./migration/moving-to-aem-as-a-cloud-service/aem-modernization-tools.md)
    + [Repository Modernization](./migration/moving-to-aem-as-a-cloud-service/repository-modernization.md)
    + [Onboarding](./migration/moving-to-aem-as-a-cloud-service/onboarding.md)
    + [Cloud Manager](./migration/moving-to-aem-as-a-cloud-service/cloud-manager.md)
    + [Dispatcher](./migration/moving-to-aem-as-a-cloud-service/dispatcher.md)
    + Content Migration {#content-migration}
      + [Bulk Import Service](./migration/moving-to-aem-as-a-cloud-service/content-migration/bulk-import-service.md)
      + [Content Transfer Tool](./migration/moving-to-aem-as-a-cloud-service/content-migration/content-transfer-tool.md)
    + [Search and Indexing](./migration/moving-to-aem-as-a-cloud-service/search-and-indexing.md)
    + [Asset Compute Microservices](./migration/moving-to-aem-as-a-cloud-service/asset-compute-microservices.md)
    + AEM Forms as a Cloud Service {#aem-forms}
      + [Introduction](./migration/moving-to-aem-as-a-cloud-service/aem-forms/introduction.md)
      + [Digital Enrollment](./migration/moving-to-aem-as-a-cloud-service/aem-forms/digital-enrollment.md)
      + [Communications](./migration/moving-to-aem-as-a-cloud-service/aem-forms/communications.md)

  + Cloud Acceleration Manager {#cloud-acceleration-manager}
    + [Introduction](./migration/cloud-acceleration-manager/introduction.md)
    + [Readiness and Best Practice Analyzer](./migration/cloud-acceleration-manager/readiness-and-best-practice-analyzer.md)
    + [Implementation phase](./migration/cloud-acceleration-manager/implementation-phase.md)
    + [Content Transfer Tool](./migration/cloud-acceleration-manager/content-transfer-tool.md)
    + [Code Refactoring tools](./migration/cloud-acceleration-manager/code-refactoring-tools.md)
    + [Code Repository Modernizer](./migration/cloud-acceleration-manager/code-repository-modernizer.md)
    + [Dispatcher Converter](./migration/cloud-acceleration-manager/dispatcher-converter.md)
    + [Index Converter](./migration/cloud-acceleration-manager/index-converter.md)
    + [Asset Workflow Migration Tool](./migration/cloud-acceleration-manager/asset-workflow-migration-tool.md)
    + [Navigating the Cloud Acceleration Manager](./migration/cloud-acceleration-manager/navigating.md)
    + [Using the Cloud Acceleration Manager](./migration/cloud-acceleration-manager/using.md)
+ Forms{#forms}
  + Create Adaptive Form{#create-first-af}
    + [Introduction](./forms/create-first-af/introduction.md)
    + [Create Theme](./forms/create-first-af/create-theme.md)
    + [Create Template](./forms/create-first-af/create-template.md)
    + [Create Fragment](./forms/create-first-af/create-fragments.md)
    + [Create Form](./forms/create-first-af/create-af.md)
    + [Configure root panel](./forms/create-first-af/configure-root-panel.md)
    + [Configure people panel](./forms/create-first-af/configure-people-panel.md)
    + [Configure income panel](./forms/create-first-af/configure-income-panel.md)
    + [Configure assets panel](./forms/create-first-af/configure-assets-panel.md)
    + [Configure start panel](./forms/create-first-af/configure-start-panel.md)
    + [Add and Configure toolbar](./forms/create-first-af/add-configure-toolbar.md)
  + Document Cloud API and AEM Forms CS{#doc-cloud-sdk}
    + [Introduction](./forms/doc-cloud-sdk/introduction.md)
    + [Create Adobe I/O project](./forms/doc-cloud-sdk/create-document-cloud-credentials.md)
    + [Create OSGi configuration](./forms/doc-cloud-sdk/create-doc-cloud-configuration.md)
    + [Define interface](./forms/doc-cloud-sdk/create-interface.md)
    + [Implement interface](./forms/doc-cloud-sdk/implement-interface.md)
    + [Create JSON part](./forms/doc-cloud-sdk/get-content-analyzer.md)
    + [Custom process step](./forms/doc-cloud-sdk/custom-process-step.md)
  + Azure Portal Storage{#forms-cs-azure-portal}
    + [Introduction](./forms/forms-cs-azure-portal/introduction.md)
    + [Create Form Data Model](./forms/forms-cs-azure-portal/create-fdm.md)
    + [Store form data in Azure Storage](./forms/forms-cs-azure-portal/create-af.md)
    + [Pre-fill form](./forms/forms-cs-azure-portal/prefill-af-storage.md)
    + [Query submissions](./forms/forms-cs-azure-portal/query-submitted-data.md)


    + Create Review Workflow{#create-aem-workflow}
        + [Create workflow model](./forms/create-aem-workflow/create-workflow.md)
        + [Trigger workflow](./forms/create-aem-workflow/configure-af.md)
    + Adobe Sign with AEM Forms{#forms-and-sign}
        + [Introduction](./forms/forms-and-sign/introduction.md)
        + [Adobe Sign API Application](./forms/forms-and-sign/create-sign-api-application.md)
        + [Adobe Sign Cloud Configuration](./forms/forms-and-sign/create-adobe-sign-cloud-configuration.md)
        + [Create Adaptive Form](./forms/forms-and-sign/create-adaptive-form.md)
        + [Configure for fill and sign](./forms/forms-and-sign/configure-form-fill-and-sign.md)

    + Integrate with Salesforce{#integrate-with-salesforce}
        + [Introduction](./forms/integrate-with-salesforce/introduction.md)
        + [Create connected app](./forms/integrate-with-salesforce/create-connected-app.md)
        + [Create swagger file](./forms/integrate-with-salesforce/describe-rest-api.md)
        + [Create data source](./forms/integrate-with-salesforce/create-data-source.md)
        + [Create form data model](./forms/integrate-with-salesforce/create-form-data-model.md)
        + [Test form submission](./forms/integrate-with-salesforce/create-lead-submitting-form.md)
        + [Test click event](./forms/integrate-with-salesforce/create-lead-click-event.md)
+ Asset Compute Extensibility{#asset-compute}
    + [Overview](./asset-compute/overview.md)
    + Set up{#set-up}
        + [Account and service provisioning](./asset-compute/set-up/accounts-and-services.md)
        + [Local development environment](./asset-compute/set-up/development-environment.md)
        + [Adobe Project Firefly](./asset-compute/set-up/firefly.md)
    + Develop{#develop}
        + [Create an Asset Compute project](./asset-compute/develop/project.md)
        + [Configure environment variables](./asset-compute/develop/environment-variables.md)
        + [Configure the manifest.yml](./asset-compute/develop/manifest.md)
        + [Develop a worker](./asset-compute/develop/worker.md)
        + [Use the Development Tool](./asset-compute/develop/development-tool.md)
    + Test and Debug{#test-debug}
        + [Test a worker](./asset-compute/test-debug/test.md)
        + [Debug a worker](./asset-compute/test-debug/debug.md)
    + Deploy{#deploy}
        + [Deploy to Adobe I/O Runtime](./asset-compute/deploy/runtime.md)
        + [Integrate with AEM](./asset-compute/deploy/processing-profiles.md)
    + Advanced{#advanced}
        + [Metadata workers](./asset-compute/advanced/metadata.md)
    + [Troubleshooting](./asset-compute/troubleshooting.md)
+ Multi-step Tutorials{#multi-step-tutorials}
    + [AEM Sites development](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
    + [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)
    + [SPA Editor (React)](https://experienceleague.adobe.com/docs/experience-manager-learn/spa-react-tutorial/overview.html)
    + [SPA Editor (Angular)](https://experienceleague.adobe.com/docs/experience-manager-learn/spa-angular-tutorial/overview.html)
    + [AEM Sites and Adobe Target](https://experienceleague.adobe.com/docs/experience-manager-learn/aem-target-tutorial/overview.html)
    + [Token-based authentication](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html)
