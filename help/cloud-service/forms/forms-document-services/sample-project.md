---
title: Sample Project
description: Sample project that can be imported and executed in your environment
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Cloud Service
feature: Document Services
topic: Development
jira: KT-17479
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
exl-id: f1fcc4bb-cc31-45e8-b7bb-688ef6a236bb
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
