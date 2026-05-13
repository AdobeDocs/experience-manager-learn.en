---
title: Using AEM Forms with Chatbot
description: Parse ChatBot data
feature: Adaptive Forms
version: Experience Manager 6.5
jira: KT-15344
topic: Development
role: User
level: Intermediate
exl-id: 3c304b0a-33f8-49ed-a576-883df4759076
duration: 22
TQID: https://experienceleague.adobe.com/fmg1H57FrA6uf0nmLBWvpUMUHJZXNQXxzk32hY7Qnq4
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
---
# Parse ChatBot data

A [ChatBot webhook](https://www.chatbot.com/help/webhooks/what-are-webhooks/) was used to send the ChatBot data to an AEM servlet.
The data captured in the ChatBot is in JSON format with the user entered data in the attributes object as shown below
![chatbot-data](assets/chat-bot-data.png)

To merge the data with the XDP template, we need to create the following XML. Notice the root element of the xml, this has to match with the root element of the XDP template for the data to merge successfully.


```xml
<topmostSubForm>
    <f1_01>David Smith</f1_01>
    <signmethod>ESIGN</signmethod>
    <corporation>1</corporation>
    <f1_08>San Jose, CA, 95110</f1_08>
    <f1_07>345 Park Avenue</f1_07>
    <ssn>123-45-6789</ssn>
    <form_name>W-9</form_name>
</topmostSubForm>

```

![xdp-template](assets/xdp-template.png)

## Next Steps

[Merge data with XDP template](./merge-data-with-template.md)
