---
title: 全局禁止列表
description: 了解全局禁止列表
hide: true
source-git-commit: a946cfb1027896f6e45aaf88d25ad7114d6b5ac6
workflow-type: ht
source-wordcount: '628'
ht-degree: 100%

---

# 全局禁止列表 {#global-suppression-list}

禁止列表由客户要从其投递中排除的电子邮件地址组成，因为发给这些联系人可能会损害其发送信誉和投递率。目前，Adobe 留存一份已证明损害参与和邮件声誉的已知不良电子邮件地址的最新列表，并确保不将电子邮件投递到这些地址。在所有 Adobe 客户共有的一个全局禁止列表中管理此列表。全局禁止列表中包含的地址和域名被隐藏起来。在投递报告中仅指示被排除的收件人数量。

现在可以从一个供内部使用的界面管理全局禁止列表。只有投递顾问将维护此列表。全局禁止列表可以包括电子邮件或域地址。

## 访问全局禁止列表

要访问排除的电子邮件地址和域的详细列表，请转到&#x200B;**[!UICONTROL 全局禁止列表]**。

>[!CAUTION]
>
>查看、导出和管理全局禁止列表的权限取决于将您分配到的分发列表。了解详情

其中显示两个选项卡：**[!UICONTROL 电子邮件]**&#x200B;和&#x200B;**[!UICONTROL 域]**。

其中提供过滤器以帮助您浏览列表。

## 添加地址和域

目前有两种方式可将地址添加到全局禁止列表：

* 由投递团队精心整理的列表。
* 由第三方服务提供商 Blackbox 提供的列表。

可[一次一个地](#add-one-address-or-domain)或通过上传 CSV 文件[以批量方式](#upload-csv-file)添加电子邮件地址或域。

为此，请选择&#x200B;**[!UICONTROL 添加电子邮件或域]**&#x200B;按钮，然后按照以下方法之一进行操作。

### 添加一个地址或域 {#add-one-address-or-domain}

1. 选择&#x200B;**[!UICONTROL 逐个]**&#x200B;选项。

1. 选择地址类型：**[!UICONTROL 电子邮件地址]**&#x200B;或&#x200B;**[!UICONTROL 域地址]**。

1. 输入您要从发送中排除的电子邮件地址或域。

   >[!NOTE]
   >
   >确保输入有效的电子邮件地址（例如 abc@company.com）或域（例如 abc.company.com）。

1. 如果需要，请指定原因。

   >[!NOTE]
   >
   >在此字段中允许使用值为 32 至 126 的所有 ASCII 可打印字符。可在[此页面](https://en.wikipedia.org/wiki/Wikipedia:ASCII#ASCII_printable_characters){target="_blank"}上找到完整列表以供参考。

1. 单击&#x200B;**[!UICONTROL 提交]**&#x200B;以确认。

### 上传 CSV 文件 {#upload-csv-file}

1. 选择&#x200B;**[!UICONTROL 上传 CSV]** 选项。

1. 下载要使用的 CSV 模板，该模板包括以下列和格式：

   ```
   TYPE,VALUE,COMMENT
   EMAIL,abc@somedomain.com,Comment
   DOMAIN,somedomain.com,Comment
   ```

   >[!CAUTION]
   >
   >请勿更改 CSV 模板中的列名。
   >
   >文件大小不应超过 1 MB。

1. 将要添加到禁止列表的电子邮件地址和/或域填入该 CSV 模板。

   >[!NOTE]
   >
   >在&#x200B;**备注**&#x200B;列中允许使用值为 32 至 126 的所有 ASCII 字符。可在[此页面](https://en.wikipedia.org/wiki/Wikipedia:ASCII#ASCII_printable_characters){target="_blank"}上找到完整列表以供参考。

1. 完成后，拖放您的 CSV 文件，然后单击&#x200B;**[!UICONTROL 提交]**&#x200B;以确认。

>[!NOTE]
>
>上传完毕后，通过在界面中检查其状态而确保其成功。[了解如何操作](#recent-uploads)

### 检查最近的上传状态 {#recent-uploads}

单击&#x200B;**[!UICONTROL 最近的上传]**&#x200B;按钮以检查您上传的最新 CSV 文件的状态。

可能的状态是：

* **[!UICONTROL 待定]**：正在处理文件上传。
* **[!UICONTROL 错误]**：由于技术问题或文件格式错误，文件上传过程失败。
* **[!UICONTROL 完成]**：成功完成了文件上传过程。

在上传过程中，如果某些地址的格式不正确，则不将这些地址添加到全局禁止列表。

在这种情况下，当上传完毕后，它与某个报告关联。可下载该报告以检查遇到的错误。

## 删除地址

要从全局禁止列表中删除地址，请使用&#x200B;**[!UICONTROL 删除]**&#x200B;按钮。

>[!CAUTION]
>
>顾问无法通过界面删除由第三方服务提供商 Blackbox 自动添加的地址或域。只能通过后端工单执行此操作。

