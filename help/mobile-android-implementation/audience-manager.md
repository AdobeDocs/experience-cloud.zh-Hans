---
title: 通过Launch实施Adobe Audience Manager
description: 了解如何使用服务器端转发和启动在您的网站上实施Adobe Audience Manager。 本课程是在Mobile android应用程序中实施Experience cloud教程的一部分。
seo-description: null
seo-title: 通过Launch实施Adobe Audience Manager
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: e9dee6d0aa3b775d0ce617e2b2c57b56de491b8d

---


# 添加Adobe Audience Manager

本课将指导您逐步使用服务器端转发将Adobe Audience Manager实施到Experience Platform Mobile SDK中。

[Adobe Audience Manager](https://docs.adobe.com/content/help/en/audience-manager/user-guide/aam-home.html) (AAM)为在线受众数据管理提供行业领先的服务，为数字广告商和出版商提供控制和利用其数据资产来帮助推动销售成功所需的工具。

## 学习目标

在本课程结束后，您将能够：

1. 描述在移动应用程序中实施Audience Manager的两种主要方法
1. 使用分析信标的服务器端转发添加Audience Manager
1. 验证Audience manager实施

## 先决条件

要完成本课程，您需要：

1. 要完成“配置启动项”部分下的课程，即“创建启动项属性 [”、“添加扩展”](launch-create-a-property.md)、“创建库 [”和“](launch-add-extensions.md)[](launch-create-a-library.md)[](launch-install-the-mobile-sdk.md)安装移动SDK”部分。

1. 管理员对Adobe Analytics的访问权限，以便您能够为本教程中使用的报表包启用服务器端转发。 或者，也可以按照下面的说明，请求贵组织的现有管理员为您执行此操作。

## 实施选项

在应用程序中实施Audience Manager有两种方法：

* 服务器端转发(SSF)-对于使用Adobe Analytics的客户，这是最简单、推荐的实施方式。 Adobe Analytics将数据转发到Adobe后端的AAM，这样您就不必直接从应用程序向Audience manager发出请求。 这还支持关键集成功能，并符合Audience manager代码实施和部署的最佳实践。

* 客户端DIL —— 此方法适用于没有Adobe Analytics的客户。 应用程序中的Audience manager方法将数据直接发送到Audience Manager。 在这种情况下，在设置移动Launch属性时，您应在Launch中使用Audience Manager扩展。

当您之前在本教程的“添加扩展”部分中设置 [Analytics扩展时](launch-add-extensions.md) ，您选中了该框以启动从Analytics向Audience Manager传输数据的服务器端转发。 这将动态插入处理Audience manager区段响应所需的代码，并将其重新插入您的应用程序。 我们不会在本教程中添加Audience Manager扩展，因为同样，这仅用于您没有Adobe Analytics的用例。

## 启用服务器端转发

实现SSF主要有三个步骤：

1. 将Experience Cloud Mobile SDK和Analytics扩展添加到应用程序中，*您&#x200B;**已在配置启动课程中完成** 。
1. 在Analytics扩展配置中启用Audience Manager Forwarding，您 ***在添加扩展课程中*** ，只需选中一个框 [](launch-add-extensions.md) 即可完成此操作。
1. 在Analytics Admin Console中打开“切换”，将数据从Analytics转发到每个报告包的Audience Manager **，我们将在本课的其余部分中查看该功能。

### 在 Analytics Admin Console 中启用服务器端转发

需要在Adobe Analytics Admin Console中配置，才能开始将数据从Adobe Analytics转发到Adobe Audience Manager。 请注意，系统最多可能需要四小时才能开始转发数据，因此，在排除转发故障时请牢记这一点。

#### 在Analytics Admin Console中启用SSF

1. 通过Experience Cloud UI登录Analytics。 如果您没有Analytics的管理员访问权限，则需要与Experience cloud或Analytics管理员交谈，为您分配访问权限或完成这些步骤。

   ![登录Adobe Analytics UI](images/mobile-aam-logIntoAnalytics.png)

1. 从Analytics的顶部导航中，选择 **[!UICONTROL Admin &gt; Report Suites]**，然后从列表中选择（或多选）要转发到Audience Manager的报表包。

   ![单击到Admin Console](images/mobile-aam-analyticsAdminConsoleReportSuites.png)

1. 从“报表包”屏幕中，在选择报表包的情况下，选择“编辑设置”&gt;“ **[!UICONTROL 常规”&gt;“服务器端转发”]**。

   ![选择SSF菜单](images/mobile-aam-selectSSFmenu.png)

   >[!WARNING]  如上所述，您需要拥有管理员权限，才能查看此菜单项。

1. 在“服务器端转发”页面上，阅读信息并选中该框以为报表包启 **[!UICONTROL 用服务器端转发]** 。

1. Click **[!UICONTROL Save]**

   ![完成SSF设置](images/mobile-aam-enableSSFcomplete.png)

>[!NOTE] 由于每个报表包都需要启用SSF，因此，在实际应用程序的报表包中部署SSF时，请不要忘记为实际报表包重复此步骤。
>
>此外，如果SSF选项灰显，您需要“将报表包映射到您的Experience Cloud组织”，以启用此选项。 [此文档](https://docs.adobe.com/content/help/en/core-services/interface/about-core-services/report-suite-mapping.html)对此进行了说明。

只要您实施了Adobe Experience Platform Identity Service，此交换机就会开始将数据实际转发到AAM。 其余的SSF实现都发生在代码中，当您选中Analytics扩展中的框以转发到AAM时，该代码在Launch中处理。

服务器端转发代码现已为您的应用程序实现！

[下一个“发布您的属性”&gt;](publish.md)