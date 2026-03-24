---
title: 跨环境查看功能标记
description: 了解如何在Adobe Experience转出中查看应用程序在所有链接环境中的功能标记状态。
source-git-commit: 5c99061a7f2aaaad98190166ea6fd79b7eb26dec
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 3%

---


# 跨环境查看功能标记 {#view-flags-across-environments}

跨环境链接应用程序实例后，体验转出会直接在功能标记列表页面中显示所有链接环境中的每个功能标记的状态。 这为您提供了单个视图来比较标记状态（例如，标记在暂存环境中是否为ON，在生产环境中是否为OFF），而无需切换环境。

## 先决条件 {#prerequisites}

在跨环境状态可见之前，必须跨环境链接您的应用程序实例。 有关设置说明，请参阅[将环境关联到应用程序](associate-environments.md)。

## 工作原理 {#how-it-works}

当您导航到&#x200B;**功能和版本>功能标志**&#x200B;并选择具有链接实例的应用程序时，列表页会显示每个链接环境的附加列。 每列都显示该环境中功能标志的当前状态。

功能标志通过其&#x200B;**key**&#x200B;在各个环境中匹配，而不是通过它们的名称匹配。 这意味着：

* 只要键相同，标记在每个环境中都可以有不同的显示名称。
* 每个环境列中显示的名称是该环境中使用的名称。

## 用例 {#use-case}

典型的工作流是在较低层环境（例如，暂存）中开发和测试功能标记，然后验证其状态，然后再将配置提升至生产环境。 通过跨环境可见性，可在将标志导入生产环境之前，先确认已在暂存中正确配置了标记 — 所有这些操作都可从生产控制台中完成。

## 另请参阅 {#see-also}

* [将环境与应用程序关联](associate-environments.md)
* [导入功能标志](import-feature-flags.md)
* [跨环境概念](cross-environment-concept.md)
