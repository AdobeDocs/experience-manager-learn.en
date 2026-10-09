---
title: Customize Summary Component
description: Extend the summary step component to include the capability to navigate to the next form in the package.
feature: Adaptive Forms
version: Experience Manager 6.4, Experience Manager 6.5
jira: KT-6894
thumbnail: 6894.jpg
topic: Development
role: Developer
level: Experienced
exl-id: fb68579d-241c-414d-92f4-13194f4d1923
duration: 38
TQID: 'https://experienceleague.adobe.com/jn-k9KrGdNpBkAcDQuDb4LWY5KdXrDYBCgCzeg6DURI'
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
    internal-label: Experienced
---
# Customize summary step

Summary step component is used to display the summary of your form submission with a link to download the signed form. Summary step is typically placed in the last panel of your form. 
For the purpose of this use case we have created a new component based on the out of the box Summary component and extended the capability to include custom clientlib.

This component is identified by the label Sign Multiple Form

The following screen shot shows the new component that was created to display the message on completion of the signing ceremony

![summary component](assets/summary.PNG)

The new component is based on the out of the box summary component.
![component-prop](assets/componentprop.PNG)

We have added a button to navigate to the next form for signing
![template-code](assets/template-code.PNG)

The summary.jsp has the following code. It has reference to the client library identified by the category id **getnextform** 

```java
<%--
  Guide Summary Component
--%>
<%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
<%@include file="/libs/fd/afaddon/components/summary/summary.jsp"%>
<ui:includeClientLib categories="getnextform"/>

```

## Assets

The custom summary component can be [downloaded from here](assets/custom-summary-step.zip)

## Next Steps

[Get the next form for signing](./create-client-lib.md)