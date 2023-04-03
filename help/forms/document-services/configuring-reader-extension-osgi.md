---
title: Configuring Reader Extensions in AEM Forms OSGi
description: Add Reader Extensions credential to the trust store in AEM Forms OSGi
feature: Reader Extensions
audience: developer
type: Tutorial
version: 6.4,6.5
topic: Administration
role: Admin
level: Beginner
exl-id: 1f16acfd-e8fd-4b0d-85c4-ed860def6d02
last-substantial-update: 2020-08-01
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
