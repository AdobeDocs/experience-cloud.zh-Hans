---
title: 功能管理API概述
description: Experience Rollout管理API的概述，它允许您以编程方式创建、读取、更新和删除功能标记、功能组和版本。
source-git-commit: db719ba7b9db91aea818d8ef216a28fcedc6aa65
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# 功能管理API概述 {#feature-management-apis-overview}

体验转出管理API允许您以编程方式管理功能标记、功能组和版本。 需要自动化工作流或将体验转出集成到现有部署管道中的团队可以使用这些API，而不是控制台。

>[!NOTE]
>
>根据请求，允许使用服务令牌访问管理API。 联系体验转出支持并提供请求访问权限的业务理由。

## 可用的管理API {#available-apis}

以下管理API可供使用：

* [功能标记管理API](feature-flags-management-api.md) — 创建、读取、更新和删除应用程序的功能标记。
* [功能组管理API](feature-group-management-api.md) — 创建、读取、更新和删除功能组。
* [版本管理API](release-management-apis.md) — 创建和编辑跨团队功能组和版本。

## 常见要求 {#common-requirements}

所有管理API调用都需要以下项：

* 来自Adobe Developer Console的&#x200B;**API密钥** — 请参阅[订阅API应用程序](../guides/integrate/subscribe-to-api-application.md)。
* **IMS用户访问令牌**&#x200B;或&#x200B;**服务令牌**，在`Authorization`标头中作为`Bearer <token>`传递。
* `Content-Type: application/json`标头。

必须为暂存环境和生产环境单独配置API密钥和令牌。

## 帮助程序指南 {#helper-guides}

以下指南有助于构建正确的API负载：

* [获取应用程序的客户端ID](get-client-id.md) — 查找功能标志和功能组管理API所需的数字客户端ID。
* [获取所需的受众条件](get-audience-criteria.md) — 使用控制台和GET API生成正确的受众条件JSON结构。
* [管理修补程序API](management-patch-api.md) — 更新功能标志、功能组或跨团队功能组的单个字段，而不传递完整对象。

## 另请参阅 {#see-also}

* **GET功能API V3**&#x200B;和&#x200B;**GET功能API V2** — 有关完整参考，请参阅本指南的功能API部分。
* [订阅API应用程序](../guides/integrate/subscribe-to-api-application.md)
