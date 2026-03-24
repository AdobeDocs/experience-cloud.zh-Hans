---
title: 订阅Adobe Developer Console中的API应用程序
description: 了解如何通过Adobe Developer Console将您的应用程序订阅到Experience Rollout API，以便您可以调用功能标记端点。
source-git-commit: 120a2ea34682c878aaf6f6cb75504a8704d10e3d
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 3%

---


# 订阅Adobe Developer Console中的API应用程序 {#subscribe-to-api}

若要从应用程序调用Experience Rollouts API，您需要通过[Adobe Developer Console](https://developer.adobe.com/console)订阅它。 这可为您的应用程序提供一个客户端ID，Experience Rollout可使用该客户端ID来标识调用方。

## 先决条件 {#prerequisites}

在订阅之前，请确认以下内容：

* 您的应用程序已载入体验转出控制台 — 请参阅[载入您的应用程序](../applications/onboard-your-application.md)
* 您有权访问组织的Adobe Developer Console

## 订阅体验转出API {#subscribe}

要将应用程序订阅到Experience Rollout API，请执行以下步骤：

1. 转到[Adobe Developer Console](https://developer.adobe.com/console)并使用您的组织凭据登录。
2. 选择您的项目，或创建一个新项目。
3. 选择&#x200B;**添加API**。
4. 搜索并选择&#x200B;**体验转出API**。
5. 按照提示配置API并生成凭据。
6. 请注意为您的项目生成的&#x200B;**客户端ID**。 这是您在调用体验转出API时以及在“体验转出”控制台中载入应用程序时使用的标识符。

## 服务器端SDK集成 {#server-sdk}

如果您使用Java SDK或Node.js SDK进行集成，则除了API密钥之外，您还需要一个&#x200B;**服务令牌**&#x200B;客户端ID。 服务令牌允许SDK在后台调用Experience Rollout API。

>[!NOTE]
>
>服务器端SDK客户端ID必须先由Experience Rollout支持部门列入允许列表，然后才能进行API调用。 完成Developer Console设置后，请联系支持人员。

## 另请参阅 {#see-also}

* [启动指南](startup-guide.md)
* [SDK](sdks.md)
* [载入您的应用程序](../applications/onboard-your-application.md)
* [集成步骤](integration-steps.md)
