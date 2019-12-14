---
title: 通过Adobe Experience Platform Launch在网站中实施Adobe Experience Cloud
description: 在包含Launch的网站中实施Experience cloud是前端开发人员或技术营销人员的理想起点，他们希望了解如何在其网站上实施Adobe Experience cloud解决方案。
seo-description: null
seo-title: 通过Adobe Experience Platform Launch在网站中实施Adobe Experience Cloud
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: 7166d2933cc99bcbbd4713fba8f87fb0826b711e

---


# 概述

_在包含Launch的网站中实施Experience Cloud_ ，是前端开发人员或技术营销人员的理想起点，他们希望了解如何在其网站上实施Adobe Experience cloud解决方案。

每个课程都包含操作方法练习和基本信息，帮助您实施Experience Cloud并了解其价值。  我们提供了标注，以突出显示可能对从我们旧版标签管理器动态标签管理迁移的客户有用的信息。 我们为您提供了演示网站来完成教程，这样您就可以在安全的环境中学习基础技术。完成本教程后，您应该可以开始在自己的网站上通过Launch实施所有营销解决方案。

完成此操作后，您将能够：

* 创建启动项属性

* 在网站上安装启动属性

* 添加以下Adobe Experience cloud解决方案：
   * **[Adobe Experience Platform Identity Service](id-service.md)**
   * **[Adobe Target](target.md)**
   * **[Adobe Analytics](analytics.md)**
   * **[Adobe Audience Manager](audience-manager.md)**

* 创建规则和数据元素，将数据发送到Adobe解决方案

* 使用Adobe Experience Cloud Debugger验证实施

* 通过开发、暂存和生产环境发布Launch中的更改

>[!NOTE] 以下平台也提供类似的多解决方案教程：
>
> * [在Mobile iOS Swift™应用程序中实施Experience Cloud](/help/mobile-ios-swift-implementation/index.md)
* [在移动iOS Objective-C应用程序中实施Experience Cloud](/help/mobile-ios-objective-c-implementation/index.md)
* [在移动Android应用程序中实施Experience Cloud](/help/mobile-android-implementation/index.md)


## 先决条件

在这些课程中，假定您拥有Adobe ID和完成练习所需的权限。 否则，您可能需要联系您的Experience cloud管理员以请求访问权限。

* 对于Launch，您必须拥有“开发”、“批准”、“发布”、“管理扩展”和“管理环境”的权限。 For more information on Launch permissions, see [the documentation](https://docs.adobe.com/content/help/en/launch/using/reference/admin/user-permissions.html).
* 对于Adobe Analytics，您必须了解跟踪服务器以及要用于完成本教程的报表包
* 对于Audience Manager，您必须了解您的Audience Manager子域（也称为“合作伙伴名称”、“合作伙伴ID”或“合作伙伴子域”）

此外，我们还假定您熟悉 HTML 和 JavaScript 等前端开发语言。您无需精通这些语言也可完成课程，但如果您能够轻松阅读和理解代码，将可从这些课程中学到更多知识。

## 关于 Launch

Adobe Experience Platform Launch是Adobe提供的新一代网站标签和移动SDK管理功能。 Launch为客户提供了部署和管理支持相关客户体验所需的所有分析、营销和广告解决方案的简单方法。 Launch不收取任何额外费用。 它适用于任何Adobe Experience cloud客户。

Launch for websites允许您集中管理与桌面和移动站点上使用的分析、营销和广告解决方案相关的所有JavaScript。 例如，如果您部署Adobe Analytics,Launch将管理AppMeasurement javaScript库、填充变量和触发请求。

Launch容器标签比DTM轻60%，比Google Tag Manager轻40%。 容器的内容，包括您的自定义代码在内，都进行了压缩。所有一切都是模块化的。如果您不需要某个项目，则可以不将其纳入您的库中。这样，实施就会变得快速而紧凑。

Launch还是一个平台，它允许第三方供应商创建扩展，以便通过Launch轻松部署其解决方案。 扩展是扩展Launch UI和客户端功能的一个代码包（JavaScript、HTML和CSS）。 如果将 Launch 看作一种操作系统，那么扩展就是用来完成任务的应用程序。

## 关于课程

在这些课程中，您将将Adobe Experience Cloud实施到称为Luma的假零售网站中。 Luma站 [点具有丰富的数据层](https://luma.enablementadobe.com/content/luma/us/en.html) ，并具备丰富的功能，使您能够构建出一个真实的实施。 您将在您自己的Experience cloud组织中构建自己的Launch属性，并使用Experience cloud调试器将其映射到我们托管的Luma站点。

[![Luma网站](images/overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)

## 获取工具

1. Because you will be using some browser-specific extensions, we recommend completing the tutorial using the [Chrome Web Browser](https://www.google.com/chrome/)
1. Add the [Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) extension to your Chrome browser
1. Download the [sample html page](https://www.enablementadobe.com/multi/web/basic-sample.html) (right-click on this link and click "Save Link As")
1. 获取文本编辑器，在该编辑器中可以更改示例HTML页。 (如果您没有，我们建议您试用 [Brackets](http://brackets.io/))
1. 将Luma站点 [加入书签](https://luma.enablementadobe.com/content/luma/us/en.html)

>[!NOTE] 在Chrome中打开Luma站点时，您可能会发现完成本教程更简单，同时阅读本教程并在其他浏览器中完成启动界面步骤。

开始吧！

[下一个“创建启动项属性”&gt;](launch.md)