---
title: 全局抑制列表
description: 发现全局抑制列表
hide: true
source-git-commit: a946cfb1027896f6e45aaf88d25ad7114d6b5ac6
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---

# 全局抑制列表 {#global-suppression-list}

抑制列表由客户要从投放中排除的电子邮件地址组成，因为向这些联系人发送可能会损害他们的发送信誉和投放率。 目前，Adobe会保留已知错误电子邮件地址的更新列表，这些地址已证实对参与度和邮件声誉有害，并确保不会向他们发送电子邮件。 此列表在全局抑制列表中进行管理，该列表在所有Adobe客户中都是通用的。 全局禁止列表中包含的地址和域名将被隐藏。 投放报表中仅显示被排除的收件人数。

现在，可以从内部提供的界面管理全局抑制列表。 此列表将仅由可交付性顾问维护。 全局抑制列表可以包含电子邮件地址或域名地址。

## 访问全局禁止列表

要访问排除的电子邮件地址和域的详细列表，请转到 **[!UICONTROL 全局抑制列表]**.

>[!CAUTION]
>
>查看、导出和管理全局隐藏列表的权限取决于您分配给的通讯组列表。 了解更多

将显示两个选项卡： **[!UICONTROL 电子邮件]** 和 **[!UICONTROL 域]**.

过滤器可帮助您浏览列表。

## 添加地址和域

目前，有两种方法可以将地址添加到全局禁止列表：

* 可投放性团队策划的列表。
* 由第三方服务提供商Blackbox提供的列表。

您可以添加电子邮件地址或域 [一次一个](#add-one-address-or-domain)或 [在批量模式下](#upload-csv-file) 通过CSV文件上传。

为此，请选择 **[!UICONTROL 添加电子邮件或域]** 按钮，然后按照以下方法之一操作。

### 添加一个地址或域 {#add-one-address-or-domain}

1. 选择 **[!UICONTROL 一个一个]** 选项。

1. 选择地址类型： **[!UICONTROL 电子邮件地址]** 或 **[!UICONTROL 域地址]**.

1. 输入要从发送中排除的电子邮件地址或域。

   >[!NOTE]
   >
   >请确保输入有效的电子邮件地址(如abc@company.com)或域名（如abc.company.com）。

1. 根据需要指定原因。

   >[!NOTE]
   >
   >此字段中允许包含32到126之间的所有ASCII可打印字符。 完整列表可在 [本页](https://en.wikipedia.org/wiki/Wikipedia:ASCII#ASCII_printable_characters){target="_blank"} 例如。

1. 单击 **[!UICONTROL 提交]** 确认。

### 上传CSV文件 {#upload-csv-file}

1. 选择 **[!UICONTROL 上传CSV]** 选项。

1. 下载要使用的CSV模板，该模板包括以下列和格式：

   ```
   TYPE,VALUE,COMMENT
   EMAIL,abc@somedomain.com,Comment
   DOMAIN,somedomain.com,Comment
   ```
   >[!CAUTION]
   >
   >请勿更改CSV模板中列的名称。
   >
   >文件大小不应超过1 MB。

1. 在CSV模板中填写要添加到禁止列表的电子邮件地址和/或域。

   >[!NOTE]
   >
   >在 **注释** 列。 完整列表可在 [本页](https://en.wikipedia.org/wiki/Wikipedia:ASCII#ASCII_printable_characters){target="_blank"} 例如。

1. 完成后，拖放CSV文件，然后单击 **[!UICONTROL 提交]** 确认。

>[!NOTE]
>
>上传完成后，请通过界面检查其状态，确保上传成功。 [了解如何](#recent-uploads)

### 检查最近上载状态 {#recent-uploads}

单击 **[!UICONTROL 最近上传]** 按钮来检查您上传的最新CSV文件的状态。

可能的状态包括：

* **[!UICONTROL 待定]**:正在处理文件上传。
* **[!UICONTROL 错误]**:由于技术问题或文件格式错误，文件上传过程失败。
* **[!UICONTROL 完成]**:文件上传过程已成功完成。

在上传期间，如果某些地址的格式不正确，则它们不会添加到全局禁止列表中。

在这种情况下，上传完成后，它将与报表关联。 您可以下载它以检查遇到的错误。

## 删除地址

要从全局抑制列表中删除地址，请使用 **[!UICONTROL 删除]** 按钮。

>[!CAUTION]
>
>顾问无法通过界面删除由第三方服务提供商Blackbox自动添加的地址或域。 此操作只能通过后端票证完成。

