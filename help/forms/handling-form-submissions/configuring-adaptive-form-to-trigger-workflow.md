---
title: Configuring Adaptive Form to trigger AEM Workflow overview
description: Configure payload options when triggering AEM workflow on form submission
feature: Workflow
doc-type: article
version: Experience Manager 6.4, Experience Manager 6.5
jira: KT-5407
thumbnail: 40258.jpg
topic: Development
role: Developer
level: Beginner
exl-id: 9f1dbd02-774a-4b84-90fa-02d4e468cbac
last-substantial-update: 2020-07-07T00:00:00.000Z
duration: 573
TQID: https://experienceleague.adobe.com/lcUf989Qq7hbbZR-G1sUdkaR-r15PcWFvxwIquMU-7c
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
---
# Configuring Adaptive Form to trigger AEM Workflow

## Prerequisites

The sample form used in this workflow is based on a custom adaptive form template which needs to be imported into your AEM server. The sample form that is provided needs to be imported after importing the template.

### Get the Adaptive Form Templates

* Download [Adaptive Form Template](assets/af-form-template.zip)
* [Import the template using package manager](http://localhost:4502/crx/packmgr/index.jsp)
* Upload and install the Adaptive Form template

### Get the sample Adaptive Form

* Download [Adaptive Form](assets/peak-application-form.zip) 
* Browse to [Form And Documents](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments)
* Click Create -> File Upload
* The sample adaptive form is placed in a folder called [Application Forms](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments/applicationforms)

The following video explains how to configure an Adaptive Form to trigger an AEM Workflow
>[!VIDEO](https://video.tv.adobe.com/v/40258?quality=12&learn=on)

The following video shows you the workflow payload and other details in the crx repository

>[!VIDEO](https://video.tv.adobe.com/v/40259?quality=12&learn=on)
