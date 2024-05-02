---
title: 推送通知报告
description: 使用推送通知现成报告，了解推送通知是否成功。
level: Intermediate
audience: end-user
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
source-git-commit: 3f4400f24b75e8e435610afbe49e9d9444dbf563
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# 推送通知报告{#push-notification-report}

>[!CAUTION]
>
>请注意，您必须拖放 **[!UICONTROL 消息类型]** 量度到您的表中，以根据投放类型拆分数据，在本例中是推送通知投放。

此 **推送通知** 报表提供了Adobe Campaign中推送通知营销绩效的详细信息。 此开箱即用的报表可帮助您了解用户如何与推送通知、移动应用程序和投放进行交互。

![](assets/dynamic_report_push.png)

每个表格都由摘要数字和图表表示。 您可以更改详细信息在其各自可视化图表设置中的显示方式。

第一个表 **推送通知参与摘要** 分为三类：按日、按移动应用程序和按投放。 它包含可用于收件人对投放的反应性的数据：

* **[!UICONTROL 已处理/已发送]**：发送的推送通知总数。
* **[!UICONTROL 已投放]**：成功发送的推送通知数，与已发送推送通知的总数相关。
* **[!UICONTROL 展示次数]**：将推送通知发送到设备并在通知中心保持不接触的次数。 在大多数情况下，展示次数应与交付次数相似。 这可确保设备收到消息并将该信息中继回服务器。
* **[!UICONTROL 独特展示次数]**：收件人展示的次数。
* **[!UICONTROL 点进率]**：与推送通知交互的用户百分比。
* **[!UICONTROL 打开率]**：已打开推送通知的百分比。

![](assets/dynamic_report_push_2.png)

第二张表 **推送通知点击次数和打开次数** 分为三类：按日、按移动应用程序和按投放。 它包含每次投放的收件人行为可用数据：

* **[!UICONTROL 展示次数]**：收件人看到的推送通知总数。
* **[!UICONTROL 独特展示次数]**：收件人展示的次数。
* **[!UICONTROL 单击]**：推送通知送达设备并被用户单击的次数。 用户希望查看通知（通知随后将被移动到推送打开跟踪），或者关闭它。
* **[!UICONTROL 独特点击]**：独特用户与推送通知进行交互（例如单击通知或按钮）的次数。
* **[!UICONTROL 打开]**：发送到设备并由用户单击从而打开应用程序的推送通知总数。 这与推送点击类似，不同之处在于，如果取消通知，则不会触发推送打开。
* **[!UICONTROL 独特打开次数]**：打开投放的收件人数量。
