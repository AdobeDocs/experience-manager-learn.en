---
title: Overview of Observability via OpenTelemetry in AEM as a Cloud Service
description: Learn how AEM as a Cloud Service provides observability via OpenTelemetry for Application Performance Monitoring (APM).
version: Experience Manager as a Cloud Service
feature: Operations, Cloud Manager
topic: Development, Architecture, Performance
role: Admin, Developer
level: Beginner, Intermediate
doc-type: Article
jira: 
thumbnail: 
last-substantial-update: 2026-10-16
---

# Overview of Observability via OpenTelemetry in AEM as a Cloud Service

AEM as a Cloud Service (AEMaaCS) provides observability via [OpenTelemetry](https://opentelemetry.io/), enabling Application Performance Monitoring (APM) for your AEM hosted websites, assets and forms. OpenTelemetry provides a standard way to collect and export application telemetry data, including traces, metrics, and logs. 

In AEM as a Cloud Service, OpenTelemetry lets you send application-level telemetry from AEM _Author, Publish and Preview_ services to an observability platform of your choice that supports OpenTelemetry Protocol over HTTPS (OTLP/HTTPS).

After configuring OpenTelemetry in your AEMaaCS environment, your operations and development teams can observe AEM alongside other applications and services using the monitoring tools already used by your organization.

In this tutorial, we explain what the OpenTelemetry integration provides, how telemetry flows from AEM to your observability platform, what you can control, and what to consider before configuring the integration.

## Why OpenTelemetry

Application Performance Monitoring (APM) in AEM as a Cloud Service has traditionally relied on vendor-specific integrations. OpenTelemetry provides an open, vendor-neutral standard for collecting and exporting telemetry.

Using OpenTelemetry with AEM as a Cloud Service provides several benefits:

- **Choice of observability platform**: Send telemetry to an OpenTelemetry-compatible backend that meets your organization's monitoring requirements.
- **Application telemetry in one place**: Use traces, metrics, and optionally logs to understand application behavior.
- **Self-service configuration**: Configure the customer telemetry destination through the Cloud Manager Config Pipeline.
- **Open standard**: Use OTLP/HTTPS rather than a proprietary telemetry export format.
- **Customer-managed observability**: Manage dashboards, alerts, and telemetry retention in your observability platform.

Adobe manages the instrumentation and collection components running with AEM, while you choose where your customer telemetry is exported.

## How OpenTelemetry works in AEM as a Cloud Service

Following diagram depicts the logical flow of telemetry from AEM services to the customer observability platform:

![Logical flow of telemetry from AEM services to the customer observability platform](./assets/OTel-logical-flow.png)  



At a high level, telemetry follows this path:

**AEM Services (Author, Publish, Preview) -\> OpenTelemetry Java agent -\> OpenTelemetry Collector -\> Customer observability platform**

The OpenTelemetry integration contains two main runtime components:

**OpenTelemetry Java agent**: Instruments the AEM Java runtime and produces telemetry.
**OpenTelemetry Collector**: Receives telemetry from AEM, filters
    applicable data, and routes it to the configured destination.



### Customer telemetry path

The customer telemetry path exports application-level telemetry to the _endpoint you configure_. The destination can be a supported SaaS observability platform or another OpenTelemetry-compatible backend that accepts OTLP over HTTPS.

For a public SaaS endpoint, telemetry can use the standard outbound network path. If the **destination is private** or requires a stable allow-listed _egress IP address_, _advanced networking_ is required.

## What telemetry is available

The integration focuses on **application-level telemetry** from AEM.

### Traces

Traces provide visibility into requests processed by the AEM application.

Examples include:

- Inbound HTTP requests
- Servlet processing
- JDBC activity
- Outbound HTTP client requests
- AEM-specific spans such as Sling request, component, HTL, and JCR query activity as the corresponding instrumentation is available

Routine platform noise, such as health checks and similar internal activity, is filtered so that the exported telemetry is more useful for application analysis.

Traces are the core signal of the integration and are **always enabled** when OpenTelemetry is enabled.

### Metrics

Metrics provide time-series measurements that help you understand the health and behavior of the AEM Java application.

Examples include:

- JVM memory usage
- Garbage collection
- Thread activity
- CPU-related JVM metrics
- HTTP server request counts and duration
- JMX metrics as supported by the integration

Metrics **can be enabled** for the customer destination in the OpenTelemetry configuration.

### Logs

AEM application logs can also be exported using the OpenTelemetry logs signal.

The integration exports application logs at the supported log level and correlates them with traces using trace and span identifiers where available. This correlation can make it easier to move from an application error in a log entry to the request trace that produced it.

Logs **can be enabled** for the customer destination in the OpenTelemetry configuration.

## How AEM services are identified

Telemetry includes resource attributes that let your observability platform distinguish between AEM environments and tiers.

A service name follows this general pattern:

``` text
cm-p<program>-e<environment>-aem-<author|publish|preview>-<environment-type>
```

For example, the service name lets you distinguish Author from Publish and Preview, and separate telemetry from production, stage, and development environments.

Additional resource attributes can be used by the observability platform to filter and group telemetry by environment, AEM tier, and service instance.

## What you control

You configure the customer-facing OpenTelemetry destination through Cloud Manager and the Config Pipeline.

Your configuration determines:

- Whether customer telemetry export is enabled
- The destination type and OTLP/HTTPS endpoint
- The authentication secret reference
- Whether metrics are exported
- Whether logs are exported
- Whether Advanced Networking is used for the destination

Authentication credentials are stored as Cloud Manager secret environment variables. The configuration file references the secret, the actual credentials should not be stored as plain text in the repository.

## Supported observability destinations

The integration can send telemetry to an observability backend that accepts OTLP over HTTPS.

Examples include:

- New Relic
- Dynatrace
- Datadog
- Grafana Cloud
- Splunk Observability Cloud
- Dash0
- Other compatible OTLP/HTTPS endpoints

The observability vendor and the OpenTelemetry instrumentation are
separate concerns. OpenTelemetry provides the telemetry format and
export protocol, while your selected backend determines how the data is
queried, visualized, retained, and alerted on.

## Supported AEM environments

OpenTelemetry can be enabled for production, stage, and
development AEM environments. Rapid Development Environments (RDEs) are not supported, also sandbox programs are not supported.

