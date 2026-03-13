---
title: SAML 2.0 Custom Login Hook
description: Learn how to develop a custom SAML 2.0 login hook for AEM.
version: Experience Manager as a Cloud Service
feature: Security
topic: Development, Security
role: Developer
level: Intermediate
last-substantial-update: 2025-03-11
duration: 520
exl-id: a401823a-416c-4b35-9cdb-bd432f066279
---
# SAML 2.0 login hook   

Learn how to develop a custom SAML 2.0 login hook for AEM. This tutorial provides step-by-step instructions to create a custom login hook that integrates with a SAML 2.0 identity provider, allowing users to authenticate using their SAML credentials.

If the IDP cannot send the user profile data and the user group membership in the SAML assertion, or if the data needs to be transformed before synchronization to AEM, custom SAML hooks can be implemented to extend the SAML authentication process. SAML hooks allow customization of group membership assignment, modification of user profile attributes, and addition of custom business logic during the authentication flow.

>[!NOTE]
>Custom SAML hooks are supported on **AEM as a Cloud Service** and **AEM LTS**. This feature is not available on older AEM versions.

## Common use cases

Custom SAML hooks are useful when it is necessary to:

+ Dynamically assign group membership based on custom business logic beyond what's provided in SAML assertions
+ Transform or enrich user profile data before it's synchronized to AEM
+ Map complex SAML attribute structures to AEM user properties
+ Implement custom authorization rules or conditional group assignments
+ Add custom logging or auditing during SAML authentication
+ Integrate with external systems during the authentication process

## `SamlHook` OSGi service interface

The `com.adobe.granite.auth.saml.spi.SamlHook` interface provides two hook methods that are invoked at different stages of the SAML authentication process:

### `postSamlValidationProcess()` method

This method is called **after** the SAML response has been validated but **before** the user synchronization process starts. This is the ideal place to modify the SAML assertion data, such as adding or transforming attributes.

```java
public void postSamlValidationProcess(
    HttpServletRequest request, 
    Assertion assertion, 
    Message samlResponse)
```

#### Use cases

+ Add additional group memberships to the assertion
+ Transform attribute values before they are synchronized
+ Enrich the assertion with data from external sources
+ Validate custom business rules

### `postSyncUserProcess()` method

This method is called **after** the user synchronization process has been completed. This hook can be used to perform additional operations after the AEM user has been created or updated.

```java
public void postSyncUserProcess(
    HttpServletRequest request, 
    HttpServletResponse response, 
    Assertion assertion,
    AuthenticationInfo authenticationInfo, 
    String samlResponse)
```

#### Use cases

+ Update additional user profile properties not covered by standard synchronization
+ Create or update custom user-related resources in AEM
+ Trigger workflows or notifications after user authentication
+ Log custom authentication events

**Important:** To modify user properties in the repository, the hook implementation requires:

+ A `SlingRepository` reference injected via `@Reference`
+ A configured [service user](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/advanced/service-users) with appropriate permissions (configured in "Apache Sling Service User Mapper Service Amendment")
+ Proper session management with try-catch-finally blocks

## Implement a custom SAML hook

The following steps outline how to create and deploy a custom SAML hook.

### Create the SAML hook implementation

Create a new Java class in the AEM project that implements the `com.adobe.granite.auth.saml.spi.SamlHook` interface:

```java
package com.mycompany.aem.saml;

import com.adobe.granite.auth.saml.spi.Assertion;
import com.adobe.granite.auth.saml.spi.Attribute;
import com.adobe.granite.auth.saml.spi.Message;
import com.adobe.granite.auth.saml.spi.SamlHook;
import org.apache.jackrabbit.api.JackrabbitSession;
import org.apache.jackrabbit.api.security.user.Authorizable;
import org.apache.jackrabbit.api.security.user.UserManager;
import org.apache.sling.auth.core.spi.AuthenticationInfo;
import org.apache.sling.jcr.api.SlingRepository;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.osgi.service.component.annotations.ReferenceCardinality;
import org.osgi.service.metatype.annotations.AttributeDefinition;
import org.osgi.service.metatype.annotations.Designate;
import org.osgi.service.metatype.annotations.ObjectClassDefinition;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import javax.annotation.Nonnull;
import javax.jcr.RepositoryException;
import javax.jcr.Session;
import javax.jcr.ValueFactory;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@Component
@Designate(ocd = SampleImpl.Configuration.class, factory = true)
public class SampleImpl implements SamlHook {
    @ObjectClassDefinition(name = "Saml Sample Authentication Handler Hook Configuration")
    @interface Configuration {
        @AttributeDefinition(
                name = "idpIdentifier",
                description = "Identifier of SAML Idp. Match the idpIdentifier property's value configured in the SAML Authentication Handler OSGi factory configuration (com.adobe.granite.auth.saml.SamlAuthenticationHandler~<unique-id>) this SAML hook will hook into"
        )
        String idpIdentifier();

    }

    private static final String SAMPLE_SERVICE_NAME = "sample-saml-service";
    private static final String CUSTOM_LOGIN_COUNT = "customLoginCount";

    private final Logger log = LoggerFactory.getLogger(getClass());

    private SlingRepository repository;

    @SuppressWarnings("UnusedDeclaration")
    @Reference(name = "repository", cardinality = ReferenceCardinality.MANDATORY)
    public void bindRepository(SlingRepository repository) {
        this.repository = repository;
    }

    /**
     * This method is called after the user sync process is completed.
     * At this point, the user has already been synchronized in OAK (created or updated).
     * Example: Track login count by adding custom attributes to the user in the repository
     *
     * @param request
     * @param response
     * @param assertion
     * @param authenticationInfo
     * @param samlResponse
     */
    @Override
    public void postSyncUserProcess(HttpServletRequest request, HttpServletResponse response, Assertion assertion,
                                    AuthenticationInfo authenticationInfo, String samlResponse) {
        log.info("Custom Audit Log: user {} successfully logged in", authenticationInfo.getUser());

        // This code executes AFTER the user has been synchronized in OAK
        // The user object already exists in the repository at this point
        Session serviceSession = null;
        try {
            // Get a service session - requires "sample-saml-service" to be configured as system user
            // Configure in: "Apache Sling Service User Mapper Service Amendment"
            serviceSession = repository.loginService(SAMPLE_SERVICE_NAME, null);

            // Get the UserManager to work with users and groups
            UserManager userManager = ((JackrabbitSession) serviceSession).getUserManager();

            // Get the authorizable (user) that just logged in
            Authorizable user = userManager.getAuthorizable(authenticationInfo.getUser());

            if (user != null && !user.isGroup()) {
                ValueFactory valueFactory = serviceSession.getValueFactory();

                // Increment login count
                long loginCount = 1;
                if (user.hasProperty(CUSTOM_LOGIN_COUNT)) {
                    loginCount = user.getProperty(CUSTOM_LOGIN_COUNT)[0].getLong() + 1;
                }
                user.setProperty(CUSTOM_LOGIN_COUNT, valueFactory.createValue(loginCount));
                log.debug("Set {} property to {} for user {}", CUSTOM_LOGIN_COUNT, loginCount, user.getID());

                // Save all changes to the repository
                if (serviceSession.hasPendingChanges()) {
                    serviceSession.save();
                    log.debug("Successfully saved custom attributes for user {}", user.getID());
                }
            } else {
                log.warn("User {} not found or is a group", authenticationInfo.getUser());
            }

        } catch (RepositoryException e) {
            log.error("Error adding custom attributes to user repository for user: {}",
                     authenticationInfo.getUser(), e);
        } finally {
            if (serviceSession != null) {
                serviceSession.logout();
            }
        }
    }

    /**
     * This method is called after the SAML response is validated but before the user sync process starts.
     * We can modify the assertion here to add custom attributes.
     *
     * @param request
     * @param assertion
     * @param samlResponse
     */
    @Override
    public void postSamlValidationProcess(@Nonnull HttpServletRequest request, @Nonnull Assertion assertion, @Nonnull Message samlResponse) {
        // Add the attribute "memberOf" with value "sample-group" to the assertion
        // In this example "memberOf" is a multi-valued attribute that contains the groups from the Saml Idp
        log.debug("Inside postSamlValidationProcess");
        Attribute groupsAttr = assertion.getAttributes().get("groups");
        if (groupsAttr != null) {
            groupsAttr.addAttributeValue("sample-group-from-hook");
        } else {
            groupsAttr = new Attribute();
            groupsAttr.setName("groups");
            groupsAttr.addAttributeValue("sample-group-from-hook");
            assertion.getAttributes().put("groups", groupsAttr);
        }
    }

}
```

### Configure the SAML hook

The SAML hook uses OSGi configuration to specify which IDP it should apply to. Create an OSGi configuration file in the project at:

`/ui.config/src/main/content/jcr_root/wknd-examples/osgiconfig/config.publish/com.mycompany.aem.saml.CustomSamlHook~okta.cfg.json`

```json
{
  "idpIdentifier": "$[env:SAML_IDP_ID;default=http://www.okta.com/exk4z55r44Jz9C6am5d7]",
  "service.ranking": 100
}
```

The `idpIdentifier` must match the `idpIdentifier` value configured in the corresponding SAML Authentication Handler OSGi factory configuration (PID: `com.adobe.granite.auth.saml.SamlAuthenticationHandler~<unique-id>.cfg.json`). This matching is critical: the SAML hook will only be invoked for the SAML Authentication Handler instance that has the same `idpIdentifier` value. The SAML Authentication Handler is a factory configuration, meaning you can have multiple instances (e.g., `com.adobe.granite.auth.saml.SamlAuthenticationHandler~okta.cfg.json`, `com.adobe.granite.auth.saml.SamlAuthenticationHandler~azure.cfg.json`), and each hook is tied to a specific handler via the `idpIdentifier`. The `service.ranking` property controls the execution order when multiple hooks are configured (higher values execute first).

### Add Maven dependencies

Add the required SAML SPI dependency to the AEM Maven core project's `pom.xml`.

**For AEM as a Cloud Service projects**, use the AEM SDK API dependency which includes the SAML interfaces:

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>aem-sdk-api</artifactId>
    <version>${aem.sdk.api}</version>
    <scope>provided</scope>
</dependency>
```

The `aem-sdk-api` artifact contains all necessary Adobe Granite SAML interfaces including `com.adobe.granite.auth.saml.spi.SamlHook`.

### Configure service user (optional)

If the SAML hook needs to modify content in AEM's JCR respository, such as user properties, (as shown in the `postSyncUserProcess` example), a [service user](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/advanced/service-users) must be configured:

1. Create a service user mapping in the project at `/ui.config/src/main/content/jcr_root/apps/myproject/osgiconfig/config/org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended~saml.cfg.json`:

```json
{
  "user.mapping": [
    "com.mycompany.aem.core:sample-saml-service=saml-hook-service"
  ]
}
```

1. Create a repoinit script to define the service user and permissions at `/ui.config/src/main/content/jcr_root/apps/myproject/osgiconfig/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~saml.cfg.json`:

```
create service user saml-hook-service with path system/saml

set ACL for saml-hook-service
    allow jcr:read,rep:write,rep:userManagement on /home/users
end
```

This grants the service user permissions to read and modify user properties in the repository.

### Deploy to AEM

Deploy the custom SAML hook to AEM as a Cloud Service:

1. Build the AEM project
1. Commit the code to the Cloud Manager Git repository
1. Deploy using a Full Stack deployment pipeline
1. The SAML hook will be automatically activated when a user authenticates via SAML


### Important considerations

+ **IDP Identifier matching**: The `idpIdentifier` configured in the SAML hook must exactly match the `idpIdentifier` in the SAML Authentication Handler factory configuration (`com.adobe.granite.auth.saml.SamlAuthenticationHandler~<unique-id>`)
+ **Attribute names**: Ensure the attribute names referenced in the hook (e.g., `groupMembership`) match the attributes configured in the SAML Authentication Handler
+ **Performance**: Keep hook implementations lightweight as they are executed during every SAML authentication
+ **Error handling**: SAML hook implementations should throw `com.adobe.granite.auth.saml.spi.SamlHookException` when critical errors occur that should fail the authentication. The SAML Authentication Handler will catch these exceptions and return `AuthenticationInfo.FAIL_AUTH`. For repository operations, always catch `RepositoryException` and log errors appropriately. Use try-catch-finally blocks to ensure proper cleanup of resources
+ **Testing**: Test custom hooks thoroughly in lower environments before deploying to production
+ **Multiple hooks**: Multiple SAML hook implementations can be configured; all matching hooks will be executed. Use the `service.ranking` property in the OSGi component to control the execution order (higher ranking values execute first). To reuse a SAML hook across multiple SAML Authentication Handler factory configurations (`com.adobe.granite.auth.saml.SamlAuthenticationHandler~<unique-id>`), create multiple hook configurations (OSGi factory configurations), each with a different `idpIdentifier` matching the respective SAML Authentication Handler
+ **Security**: Validate and sanitize all data from SAML assertions before using them in business logic
+ **Repository access**: When modifying user properties in `postSyncUserProcess`, always use a [service user](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/advanced/service-users) with appropriate permissions rather than administrative sessions
+ **Service user permissions**: Grant minimal required permissions to the [service user](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/advanced/service-users) (e.g., only `jcr:read` and `rep:write` on `/home/users`, not full admin rights)
+ **Session management**: Always use try-catch-finally blocks to ensure repository sessions are properly closed, even if exceptions occur
+ **User synchronization timing**: The `postSyncUserProcess` hook executes after the user has been synchronized to OAK, so the user object is guaranteed to exist in the repository at that point
