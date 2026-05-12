---
title: Send form attachments in an e-mail
description: Extract and send submitted form attachments in an e-mail using power automate workflow
solution: Experience Manager, Experience Manager Forms
type: Documentation
role: Developer
level: Beginner, Intermediate
version: Experience Manager as a Cloud Service
feature: Adaptive Forms
topic: Development
jira: KT-11077
exl-id: 1be90d9b-3669-44a0-84fb-cbdec44074d8
duration: 391
badgeVersions: label="AEM Forms as a Cloud Service" before-title="false"
TQID: https://experienceleague.adobe.com/j4Dj-RGeJWcIxQIPFzfXGTNoFo4Ev-Kvpjc9HOBtPFo
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Extract form attachments from submitted form data

Extract form attachments and send the attachments in an e-mail in power automate workflow.
The following video explains the steps needed to form attachments from the submitted data.
>[!VIDEO](https://video.tv.adobe.com/v/3409017?quality=12&learn=on)

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
