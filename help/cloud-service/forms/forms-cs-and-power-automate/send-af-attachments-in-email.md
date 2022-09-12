---
title: Send form attachments in an e-mail
description: Extract and send submitted form attachments in an e-mail using power automate workflow
solution: Experience Manager, Experience Manager Forms
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Cloud Service
feature: Adaptive Forms
topic: Development
kt: 11077
---
# Extract form attachments from submitted form data

Extract form attachments and send the attachments in an e-mail in power automate workflow.
The following video explains the steps needed to form attachments from the submitted data.
>[!VIDEO](https://video.tv.adobe.com/v/3409017/?quality=12&learn=on)

The following is the attachment object schema  that you need to use in the Parse JSON schema step

```json
{
    "type": "object",
    "properties": {
        "filename": {
            "type": "string"
        },
        "data": {
            "type": "string"
        },
        "contentType": {
            "type": "string"
        },
        "size": {
            "type": "integer"
        }
    }
}
```