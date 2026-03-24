---
title: 版本管理常见问题解答
description: 在Adobe体验转出中查找有关版本管理的常见问题解答。
source-git-commit: d311efb995b20ffc17370d68d57dd84a8605896c
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 1%

---


# 版本管理常见问题解答 {#release-management-faqs}

## 如何请求发布？ {#request-release}

请参阅[请求版本](request-a-release.md)，以了解完整流程和您需要提供的信息。

## 版本支持哪些受众标准？ {#audience-criteria}

版本支持以下受众规则：

* ID类型（帐户类型）
* 国家/地区
* 用户ID (GUID)
* 电子邮件地址（个人或批量列表）
* 电子邮件域
* 客户端IP
* 百分比（所有用户）
* 百分比（仅限经过身份验证的用户）

您可以使用AND/OR逻辑（包括嵌套条件）组合多个规则。 有关分步配置说明，请参阅[更新版本受众规则](update-release-audience-rules.md)。

## 如何将应用程序添加到版本中？ {#onboard-application}

创建版本后，在控制台中打开该版本，并将您的应用程序添加到版本配置。 然后，每个应用程序的产品发行版所有者可以添加相关的功能标记。 有关完整序列，请参阅[端到端发布工作流](release-workflow-end-to-end.md)。

## 对于应符合条件的用户，将不会返回功能。 如何排除故障？ {#troubleshoot}

请按照以下步骤进行调试：

1. **检查发行状态。** 发行版本必须处于&#x200B;**已发布**&#x200B;或&#x200B;**完全转出**&#x200B;状态才能提供功能。 请参阅[发行状态](release-states.md)。
2. **检查应用程序和功能标志。** 验证是否为正确的应用程序创建了功能标志，以及应用程序是否与正确的版本相关联。
3. **检查功能标志是否已启用。** 即使版本处于活动状态，也不会提供禁用的标记。
4. **查看受众条件。** 确认用户符合受众规则中定义的所有条件。 双击与功能关联的特定版本的标准。

## 另请参阅 {#see-also}

* [请求发布](request-a-release.md)
* [更新版本受众规则](update-release-audience-rules.md)
* [发行状态](release-states.md)
* [端到端发布工作流](release-workflow-end-to-end.md)
