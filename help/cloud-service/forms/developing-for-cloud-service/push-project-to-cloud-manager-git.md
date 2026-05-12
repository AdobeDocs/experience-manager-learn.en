---
title: Push AEM project to cloud manager repository
description: Push local git repository to the cloud manager repository
solution: Experience Manager
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
topic: Development
jira: KT-8851
exl-id: e61cea37-b931-49c6-9e5d-899628535480
duration: 32
TQID: https://experienceleague.adobe.com/dDIreXLEjCjJl-pijSTPqCrrsWq6GDfpApHnXydI1xM
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
# Push AEM project to cloud manager git repo

In the previous step we synchronized our AEM Project with the Adaptive Forms and Themes created in the AEM instance.
We now need to add these changes to our local git repository and then push the local git repository to the cloud manager git repository.
Open command prompt and navigate to c:\cloudmanager\aem-banking-app
Execute the following commands

```

git add .

```

This adds the new files to the stage branch of the local git repository

```

git commit -m "My First AF"

```

This commits the files to the master branch of our local git repository

```

git push -f bankingapp master:"MyFirstAF"

```

In the above command we are pushing our master branch from our local git repository into the MyFirstAF branch of the cloud manager repository identified by the bankingapp friendly name.

## Next Steps

[Deploy the project to development environment](./deploy-to-dev-environment.md)
