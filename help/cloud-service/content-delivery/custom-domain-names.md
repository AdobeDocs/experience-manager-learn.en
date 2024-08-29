---
title: Custom domain name options
description: Learn how to manage and implement custom domain names for your AEM as a Cloud Service hosted website.
version: Cloud Service
feature: Cloud Manager, Custom Domain Names
topic: Architecture, Migration
role: Admin, Architect, Developer
level: Intermediate
doc-type: Tutorial
duration: 130
last-substantial-update: 2024-08-09
jira: KT-15946
thumbnail: KT-15946.jpeg
exl-id: e11ff38c-e823-4631-a5b0-976c2d11353e
---
# Custom domain name options

Learn how to manage and implement domain names for your AEM as a Cloud Service hosted website.

>[!VIDEO](https://video.tv.adobe.com/v/3432632?quality=12&learn=on)

## Before you begin

Before you start implementing custom domain names, make sure you understand the following concepts:

### What is a domain name

A domain name is the human-friendly name web site name, like adobe.com, that points to a specific location (IP address like 170.2.14.16) on the Internet. 

### Default domain names in AEM as a Cloud Service

By default, AEM as a Cloud Service is provisioned with a default domain name, ending in `*.adobeaemcloud.com`. The wild card SSL certificate issued against `*.adobeaemcloud.com` is automatically applied to all the environments and this wild card certificate is Adobe's responsibility.

Default domain names are in the `https://<SERVICE-TYPE>-p<PROGRAM-ID>-e<ENVIRONMENT-ID>.adobeaemcloud.com` format. 

- The `<SERVICE-TYPE>` could be **author**, **publish** or **preview**.
- The `<PROGRAM-ID>` is the unique identifier for the program. An organization can have multiple programs.
- The `<ENVIRONMENT-ID>` is the unique identifier for the environment and each program contains four environments: **Rapid Development (RDE)**, **dev**, **stage**, and **prod**. Each environment contains the above mentioned three service types, except **RDE** that doesn't have a preview environment.

In summary, once all the AEM as a Cloud Service environments are provisioned, you have **11** (RDE doesn't have a preview environment) unique URLs combined with the default domain name.

### Adobe-managed CDN vs customer-managed CDN

To reduce the latency and improve the performance of the website, AEM as a Cloud Service is integrated with an Adobe-managed Content Delivery Network (CDN). Adobe-managed CDN is automatically enabled for all the environments. See [AEM as a Cloud Service caching](../caching/overview.md) for more details.

However, customers can also use their own CDN, referred to as **customer-managed CDN**. It is not necessary but few customers use it for corporate policies or other reasons. In this case, the customer is responsible for managing the CDN configurations and settings.

### Custom domain names

Custom domain names are always preferred over default domain name for branding, authenticity and business development purposes. However, they can only be applied to the **publish** and **preview** service types, and not **author**.

When adding custom domain names, you must provide a valid SSL certificate for the given custom domain. The SSL certificate must be a valid certificate signed by a trusted Certificate Authority (CA).

Typically, customers use a custom domain name for Prod environments (AEM as a Cloud Service web site) and sometimes for lower environments like **stage** or **dev**.

| AEM service type  | Custom domain supported? |
|---------------------|:-----------------------:|
| Author              | &#10008;                | 
| Preview             | &#10004;                | 
| Publish             | &#10004;                | 

## Implementing domain names

To implement domain names using Adobe-managed CDN or customer-managed CDN the following flowchart guides you through the process:

![Domain Name Management Flowchart](./assets/domain-name-management-flowchart.png){width="800" zoomable="yes"}

Also, the following table guides you where to manage the specific configurations:

| Custom domain name with  | Add SSL certificate to  | Add domain name to | Configure DNS records at| Need HTTP header validation CDN rule? |
|---------------------|:-----------------------:|-----------------------:|-----------------------:|-----------------------:|
| Adobe-managed CDN              |  Adobe Cloud Manager    | Adobe Cloud Manager    | DNS hosting service    | &#10008;                |
| Customer-managed CDN              |  CDN vendor    | CDN vendor    | DNS hosting service    | &#10004;                |

### Step-by-step tutorials

Now that you understand the domain name management process, you can implement custom domain names for your AEM as a Cloud Service web site by following the tutorials below:

**[Custom Domain Names with Adobe-managed CDN](./custom-domain-name-with-adobe-managed-cdn.md)**: In this tutorial, you learn how to add a custom domain name to an **AEM as a Cloud Service website with Adobe-managed CDN**.
**[Custom Domain Names with Customer-managed CDN](./custom-domain-names-with-customer-managed-cdn.md)**: In this tutorial, you learn how to add a custom domain name to an **AEM as a Cloud Service website with customer-managed CDN**.
