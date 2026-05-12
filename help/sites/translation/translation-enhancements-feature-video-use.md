---
title: Translation Enhancements in AEM
description: AEM's robust translation framework allows AEM content to be seamlessly translated by supported Translation vendors. Learn about the latest enhancements.
version: Experience Manager 6.4, Experience Manager 6.5
topic: Localization
feature: Multi Site Manager, Language Copy
role: User
level: Beginner
doc-type: Feature Video
exl-id: 21633308-ffe4-4023-affe-59269504da69
duration: 677
TQID: https://experienceleague.adobe.com/0aHaL2jwjKMdiK2XDSTQHkqy9ubTUqTvVLf2NpTjres
product_v2:
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ae478996-b206-4712-9b0c-dc78a2644453
    internal-label: Integrations
  - id: d429a63e-ade4-4117-b04e-9b996d1c94ef
    internal-label: Integrations
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Translation Enhancements with Multi-Site Manager {#translation-enhancements}

AEM's robust translation framework allows AEM content to be seamlessly translated by supported Translation vendors.

## Translation Enhancements in AEM 6.5

>[!VIDEO](https://video.tv.adobe.com/v/27405?quality=12&learn=on)

AEM 6.5 translation enhancements includes:

**Auto-approve translation jobs**: The approval flag in the translation job is a binary property. It does not drive or integrate with out-of-the-box review and approval workflows. To keep the number of steps in a translation job minimal,  It is by default set to "automatically approve" in [!UICONTROL Advanced Properties] of a Translation Project. If your organization requires approval for a translation job, you can uncheck the "automatically approve" option in [!UICONTROL Advanced Properties] of a Translation Project.

**Automatically delete translation launches**: Rather than manually deleting translation launches in Launches Admin after the fact, it is now possible to automatically delete translation launches after they were promoted.

**Export Translation objects in JSON format**: AEM 6.4 and earlier versions support XML and XLIFF formats of translations objects. You can now configure the export format to JSON format using your systems console [!UICONTROL Config Manager]. Look for [!UICONTROL Translation Platform Configuration], and then you can select the export format as JSON.

**Update translated AEM content in Translation Memory (TMS)**: local author who does not have access to AEM can make updates to translated content, that was already ingested back into AEM, directly in the TM (Translation Memory, in TMS), and to update the translations in AEM by resending translation job from TMS to AEM

## Translation Enhancements in AEM 6.4

>[!VIDEO](https://video.tv.adobe.com/v/21309?quality=12&learn=on)

Authors can now quickly and easily create multi-language translation projects directly from either the Sites admin or the Projects admin, set up those projects to automatically promote launches, and even set schedules for automation.

## Additional Resources {#additional-resources}

* [Translating Content for Multilingual Sites](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/translation.html)
* [https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/tc-manage.html](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/tc-manage.html)
* [Translation Best Practices](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/tc-bp.html)
