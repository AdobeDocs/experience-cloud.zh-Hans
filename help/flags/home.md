---
title: 标志
description: 了解如何使用Adobe Target中的标记通过受控转出、功能标记和针对性受众管理安全而渐进地交付功能。
hide: true
index: false
exl-id: c400d75d-d928-4cf6-a094-1a2f443389f0
source-git-commit: 8a3a8f0293e32db896f62a63ea6a886868ffe1a3
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 1%

---

# 标志 {#experience-rollouts-home}

>[!AVAILABILITY]
>
>标记当前位于Beta中，可供Adobe Target客户使用。 请联系您的Adobe代表以请求获取访问权限。

Adobe Target中的标记使产品团队能够逐步、安全地交付新功能，而无需重新部署或停机。 您可以定义谁能看到什么、何时看到以及以什么速度看到。 如果出现错误，您会立即关闭该功能。 如果一切顺利，您就可以按照计划扩大受众。

## 您可以做什么

**查看新功能的控件。** Target将版本发布到特定用户、组织、区域或自定义属性。 从一小部分开始，验证体验，然后展开 — 全部从控制台中展开，无需更改代码。

**运行A/B试验。** 为不同的受众区段提供不同的变体，并测量表现更好的效果。 在完整版本发布之前，使用结果做出明智的产品决策。

**降低发布风险。** 将大型更改分解为较小的可控转出。 如果出现错误或性能问题，请仅禁用受影响的功能 — 应用程序的其余部分将保持稳定。

**跨应用程序协调。** 功能组允许您同时管理多个功能标记，从而跨应用程序共享通用的转出受众。

**导出您的数据。** 将标记数据导出到首选报表环境，以便与其他Adobe数据一起进行分析和测量。

## 载入您的第一个标志

从标记中获取值首先需要三个步骤：

1. **通过Adobe Target访问标志** — 标志在Adobe Target中可用。 从Target界面中[请求访问](guides/console/request-access.md)并打开标志。

1. **创建并发布标志** — 按照[创建您的第一个功能标志](guides/feature-flags/create-your-first-feature-flag.md)指南来定义标志、设置初始受众并将其发布到环境。

1. **与您的应用程序集成** — 使用AEP Web SDK或AEP Mobile SDK连接您的应用程序，以便它能够在运行时检索并应用标志。 从应用程序类型的[集成步骤](guides/integrate/integration-steps.md)开始。

一旦您的第一个标志启用，您就可以优化其受众、配置逐步转出，并将其从保存提升为完全转出。

## 需要帮助？

如果某些组件的行为与预期不符，请联系您的Adobe代表寻求支持。

<!-- 
Bob was here. Again.
-->
