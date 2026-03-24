---
title: 什么是功能标记
description: 了解功能标志是什么，以及它们如何让您在运行时打开或关闭应用程序功能，而无需重新部署。
source-git-commit: 1c8fd9b42d08f657b4e6b16efae86faa04d15565
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# 什么是功能标记 {#what-is-a-feature-flag}

功能标志是一种机制，它允许您在运行时打开或关闭应用程序的功能，而无需重新部署代码。

功能标记将&#x200B;**代码部署**&#x200B;与&#x200B;**功能可用性**&#x200B;分离。 您可以将隐藏在标志后的功能作为新代码发送到生产环境，然后在准备就绪时打开该功能 — 适用于所有用户或针对某个目标子集。

这种分离可显着降低风险。 开发人员能够以最少的中断持续构建和交付，而产品团队可以完全控制功能何时以及向谁可见。

>[!NOTE]
>
>在体验转出中，功能标志是功能控制中最原子化的单位。 可以单独使用它来定位单个功能，或与[功能组](feature-groups-to-control-multiple-features.md)或[版本](release-management.md)中的其他标记组合。
