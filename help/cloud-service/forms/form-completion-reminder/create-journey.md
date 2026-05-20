---
title: Create journey
description: The first step in building the abandoned form re-engagement journey in Adobe Journey Optimizer (AJO) is to define the custom events that will drive the journey orchestration
solution: Experience Manager, Experience Manager Forms, Journey Optimizer
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
feature: Adaptive Forms
topic: Integrations, Development
jira: KT-21185
badgeIntegration: label="Integration" type="positive"
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"

---

# Create journey

Using the custom events created earlier, this journey is designed to handle both successful form submissions and abandoned form scenarios.

The journey begins when a customer triggers the StartFormFillingEvent, indicating that they have started interacting with the form. The email address captured from the form is available in the `event's contextual data` and is used by Adobe Journey Optimizer for customer identification and email delivery.

The journey then listens for the FormSubmittedEvent, which represents a successful form submission.

If the customer submits the form within the configured timeout period (5 minutes in this example), the journey checks whether the FormSessionID from the submission event matches the session associated with the form-start event. This validation ensures that the submission corresponds to the same form interaction session.

If the FormSessionID matches, the customer is sent a confirmation or thank-you email for successfully submitting the form, and the journey ends.
If the session ID does not match, the customer is routed to the alternate path.

If no form submission event is received within 5 minutes after the form-start event, the customer is considered to have abandoned the form. In this case, the journey sends a reminder email encouraging the customer to return and complete the form, after which the journey ends.

The following screenshot illustrates the completed journey configuration in Adobe Journey Optimizer using the custom events created earlier.

![journey-diagram](assets/journey-diagram.png)

