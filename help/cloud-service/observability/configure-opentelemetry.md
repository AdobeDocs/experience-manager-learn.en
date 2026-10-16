---
title: Configure OpenTelemetry for AEM as a Cloud Service
description: Learn how to configure an OpenTelemetry destination for AEM as a Cloud Service using Cloud Manager secrets and a Config Pipeline.
version: Experience Manager as a Cloud Service
feature: Operations, Cloud Manager
topic: Development, Performance
role: Admin, Developer
level: Intermediate
doc-type: Tutorial
last-substantial-update: 2026-10-16
---

# Configure OpenTelemetry for AEM as a Cloud Service

Learn how to connect an AEM as a Cloud Service environment to an OpenTelemetry compatible observability platform of your choice. This tutorial uses the [AEM WKND sample project](https://github.com/adobe/aem-guides-wknd) as an example application and shows how to configure telemetry export using Cloud Manager Config Pipeline.

In this tutorial, you learn:

1. Identify the OTLP/HTTPS endpoint and ingestion credential for your observability platform.
2. Save the credential securely in Cloud Manager.
3. Add `config/otel.yaml` to your AEM project repository.
4. Create and run the Config pipeline
5. Generate WKND traffic and verify telemetry in your observability platform.

<!-- TODO: Add a short video or screenshots after validating the workflow on a WKND-enabled AEM environment. -->

## Prerequisites

Before starting, ensure that you have:

- An **eligible AEM as a Cloud Service** development, stage, or production environment with the WKND or your application deployed. OpenTelemetry is not supported on Sandbox programs or Rapid Development Environments (RDEs).
- Access to a **Cloud Manager** to manage environment variables, create and run the Config Pipeline.
- An observability platform that accepts **OTLP over HTTPS**, with an endpoint and an ingestion credential.
- Access to the observability platform to verify incoming AEM telemetry and visualize it.

## Step 1: Obtain your observability endpoint and credential

In your observability platform, locate its **OTLP/HTTPS ingestion endpoint** and create or retrieve the appropriate ingestion credential. Please consult your platform's documentation for specific instructions on obtaining these details.

For demo purpose, a self-hosted observability platform that supports OTLP over HTTPS is used.

## Step 2: Store the credential in Cloud Manager

Store the credential as a Cloud Manager **secret environment variable** instead of committing it to Git.

1. Select your AEM program in [Cloud Manager](https://my.cloudmanager.adobe.com/).
   ![Select AEM Program in Cloud Manager](./assets/cloud-manager-env-vars.png)

1. Select the target environment and click **View Details**.
   ![View Environment Details](./assets/cloud-manager-view-details.png)
   
1. From the **Configuration** tab click **Add/Update** button to add a new environment variable. Then add an environment variable with these values:

   | Setting | Value |
   | --- | --- |
   | Name | `OTEL_CUSTOMER_AUTH` |
   | Value | Your provider's ingestion credential, note they vary by platform, see [provider-specific settings](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/opentelemetry-apm-integration?utm_source=chatgpt.com#configure-credential) and examples. |
   | Service applied | **All** |
   | Type | **Secret** |

   ![Add Environment Variable](./assets/cloud-manager-add-update.png)

   In my case, as its self-hosted observability platform, the credential is a basic authentication token in `"Basic <base64(user:pass)>"` format.

1. Click **Add** and then **Save** to store the environment variable.
   ![Save Environment Variable](./assets/cloud-manager-save-env-var.png)

The configuration `config/otel.yaml` file references the above secret as `${{secrets.OTEL_CUSTOMER_AUTH}}`. The actual credential must never appear in the repository, screenshots, or pipeline logs.

## Step 3: Add the OpenTelemetry configuration

In the **AEM project repository**, create a file at the `config/otel.yaml` path, my self-hosted observability platform uses the following configuration:

```yaml
kind: "Otel"
version: "v1"
metadata:
  envTypes:
    - "dev"
    - "stage"
    - "prod"
data:
  enabled: true
  type: "generic"
  endpoint: "https://my-self-hosted-observability.adobe.net"
  authHeaderName: "Authorization"
  authHeaderValue: "${{secrets.OTEL_CUSTOMER_AUTH}}"
  metrics: true
  logs: true
```

The key settings are:

| Setting | Purpose |
| --- | --- |
| `metadata.envTypes` | Environment types to which the configuration applies. Include the target environment type. |
| `enabled` | Enables customer telemetry export when set to `true`. |
| `type` | Selects the destination configuration, such as `newrelic`, `dynatrace`, or `generic`. |
| `endpoint` | Base OTLP/HTTPS URL for the destination. |
| `authHeaderValue` | Reference to the Cloud Manager secret, not the credential itself. |
| `metrics` | Enables metrics export when `true`. |
| `logs` | Enables application log export when `true`. |

Traces are enabled when the integration is enabled; metrics and logs are optional. 

![WKND sample configuration](./assets/wknd-sample-configuration.png)

## Step 4: Commit and run the Config Pipeline

1. Commit `config/otel.yaml` and push changes to the upstream repository from which your Config Pipeline is sourcing its configuration.
2. In Cloud Manager, create or edit the relevant **Config Pipeline**, verify the details.
    ![Config Pipeline details](./assets/config-pipeline-details.png)
3. To run the pipeline, select the name of the pipeline and click **Run**.
    ![Run Config Pipeline](./assets/run-config-pipeline.png)
4. Monitor the pipeline execution to ensure that the configuration is applied successfully.
   ![Monitor Config Pipeline](./assets/monitor-config-pipeline.png)

The configuration process checks the file format, environment eligibility, endpoint settings, secret reference, and credentials before applying the destination configuration.

## Step 5: Generate traffic in WKND

Once the configuration has been applied, generate a small amount of application activity:

1. Open the WKND site on the AEM Publish service.
2. Navigate between a few WKND pages, such as the home page and article pages.
3. Refresh a page several times to generate additional inbound HTTP requests.
4. Optionally open the WKND site in Author to compare telemetry between tiers.

This creates application requests that should produce trace data. It does not guarantee that every request is retained or visible because sampling and filtering may apply.

<!-- TODO: Screenshot of a WKND page used to generate traffic. -->

## Step 6: Verify telemetry in your observability platform

Allow a few minutes for the first data to arrive, then open your observability platform.

### Find the AEM service

Search for an AEM service name similar to:

```text
cm-p<program>-e<environment>-aem-publish-<environment-type>
```

For example, a Publish service in a production environment may resemble `cm-p12345-e67890-aem-publish-prod`. Replace these identifiers with those from your environment.

<!-- TODO: Screenshot showing the AEM service in the provider's service list. -->

### Inspect traces

Look for inbound HTTP request spans corresponding to WKND page requests. Open a trace and review its request name, duration, and related spans.

<!-- TODO: Screenshot of a real WKND request trace. -->

### Inspect metrics

Because `metrics: true` is configured, check for JVM and HTTP metrics, such as:

- `jvm.memory.used`
- `jvm.gc.duration`
- `jvm.thread.count`
- `http.server.request.duration`

<!-- TODO: Screenshot of JVM or HTTP request metrics for the AEM service. -->

### Optional: Enable logs

If you want to test log export, change the configuration to:

```yaml
  logs: true
```

Commit the change, run the Config Pipeline again, and inspect application logs in your destination. Be aware that the integration exports logs at the supported severity threshold; ordinary page visits may not generate log entries at that level.

>[!WARNING]
>
>If AEM Log Forwarding already sends logs to the same destination, enabling OpenTelemetry log export can produce duplicate log messages.

## Step 7: Update or disable telemetry export

To change the destination or signal selection, edit `config/otel.yaml`, commit the change, and rerun the Config Pipeline.

To disable customer telemetry export, set:

```yaml
  enabled: false
```

Then commit the change and run the Config Pipeline again. If your environment currently uses the legacy built-in APM integration, review migration and rollback restrictions in the [product documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/opentelemetry-apm-integration) before disabling OpenTelemetry.

## Troubleshooting

If the pipeline fails or no telemetry arrives, start with these checks:

| Symptom | What to check |
| --- | --- |
| Configuration appears to be ignored | Confirm `metadata.envTypes` includes the target environment type. |
| Secret reference error | Confirm `OTEL_CUSTOMER_AUTH` exists as a **secret environment variable**, applied to all services. |
| Authentication failure (`401` or `403`) | Check the credential type, value, and authentication header required by your provider. |
| Endpoint unreachable | Check the URL, region, and HTTPS connectivity. Private destinations may require Advanced Networking. |
| Pipeline completes but no data appears | Wait a few minutes, generate WKND traffic, then check the provider's ingestion status and service-name filters. |
| No logs appear | Check `logs: true` and whether the application has emitted logs at the supported severity. |

For a complete error reference, see the [OpenTelemetry product documentation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/opentelemetry-apm-integration).

## Next steps

You have configured an OpenTelemetry destination for an AEM as a Cloud Service environment and learned how to verify incoming telemetry from WKND.

Continue with the next tutorial, **Explore AEM telemetry in your observability platform**, to investigate traces, JVM and HTTP metrics, and logs in more detail.

## Additional resources

- [OpenTelemetry in AEM as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/opentelemetry-apm-integration)
- [AEM WKND sample project](https://github.com/adobe/aem-guides-wknd)
- [Configure Advanced Networking](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/configuring-advanced-networking)
