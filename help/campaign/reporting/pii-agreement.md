---
title: 动态报告快速入门
description: 了解有关动态报告使用协议的更多信息
level: Beginner
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
audience: end-user
source-git-commit: c6a6cb7da640c9c29af71487e468f38ebf51d4f6
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 1%

---


# 动态报告使用协议 {#pii-agreement}

动态报告使用协议的目的是作为数据处理的弹出窗口同意。 默认情况下，协议仅可见，并且只有分配了管理权限的用户才能接受或拒绝协议。

要访问动态报告使用协议，请选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 高级]** > **[!UICONTROL 部署向导]**。

![](assets/pii-agreement.png)

提供了三个选项：

* **[!UICONTROL 稍后再问]**：在您接受或拒绝协议之前，配置文件维度将不会显示在您的报表中，并且不会收集或发送您客户的个人身份信息。
* **[!UICONTROL 接受]**：接受此协议，即表示您授权Adobe Campaign收集客户的个人身份信息并将其传输到报表或数据中心。
* **[!UICONTROL 拒绝]**：如果拒绝协议，配置文件维度将不会显示在您的报表中，并且不会收集或发送客户的个人身份信息。 请注意，在这种情况下，仍会收集externalID并将其用于识别最终用户。

下表显示接受此协议后发生的情况，具体取决于您所在的区域。

|  | 动态报告 | Microsoft Dynamics 365连接器 |
|---|---|---|
| 美洲和APAC （亚太） | **功能可用**。 <br>所有现成（即城市、国家/地区、州/省、性别和年龄段）和自定义用户档案信息均推送到美国报告中心。 | **功能可用**。 <br>所有现成的用户档案和自定义用户档案字段以及Adobe Campaign事件字段都在美国数据中心进行处理。 |
| EMEA（欧洲、中东和非洲） | **功能可用**。 <br>所有现成（即城市、国家/地区、州、性别和年龄段）和推送到EMEA报告中心的自定义配置文件信息。 | **功能可用。** <br>在EMEA数据中心中处理的所有现成配置文件字段和自定义配置文件字段以及Adobe Campaign事件字段。 <br>**[!UICONTROL 控制数据&#x200B;]**，其中包含已发送并存储在美国数据中心的Adobe I/O注册数据和客户最终用户事件的ID。 |

下表根据您所在的地区显示拒绝此协议后发生的情况。 请注意，即使您拒绝此协议，也仍然可以提供有关投放和Microsoft Dynamics 365集成的报告。

| 区域 | 动态报告 | Microsoft Dynamics 365连接器 |
|---|---|---|
| 美洲和APAC （亚太） | **功能可用**。 <br>没有现成的和自定义的配置文件信息推送到US报告中心，ExternalID除外。 | **功能可用**。 <br>除外部ID和收件人ID外，没有现成或自定义的配置文件字段发送到美国数据中心。 <br>所有在美国数据中心处理的Adobe Campaign事件字段，但镜像页面ID除外。 |
| EMEA（欧洲、中东和非洲） | **功能可用**。 <br>除ExternalID外，没有现成的用户档案和自定义用户档案信息推送到EMEA报告中心。 | **功能可用。** <br>除外部ID和收件人ID外，没有现成或自定义的配置文件字段发送到EMEA数据中心。 <br>在EMEA数据中心中处理的所有Adobe Campaign事件字段，但镜像页面ID除外。 |

此选择不是最终选择，您始终可以通过在&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 平台]** > **[!UICONTROL 选项]**&#x200B;中选择&#x200B;**[!UICONTROL realtimeReporting_collectPII]**&#x200B;选项来更改它。

此值可随时更改。 值1对应于&#x200B;**[!UICONTROL 稍后询问我]**、2 **[!UICONTROL 拒绝]**&#x200B;和3 **[!UICONTROL 接受]**。
