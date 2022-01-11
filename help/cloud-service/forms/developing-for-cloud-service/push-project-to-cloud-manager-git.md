---
title: Push AEM project to cloud manager repository
description: Push local git repository to the cloud manager repository
solution: Experience Manager
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Cloud Service
topic: Development
kt: 8851
exl-id: e61cea37-b931-49c6-9e5d-899628535480
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
