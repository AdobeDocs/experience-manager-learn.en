---
title: Understanding Check-in/Check-out in AEM Assets
seo-title: Understanding Check-in/Check-out in AEM Assets
description: A technical deep-dive into how Asset's check-in/check-out feature works, and practical considerations when delivering projects leveraging this feature.
seo-description: A technical deep-dive into how Asset's check-in/check-out feature works, and practical considerations when delivering projects leveraging this feature.
uuid: ef13bb98-c617-4a23-a305-5361a4aeadb9
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
topic-tags: aem-desktop-app
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: collaboration
discoiquuid: 0746cb35-c287-4b03-9866-c768f9906728
targetaudience: target-audience advanced
---

# Understanding Check-in/Check-out in AEM Assets{#understanding-check-in-check-out-in-aem-assets}

A technical deep-dive into how Asset's check-in/check-out feature works, and practical considerations when delivering projects leveraging this feature.

## Check-in/check-out state management {#check-in-check-out-state-management}

>[!VIDEO](https://video.tv.adobe.com/v/16755/?quality=9)

When an asset has been checked out the **cq:drivelock** property is set to the principal user name which holds the Checkout lock.

* **[dam:Asset]/jcr:content@cq:drivelock=&lt;principalNameThatHoldsTheCheckOutLock&gt**

When an asset is checked in, the** [dam:Asset]/jcr:content@cq:drivelock **property is removed from the asset.

>[!NOTE]
>
>No ACL is added to the asset during check-in/check-out and the lock status is managed only with **cq:drivelock** property

## User permissions {#user-permissions}

>[!VIDEO](https://video.tv.adobe.com/v/16753/?quality=9)

Associated with asset check-in/check-out there are mainly three type of user permissions:

* Unable to check-out an asset
  * Read-only access
  * jcr:read privilege

* Able to check-in/check-out an asset
  * Read and write access
  * rep:write privilege

* Able to force check-in an asset, which has been checked out by another user
  * administrator access
  * jcr:all privilege

## ClassicUI considerations {#classicui-considerations}

>[!VIDEO](https://video.tv.adobe.com/v/16752/?quality=9)

Check-in/check-out lock status for an asset is managed by using the property: **[dam:Asset]/jcr:content@cq:drivelock** and doesnt use ACL's or JCR Level locking. This is consistent with the AEM Desktop App's check-in/out approach.

Check-in/check-out status works well in Touch UI. Checked out assets can be changed based on user's ACL restrictions via ClassicUI.

>[!NOTE]
>
>It is best to restrict access to **/damadmin** if the check-in/check-out limitations must be respected.

## The AssetCheckoutService API {#the-assetcheckoutservice-api}

>[!VIDEO](https://video.tv.adobe.com/v/16754/?quality=9)

For custom development, see the APIs links below which provide the facilities for checking lock status, and checking in/out of Assets. The new AssetsCheckoutService API helps to check the status of an asset before any update is performed.

### Code snippet without checks {#code-snippet-without-checks}

```java

<%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false" contentType="text/html; charset=utf-8" 
 pageEncoding="UTF-8"
    import="org.apache.sling.api.resource.*,
    com.day.cq.commons.jcr.JcrUtil,
    com.day.cq.dam.commons.util.DamUtil,
    java.util.*,
    javax.jcr.*,
    com.day.cq.search.*,
    com.day.cq.wcm.api.*,
    com.day.cq.dam.api.*"%><%

    // Code here
    String SRC_ASSET_PATH = "/content/dam/code/without-checks/some-other-asset.png";
    String CHECKED_OUT_ASSET_PATH = "/content/dam/code/without-checks/checked-out.png";
    
    // Get the source asset
    Asset src = DamUtil.resolveToAsset(resourceResolver.getResource(SRC_ASSET_PATH));
    
    // Get the checked out asset
    Asset dest = DamUtil.resolveToAsset(resourceResolver.getResource(CHECKED_OUT_ASSET_PATH));

    // Update the original rendition of the checked-out asset
    dest.addRendition("original", src.getOriginal().getStream(), src.getMimeType());

    resourceResolver.commit();

%>Update of the checked out asset performed as: <%= resourceResolver.getUserID() %>
```

### Code snippet with checks {#code-snippet-with-checks}

```java

<%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false" contentType="text/html; charset=utf-8" 
 pageEncoding="UTF-8"
    import="org.apache.sling.api.resource.*,
    com.day.cq.dam.api.checkout.AssetCheckoutService,
    com.day.cq.dam.commons.util.DamUtil,
    com.day.cq.commons.jcr.JcrUtil,
    java.util.*,
    javax.jcr.*,
    com.day.cq.search.*,
    com.day.cq.wcm.api.*,
    com.day.cq.dam.api.*"%><%

    // Code here
    String SRC_ASSET_PATH = "/content/dam/code/with-checks/some-other-asset.png";
    String CHECKED_OUT_ASSET_PATH = "/content/dam/code/with-checks/checked-out.png";
    
    // Asset Checkout OSGi Service
    AssetCheckoutService assetCheckout = sling.getService(AssetCheckoutService.class);

    // Get the original binary for the checked out asset
    Asset src = DamUtil.resolveToAsset(resourceResolver.getResource(SRC_ASSET_PATH));
    // Get the original binary for some other asset to replace the checked out asset's original binary with
    Asset dest = DamUtil.resolveToAsset(resourceResolver.getResource(CHECKED_OUT_ASSET_PATH));

    // Current user
    String userID = resourceResolver.getUserID();
    // Check if the asset is checked
    boolean isCheckedOut =  assetCheckout.isCheckedOut(dest);
    // The user that checked the asset out
    String checkedOutUserID = assetCheckout.getCheckedOutBy(dest);
    // Is checked out by the current user
    boolean isCheckedOutBySelf = userID.equals(checkedOutUserID);
    %>
    
Is Checked out: <%= isCheckedOut %>
Is Checked out By Self: <%= userID %> == <%= checkedOutUserID %> => <%= isCheckedOutBySelf %>
    
    <%
    if (!isCheckedOut || (isCheckedOut && isCheckedOutBySelf)) {
        // Replace the checked out assets' original binary
        dest.addRendition("original", src.getOriginal().getStream(), src.getMimeType());

        resourceResolver.commit();
    %>
Original rendition updated...
        <%
    } else {
        %>
Original rendition update skipped...
        <%
    }
%>

```

## Supporting materials {#supporting-materials}

* [ACS AEM Tools - AEM Fiddle](https://adobe-consulting-services.github.io/acs-aem-tools/features/aem-fiddle.html)