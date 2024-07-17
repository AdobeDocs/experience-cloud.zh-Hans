---
title: 退回摘要
description: 使用弹回摘要现成报告，了解已发送营销活动的状态以及他们可能遇到的错误。
audience: end-user
level: Intermediate
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
exl-id: b341edad-aa82-43d8-a5a1-b33a19973a1a
source-git-commit: 34c6f8a137a9085b26c0ea8f78930cff6192cfc9
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 1%

---

# 退回摘要{#bounce-summary}

该报告会详细描述在投放期间遇到的整体硬错误和软错误，以及退回的自动处理。

![](assets/campaign_reports_bounces.png)

每个表格都由摘要数字和图表表示。 您可以更改详细信息在其各自可视化图表设置中的显示方式。

**失败5重新分区**&#x200B;列出了隔离数量最多的五个投放：

**退回原因**&#x200B;表包含导致每次投放退回的错误类型的可用数据：

* **[!UICONTROL 用户未知]**：将投放发送到无效的电子邮件地址时生成的错误类型。
* **[!UICONTROL 无效域]**：将投放发送到域错误或不再存在的电子邮件地址时生成的错误类型。
* **[!UICONTROL 不可访问]**：在邮件投放字符串中遇到的错误类型，如暂时无法访问域。
* **[!UICONTROL 帐户已禁用]**：将投放发送到不再存在的电子邮件地址时生成的错误类型。
* **[!UICONTROL 邮箱已满]**：收件人的收件箱已满时生成的错误类型。 在生成此错误之前，会尝试五次传递消息。
* **[!UICONTROL 未连接]**：在发送消息时，收件人的手机已关闭或未连接到网络时生成的错误类型。

  >[!NOTE]
  >
  >此类错误仅与移动渠道中的投放有关。

* **[!UICONTROL 已拒绝]**：当Internet服务提供商(ISP)拒绝地址时生成的错误类型。 例如，当反垃圾邮件软件应用了安全规则时。

**域重新分区**&#x200B;表根据收件人域显示投放期间遇到的整体问题。
