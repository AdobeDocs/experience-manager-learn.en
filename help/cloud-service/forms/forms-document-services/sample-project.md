---
title: Sample Project
description: Sample project that can be imported and executed in your environment
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
feature: Document Services
topic: Development
jira: KT-17479
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
exl-id: f1fcc4bb-cc31-45e8-b7bb-688ef6a236bb
TQID: https://experienceleague.adobe.com/GlDF0DaoaK319xKqeN72-ISJYtiYh64-JZootsGygSA
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Test it on your local environment

*   Import the project

    * Download and extract the [sample project](./assets/formsdocumentservices.zip)
    * Open your preferred **Java Development Environment**(IntelliJ IDEA,Eclipse or VS Code)and import the project as Maven project
*   Configure credentials

    *   Locate the file `resources/credentials/server_credentials.json`
    *   Open it and **update the credentials** specific to your environment.
    *   Ensure it includes valid values for:
 `clientId`, `clientSecret`,`adobeIMSV3TokenEndpointURL`, and 
`scopes`

*   Execute the Main class

    * Navigate to `src/main/java/Main.java` and run the main method

*   Verify execution
    * Verify the output in the terminal window
