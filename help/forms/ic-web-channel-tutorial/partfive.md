---
title: Creating Document Fragments to hold the recipient name and address
seo-title: Creating Document Fragments to hold the recipient name and address
description: This is part 5 of a multi-step tutorial for creating your first interactive communications document. In this part, we will create document fragment to hold the recipient name and address. 
seo-description: This is part 5 of a multi-step tutorial for creating your first interactive communications document. In this part, we will create document fragment to hold the recipient name and address. 
uuid: 689931e4-a026-4e62-9acd-552918180819

feature: interactive-communication
topics: development
audience: developer
doc-type: tutorial
activity: implement
version: 6.4,6.5
discoiquuid: 404eed65-ec55-492a-85b5-59773896b217

---

# Creating Document Fragments to hold the recipient name and address {#creating-document-fragments-to-hold-the-recipient-name-and-address}

In this part, we will create document fragment to hold the recipient name and address.

>[!VIDEO](https://video.tv.adobe.com/v/22350/?quality=9)

Document fragments hold the text content of interactive communication documents. This text content can be static text or inserted from the underlying data model elements values. For example Dear {name}, where Dear is static text and {name} is the form data element name. At runtime, this will resolve to Dear Gloria Rios or Dear John Jacobs depending on the value of the name element.

The rich text editor is intuitive enough for a business user to author text and inserts form data elements. The document fragment editor has the ability to format text, specify font types and styles, ability to insert special characters and create hyperlinks.

The document fragment editor also has the ability to insert inline conditions in your text as demonstrated in this [video](https://helpx.adobe.com/experience-manager/kt/forms/using/editing-improvements-correspondence-mgmt-feature-video-use.html)

>[!NOTE]
>
>Make sure the Form Data Model elements you insert into a document fragments are descendants of the root element. For example in this use case make sure the User object's elements that you select is the child of the balances object

