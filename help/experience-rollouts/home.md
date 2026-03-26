---
title: Adobe体验转出
description: 了解如何使用Adobe体验转出，通过受控转出、功能标记和目标受众管理，安全且逐步地交付功能。
exl-id: c400d75d-d928-4cf6-a094-1a2f443389f0
source-git-commit: 4a3133f014a9bb9d6ed26eb9d9f763db79ce63b3
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 1%

---

# Adobe体验转出 {#experience-rollouts-home}

Adobe Experience转出功能使产品团队能够逐步、安全地发布新功能，而无需重新部署或停机。 您可以定义谁能看到什么、何时看到以及以什么速度看到。 如果出现错误，您会立即关闭该功能。 如果一切顺利，您就可以按照计划扩大受众。

## 您可以做什么

**查看新功能的控件。** Target将版本发布到特定用户、组织、区域或自定义属性。 从一小部分开始，验证体验，然后展开 — 全部从控制台中展开，无需更改代码。

**运行A/B试验。** 为不同的受众区段提供不同的变体，并测量表现更好的效果。 在完整版本发布之前，使用结果做出明智的产品决策。

**降低发布风险。** 将大型更改分解为较小的可控转出。 如果出现错误或性能问题，请仅禁用受影响的功能 — 应用程序的其余部分将保持稳定。

**跨团队协调。** 跨团队功能组允许多个团队参与同一个协调的发布，每个团队管理自己的功能标记，同时共享共同的转出计划和受众。

## 载入您的第一个功能

从体验转出获取价值始于三个步骤：

1. **设置您的团队和应用程序** — [请求对控制台的访问权限](guides/console/request-access.md)，然后[载入您的应用程序](guides/applications/onboard-your-application.md)，以便Experience Rollout知道要提供哪些客户端。

2. **创建并发布功能标志** — 按照[创建您的第一个功能标志](guides/feature-flags/create-your-first-feature-flag.md)指南来定义标志、设置初始受众并将其发布到环境。

3. **与您的应用程序集成** — 将您的应用程序连接到Experience Rollout API或SDK，以便它能够在运行时检索并应用功能标志。 从应用程序类型的[集成步骤](guides/integrate/integration-steps.md)开始。

一旦您的第一个标志启用，您就可以优化其受众、配置逐步转出，并将其从保存提升为完全转出。

## 需要帮助？

如果某些问题的表现与预期不符，则[疑难解答指南](guides/support/troubleshooting.md)将涵盖最常见的问题。 任何其他信息，请[联系支持人员](guides/support/contact-support.md)。
