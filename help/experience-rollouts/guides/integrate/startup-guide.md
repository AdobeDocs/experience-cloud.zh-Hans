---
title: 启动指南
description: 按照以下步骤将您的应用程序与Adobe体验转出集成，从请求访问权限到创建第一个功能标记。
exl-id: 7aa09535-45fa-4ddf-9e3f-a23f8a8ee666
source-git-commit: 2a946868f58e25f8aafbf3ccfcf6571e7d0d8d20
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 1%

---

# 启动指南 {#startup-guide}

请按照以下步骤将体验转出集成到您的应用程序中。

## 步骤1：请求访问 {#step-1-access}

请求访问体验转出控制台并加入您的团队。 有关分步说明，请参阅[请求访问权限](../console/request-access.md)。

## 步骤2：载入应用程序 {#step-2-onboard}

获得访问权限后，请登录到Experience Rollout控制台，并验证您的应用程序是否列在您的团队下。 如果不是，请让您的团队管理员添加它。 请参阅[将应用程序载入](../applications/onboard-your-application.md)。

在上线之前，请准备以下内容：

| 要求 | 详细信息 |
|---|---|
| **应用程序ID** | 调用体验转出API时使用的唯一客户端标识符。 在可用的情况下，使用应用程序的现有客户端ID。 |
| **服务器端客户端** | 如果与服务器端SDK集成，则需要具有适当权限的管理客户端ID。 |
| **桌面客户端** | 可以使用产品代码和产品版本代替客户端ID。 |

## 步骤3：获取您的凭据 {#step-3-credentials}

如果您通过服务器端SDK集成，则需要服务令牌客户端ID。 在从SDK进行API调用之前，请与Experience Rollout支持人员联系以列入允许列表您的客户端ID。

## 步骤4：使用SDK集成 {#step-4-integrate}

对您的应用程序类型执行[集成步骤](integration-steps.md)。 选择适合您的栈栈的路径：

* **Web服务** → Java SDK或Node.js SDK
* **Web和移动应用** → Web SDK或移动SDK（即将推出）
* **桌面应用程序** → SDK（即将推出）

## 步骤5：创建和测试您的第一个功能标记 {#step-5-feature-flag}

集成完成后，在控制台中创建第一个功能标记并进行测试：

* [创建您的第一个功能标记](../feature-flags/create-your-first-feature-flag.md)

## 另请参阅 {#see-also}

* [在应用程序中集成体验转出](integrating-in-your-app.md)
* [集成步骤](integration-steps.md)
* [SDK](sdks.md)
