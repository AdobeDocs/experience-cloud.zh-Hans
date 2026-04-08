---
title: 载入您的应用程序
description: 了解如何在Adobe Experience转出中载入新应用程序，以便开始创建和管理功能标记。
exl-id: d88c27a5-f490-4504-9764-5e4ce98fdf20
source-git-commit: fcb1d36fc92b3954a902d818a98f579672c577e9
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 2%

---

# 载入您的应用程序 {#onboard-your-application}

您必须具有&#x200B;**管理员**&#x200B;角色才能添加新应用程序。 如果需要验证或更新您的角色，请联系您的管理员。

## 添加新应用程序 {#add-application}

1. 登录到“体验转出”控制台，然后导航到&#x200B;**体验转出>应用程序**。

   >[!NOTE]
   >
   >如果&#x200B;**新建应用程序**&#x200B;按钮不可见，请验证您是否具有&#x200B;**Floodgate管理员**&#x200B;角色。

2. 选择&#x200B;**新建应用程序**。

3. 选择与您的应用程序类型（Web或移动设备）匹配的&#x200B;**平台**。

4. 提供以下信息：

   | 字段 | 描述 |
   |---|---|
   | **应用程序ID** | 从代码调用体验转出时使用的唯一标识符。 使用应用程序的客户端ID。 |
   | **TTL** | 刷新每个应用程序缓存的轮询间隔（秒）。 仅适用于服务器端SDK。 |

5. 选择&#x200B;**添加**。 您的应用程序现在已注册，可以配置功能标记。

## 后续内容 {#next-steps}

在应用程序上线后，您可以开始创建功能标记：

* [创建您的第一个功能标记](../feature-flags/create-your-first-feature-flag.md)
* [在应用程序中集成体验转出](../integrate/integrating-in-your-app.md)

## 另请参阅 {#see-also}

* [管理应用程序](manage-applications.md)
* [登录到控制台](../console/log-in-to-the-console.md)
