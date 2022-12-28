---
title: Email service
description: Learn how to configure AEM as a Cloud Service to connect with an email service using egress ports.
version: Cloud Service
feature: Security
topic: Development, Security
role: Architect, Developer
level: Intermediate
kt: 9353
thumbnail: KT-9353.jpeg
exl-id: 5f919d7d-e51a-41e5-90eb-b1f6a9bf77ba
---
# Email service

Send emails from AEM as a Cloud Service by configuring AEM's `DefaultMailService` to use advanced networking egress ports.

Because (most) mail services do not run over HTTP/HTTPS, connections to mail services from AEM as a Cloud Service must be proxied out.

+ `smtp.host` is set to the OSGi environment variable `$[env:AEM_PROXY_HOST;default=proxy.tunnel]` so it is routed through the egress.
  + `$[env:AEM_PROXY_HOST]` is a reserved variable that AEM as a Cloud Service maps to the internal `proxy.tunnel` host.
  + Do NOT attempt to set the `AEM_PROXY_HOST` via Cloud Manager.
+ `smtp.port` is set to the `portForward.portOrig` port that maps to the destination email service's host and port. This example uses the mapping: `AEM_PROXY_HOST:30002` &rarr; `smtp.sendgrid.com:465`.
  + The `smpt.port` is set to the `portForward.portOrig` port, and NOT the SMTP server's actual port. The mapping between the `smtp.port` and the `portForward.portOrig` port is established by the Cloud Manager `portForwards` rule (as demonstrated below). 

Since secrets must not be stored in code, the email service's username and password are best provided using [secret OSGi configuration variables](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#secret-configuration-values), set using AIO CLI, or the Cloud Manager API.

Typically, [flexible port egress](../flexible-port-egress.md) is used to satisfy integrating with an email service unless it is necessary to `allowlist` the Adobe IP, in which case [dedicated egress ip address](../dedicated-egress-ip-address.md) can be used.

## Advanced networking support

The following code example is supported by the following advanced networking options.

Ensure the the [appropriate](../advanced-networking.md#advanced-networking) advanced networking configuration has been set up prior to following this tutorial.

| No advanced networking | [Flexible port egress](../flexible-port-egress.md) | [Dedicated egress IP address](../dedicated-egress-ip-address.md) | [Virtual Private Network](../vpn.md) |
|:-----:|:-----:|:------:|:---------:|
| &#10008; | &#10004; | &#10004; | &#10004; |

## OSGi configuration

This OSGi configuration example configures AEM's Mail OSGi Service to use an external mail service, by way of the following Cloud Manager `portForwards` rule of the [enableEnvironmentAdvancedNetworkingConfiguration](https://www.adobe.io/experience-cloud/cloud-manager/reference/api/#operation/enableEnvironmentAdvancedNetworkingConfiguration) operation.

```json
...
"portForwards": [{
    "name": "smtp.mymail.com",
    "portDest": 465,
    "portOrig": 30002
}]
...
```

+ `ui.config/src/jcr_root/apps/wknd-examples/osgiconfig/config/com.day.cq.mailer.DefaultMailService.cfg.json`

Configure AEM's [DefaulMailService](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html#sending-email) as required by your email provider (e.g. `smtp.ssl`, etc.).

```json
{
    "smtp.host": "$[env:AEM_PROXY_HOST;default=proxy.tunnel]",
    "smtp.port": "30002",
    "smtp.user": "$[env:EMAIL_USERNAME;default=myApiKey]",
    "smtp.password": "$[secret:EMAIL_PASSWORD]",
    "from.address": "noreply@wknd.site",
    "smtp.ssl": true,
    "smtp.starttls": false, 
    "smtp.requiretls": false,
    "debug.email": false,
    "oauth.flow": false
}
```

The `EMAIL_USERNAME` and `EMAIL_PASSWORD` OSGi variable and secret can be set per environment, using either:

+ [Cloud Manager Environment Configuration](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/environment-variables.html)
+ or using the `aio CLI` command

  ```shell
  $ aio cloudmanager:set-environment-variables --programId=<PROGRAM_ID> <ENVIRONMENT_ID> --secret EMAIL_USERNAME "myApiKey" --secret EMAIL_PASSWORD "password123"
  ```
