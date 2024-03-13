---
title: Add Custom Domain Name
description: Learn how to add a custom domain name to AEM as a cloud service-hosted site.
version: Cloud Service
feature: Cloud Manager, Operations
topic: Administration, Architecture
role: Admin, Developer
level: Intermediate
doc-type: Tutorial
duration: 
last-substantial-update: 2024-03-12
jira: KT-15121
thumbnail: KT-15121.jpeg
---

# Add custom domain name

Learn how to add a custom domain name to AEM as a Cloud Service web site. 

In this tutorial, the branding of the sample [AEM WKND](https://github.com/adobe/aem-guides-wknd) site is enhanced by adding an HTTPS-addressable custom domain name `wknd.enablementadobe.com` with Transport Layer Security (TLS).

>[!VIDEO](https://video.tv.adobe.com/v/3427817?quality=12&learn=on)

The high-level steps are:

![High Custom Domain Name](./assets/add-custom-domain-name-steps.png){width="800" zoomable="yes"}

## Prerequisites

- [OpenSSL](https://www.openssl.org/) and [dig](https://www.isc.org/blogs/dns-checker/) are installed on your local machine.
- Access to third-party services:
    - Certificate Authority (CA) -  to request the signed certificate for your site domain, like [DigitCert](https://www.digicert.com/) 
    - Domain Name System (DNS) hosting service - to add DNS records for your custom domain, like Azure DNS, or AWS Route 53. 
- Access to [Adobe Cloud Manager](https://my.cloudmanager.adobe.com/) as Business Owner or Deployment Manager role.
- Sample [AEM WKND](https://github.com/adobe/aem-guides-wknd) site is deployed to AEMCS environment of [production program](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/programs/introduction-production-programs.html) type.

If you do not have access to third-party services, _collaborate with your security or hosting team to complete the steps_.

## Generate SSL certificate

You have two options:

- Using `openssl` command-line tool - you can generate a private key and a Certificate Signing Request (CSR) for your site domain. To request a signed certificate submit the CSR to a Certificate Authority (CA).

- Your hosting team provides the required private key and signed certificate for your site.

Let's review the steps for the first option. 

To generate a private key and a CSR, run the following commands and provide the required information when prompted:

```bash
# Generate a private key and a CSR
$ openssl req -newkey rsa:2048 -keyout <YOUR-SITE-NAME>.key -out <YOUR-SITE-NAME>.csr -nodes
```

To request a signed certificate, provide the generated CSR to the CA by following their documentation. Once the CA signs the CSR, you receive the signed certificate file.

### Review signed certificate

Reviewing the signed certificate before adding it to the Cloud Manager is a good practice. You can review the certificate details using the following command:

```bash
# Review the certificate details
$ openssl crl2pkcs7 -nocrl -certfile <YOUR-SIGNED-CERT>.crt | openssl pkcs7 -print_certs -noout
```

The signed certificate may contain the certificate chain, which includes the root and intermediate certificates along with the end-entity certificate. 

The Adobe Cloud Manager accepts the end-entity certificate and the certificate chain _in separate form fields_, so you must extract the end-entity certificate and the certificate chain from the signed certificate.

In this tutorial, the [DigitCert](https://www.digicert.com/) signed certificate issued against `*.enablementadobe.com` domain is used as an example. The end-entity and certificate chain is extracted by opening the signed certificate in a text editor and copying the content between the `-----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` markers.

## Add SSL certificate in Cloud Manager

To add the SSL certificate in Cloud Manager, follow the [Add SSL Certificate](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html) documentation.

## Domain name verification

To verify the domain name follow these steps:

- Add domain name in Cloud Manager by following the [Add Custom Domain Name](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name.html) documentation.
- Add an AEM-specific [TXT record](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-text-record.html) in your DNS hosting service.
- Verify the above steps by querying the DNS servers using the `dig` command.

```bash
# General syntax, the `_aemverification` is prefix provided by Adobe
$ dig _aemverification.[YOUR-DOMAIN-NAME] -t txt

# This tutorial specific example, as the subdomain `wknd.enablementadobe.com` is used
$ dig _aemverification.wknd.enablementadobe.com -t txt
```

The sample successful response looks like this:

```bash
; <<>> DiG 9.10.6 <<>> _aemverification.wknd.enablementadobe.com -t txt
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 8636
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1220
;; QUESTION SECTION:
;_aemverification.wknd.enablementadobe.com. IN TXT

;; ANSWER SECTION:
_aemverification.wknd.enablementadobe.com. 3600    IN TXT "adobe-aem-verification=wknd.enablementadobe.com/105881/991000/bef0e843-9280-4385-9984-357ed9a4217b"

;; Query time: 81 msec
;; SERVER: 153.32.14.247#53(153.32.14.247)
;; WHEN: Tue Mar 12 15:54:25 EDT 2024
;; MSG SIZE  rcvd: 181
```

In this tutorial, Azure DNS is used as an example. To add the TXT record, you must follow the documentation of your DNS hosting service.

Review the [Checking Domain Name Status](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html) documentation if there is an issue.

## Configure DNS record

To configure the DNS record for your custom domain follow these steps,

- Determine the DNS record type (CNAME or APEX) based on the domain type, like root domain (APEX) or subdomain (CNAME), and follow the [Configuring DNS Settings](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/configure-dns-settings.html) documentation.
- Add the DNS record in your DNS hosting service.
- Trigger the DNS record validation by following the [Checking DNS Record Status](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html) documentation.

In this tutorial, as a **subdomain** `wknd.enablementadobe.com` is used, the CNAME record type that points to `cdn.adobeaemcloud.com` is added. 

However, if you are using the **root domain**, you must add APEX record type (aka A, ALIAS, or ANAME) that points to the specific IP addresses provided by Adobe.

## Site verification

To verify the site is accessible using the custom domain name, open a web browser and navigate to the custom domain URL. Make sure that the site is accessible and the browser shows a secure connection with the padlock icon.


