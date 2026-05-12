---
title: Configuring Reader Extensions in AEM Forms OSGi
description: Add Reader Extensions credential to the trust store in AEM Forms OSGi
feature: Reader Extensions
type: Tutorial
version: Experience Manager 6.4, Experience Manager 6.5
topic: Administration
role: Admin
level: Beginner
exl-id: 1f16acfd-e8fd-4b0d-85c4-ed860def6d02
last-substantial-update: 2020-08-01T00:00:00.000Z
duration: 308
TQID: https://experienceleague.adobe.com/Eig9DwXjKcNzww4eV6LDI28ddxFExo9dfbJpPHnRiRE
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: d49d6117-dd89-469c-a774-cc96b7eee433
    internal-label: Administration
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
# Add Reader Extensions credential{#configuring-reader-extension-osgi}

The DocAssurance service can apply usage rights to PDF documents. To apply usage rights to PDF documents, configure the certificates.

## Create keystore for fd-service user

The reader extensions credential is associated with fd-service user. To add the credential to the fd-service user please follow the following steps. If you have already created the keystore for the fd-service user skip this section

* Login to your AEM Author instance as an Administrator
* Go to Tools-Security-Users
* Scroll down the list of users till you find fd-service user account
* Click on the fd-service user
* Click on the keystore tab
* Click on Create KeyStore
* Set the KeyStore Access Password and save your settings to create the KeyStore password

### Add credential to the fd-service user keystore

Please follow the video to add the credentials to the fd-service user

>[!VIDEO](https://video.tv.adobe.com/v/335849?quality=12&learn=on)


The command to list the details of the pfx file is. The following command assumes you are in the same directory as the pfx file .

**keytool -v -list -storetype pkcs12 -keystore <name of your .pfx file>**

For example  keytool -v -list -storetype pkcs12 -keystore 1005566.pfx where 1005566.pfx is the name of my pfx file
