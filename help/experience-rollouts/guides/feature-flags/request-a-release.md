---
title: 请求发布
description: 了解如何在Adobe Experience转出中请求新的协调版本，以及要提供哪些信息。
source-git-commit: d311efb995b20ffc17370d68d57dd84a8605896c
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 2%

---


# 请求发布 {#request-a-release}

## 先决条件 {#prerequisites}

* 您具有&#x200B;**版本管理器**&#x200B;角色 — 请参阅[用户角色](../teams/user-roles.md)
* 您的应用程序已载入 — 请参阅[将应用程序载入](../applications/onboard-your-application.md)

>[!TIP]
>
>在请求版本之前，请查看[版本和跨团队功能组](releases-and-cross-team-feature-groups.md)。 跨团队功能组能够以更少的开销满足您的需求 — 它是自助式的，支持更丰富的受众定位。

## 提交支持请求 {#submit}

版本创建不是自助式的。 联系Experience Rollout支持人员以请求新版本。 提供以下信息：

| 字段 | 描述 |
|---|---|
| **名称** | 版本的唯一名称。 发行版本名称中不要包含空格。 |
| **团队** | 将拥有此版本的团队。 |
| **环境** | 应在其中创建版本的环境（暂存或生产）。 |
| **目标** | 此版本将推出哪些功能及推出原因的简要说明。 |
| **应用程序** | 要包含在发行版中的一个或多个应用程序。 |
| **持续时间** | 需要发布多长时间才能保持活动状态。 预计将在三个月内关闭或批准发行。 如果您需要更长的时间，请提供业务理由。 |

>[!NOTE]
>
>任何给定时间的活动发行版本数都是有限的。 计划在三个月内审核或关闭您的发布以释放其他团队的容量。

## 创建版本后 {#after}

收到已创建版本的确认后，登录到控制台并完成版本配置。 有关完整步骤序列，请参阅[发布端对端工作流程](release-workflow-end-to-end.md)。

## 另请参阅 {#see-also}

* [端到端发布工作流](release-workflow-end-to-end.md)
* [更新版本受众规则](update-release-audience-rules.md)
* [发行状态](release-states.md)
