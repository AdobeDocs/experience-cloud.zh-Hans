---
title: 载入您的应用程序
description: 了解如何在Adobe Experience转出中载入新应用程序，以便您的团队可以开始创建和管理功能标记。
source-git-commit: 9bfe0e55e89c1d7fbd77cde63831a6a186820e24
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 1%

---


# 载入您的应用程序 {#onboard-your-application}

您必须具有&#x200B;**管理员**&#x200B;角色才能添加新应用程序。 如果需要验证您的角色或向团队管理员请求该角色，请查看[用户角色](../teams/user-roles.md)。

## 添加新应用程序 {#add-application}

1. 登录到“体验转出”控制台，然后导航到&#x200B;**管理员>应用程序**。

   >[!NOTE]
   >
   >如果&#x200B;**新建应用程序**&#x200B;按钮不可见，请验证您是否属于正确的团队，以及您是否具有&#x200B;**管理员**&#x200B;角色。

2. 选择&#x200B;**新建应用程序**。

3. 选择与您的应用程序类型（Web、移动设备、桌面或服务）匹配的&#x200B;**渠道**。

4. 提供以下信息：

   | 字段 | 描述 |
   |---|---|
   | **应用程序ID** | 从代码调用体验转出时使用的唯一标识符。 使用应用程序的客户端ID。 |
   | **TTL** | 刷新每个应用程序缓存的轮询间隔（秒）。 仅适用于服务器端SDK。 |
   | **团队** | 将拥有和管理此应用程序的团队。 只有此团队的成员才能为其创建和编辑功能标记。 |

5. 选择&#x200B;**添加**。 您的应用程序现在已注册，可以配置功能标记。

## 后续内容 {#next-steps}

应用程序上线后，您的团队可以开始创建功能标记：

* [创建您的第一个功能标记](../feature-flags/create-your-first-feature-flag.md)
* [在应用程序中集成体验转出](../integrate/integrating-in-your-app.md)

## 另请参阅 {#see-also}

* [管理应用程序](manage-applications.md)
* [用户角色](../teams/user-roles.md)
* [登录到控制台](../console/log-in-to-the-console.md)
