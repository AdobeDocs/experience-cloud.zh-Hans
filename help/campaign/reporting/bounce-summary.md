---
title: 退回摘要
description: 使用弹回摘要现成报告，了解已发送营销活动的状态以及他们可能遇到的错误。
audience: end-user
level: Intermediate
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard迁移的用户"
exl-id: b341edad-aa82-43d8-a5a1-b33a19973a1a
TQID: https://experienceleague.adobe.com/gfOXWpdQvONw72sdpnGehwpXcgte16B6dLiWV2LZXOc
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: ad84694f2f6f45e4ee30fc51379106835ac302be
workflow-type: tm+mt
source-wordcount: 298
ht-degree: 8%

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
