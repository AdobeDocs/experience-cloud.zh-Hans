---
title: 创建功能组
description: 了解如何在Adobe Experience转出中创建功能组，以便作为一个单元管理团队中跨应用程序的多个功能标记。
source-git-commit: 9bfe0e55e89c1d7fbd77cde63831a6a186820e24
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# 创建功能组 {#create-feature-group}

## 先决条件 {#prerequisites}

在创建特征组之前，请完成以下操作：

* 您有权访问体验转出控制台 — 请参阅[登录到控制台](../console/log-in-to-the-console.md)
* 您属于一个团队 — 请参阅[管理团队](../teams/manage-teams.md)
* 您的应用程序已载入 — 请参阅[将应用程序载入](../applications/onboard-your-application.md)
* 您具有&#x200B;**开发人员**&#x200B;或&#x200B;**产品版本所有者**&#x200B;角色 — 请参阅[用户角色](../teams/user-roles.md)
* 您已创建要添加到组的功能标志 — 请参阅[创建您的第一个功能标志](create-your-first-feature-flag.md)

有关功能组的介绍，请参阅[控制多个功能的功能组](../../concepts/feature-groups-to-control-multiple-features.md)。

## 第1步：创建特征组 {#create}

打开控制台并启动新功能组：

1. 登录到“体验转出”控制台，然后导航到&#x200B;**功能测试>功能组**。
2. 选择&#x200B;**新建功能组**。

## 步骤2：基本详细信息 {#basic-details}

配置功能组的常规设置：

1. 提供标题、键、描述和（可选）标记。
2. 为功能组设置&#x200B;**百分比转出**。
3. 如果要运行A/B测试，请选择多个变体。 否则，将其保留在一个变体中。 有关详细信息，请参阅带有功能标志[&#128279;](a-b-testing.md)的A/B测试。

## 步骤3：受众 {#audience}

定义将接收此组中各项功能的人员：

1. 在&#x200B;**受众**&#x200B;选项卡上，添加受众条件以定义哪些用户接收该功能。
2. 在&#x200B;**应用程序**&#x200B;下，从您的团队添加一个或多个应用程序。 功能组可以跨多个应用程序，只要它们都属于同一个团队。

>[!NOTE]
>
>**开发人员**&#x200B;角色已沙盒。 在&#x200B;**受众>配置文件>用户ID**&#x200B;下添加您自己的用户ID以进行私下测试。 若要定位外部用户，您需要&#x200B;**产品版本所有者**&#x200B;角色。

## 步骤4：功能 {#features}

分配将由此组控制的功能标志：

1. 在&#x200B;**功能**&#x200B;选项卡下，您会看到每个选定应用程序的框。
2. 为每个应用程序添加功能标记。
3. 如果您选择了多个变体（用于A/B测试），则会看到每个变体的选项卡。 为每个添加相应的功能标记。

>[!IMPORTANT]
>
>功能标志只能通过一种方法提供 — 直接作为功能标志、通过功能组或通过发布。 当您将功能标记添加到功能组时，将删除对该标记设置的任何受众或百分比转出。 已分配给其他版本或功能组的功能标记将不会显示在列表中。

## 步骤5：计划（可选） {#schedule}

您可以安排在将来的日期和时间激活功能组。 有关详细信息，请参阅[计划](schedule.md)。

## 另请参阅 {#see-also}

* [设置功能组以逐步推出](set-feature-group-gradual-rollout.md)
* [使用功能标记进行A/B测试](a-b-testing.md)
* [用于控制多个特征的特征组](../../concepts/feature-groups-to-control-multiple-features.md)
