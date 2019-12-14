---
title: 通过Launch实施Adobe Audience Manager
description: 了解如何使用服务器端转发和启动在您的网站上实施Adobe Audience Manager。 本课程是在Mobile iOS Swift应用程序中实施Experience cloud教程的一部分。
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

如果您尚未实施Audience Manager，请按照以下说明获取 [您的Audience Manager子域](https://docs.adobe.com/content/help/en/audience-manager-learn/tutorials/web-implementation/how-to-identify-your-partner-id-or-subdomain.html)。

## 实施选项

在应用程序中实施Audience Manager有两种方法：

* 服务器端转发(SSF)-对于使用Adobe Analytics的客户，这是最简单、推荐的实施方式。 Adobe Analytics将数据转发到Adobe后端的AAM，这样您就不必直接从应用程序向Audience manager发出请求。 这还支持关键集成功能，并符合Audience manager代码实施和部署的最佳实践。

* 客户端DIL —— 此方法适用于没有Adobe Analytics的客户。 应用程序中的Audience manager方法将数据直接发送到Audience Manager。 在这种情况下，在设置移动Launch属性时，您应在Launch中使用Audience Manager扩展。

当您之前在本教程的“添加扩展”部分中设置 [Analytics扩展时](launch-add-extensions.md) ，您选中了该框以启动从Analytics向Audience Manager传输数据的服务器端转发。 这将动态插入处理Audience manager区段响应所需的代码，并将其重新插入您的应用程序。 我们不会在本教程中添加Audience Manager扩展，因为同样，这仅用于您没有Adobe Analytics的用例。

## 启用服务器端转发

执行SSF实施有两个主要步骤：

1. 在Analytics Admin Console中打开“切换”，将数据从Analytics转发到每个报告包 *的Audience Manager*。
1. 将SDK代码置于适当位置， **您只需选中Analytics扩展中的框** ，即可通过Launch将数据转发到AAM。

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

### 验证服务器端转发

验证服务器端转发是否已启动并正在运行的主要方法是查看对来自应用程序的任何Adobe Analytics点击的响应。

如果您不从Analytics向Audience Manager转发数据(SSF)，则Analytics信标（除2x2像素外）实际上没有响应。 但是，启用SSF后，您可以在Analytics请求和响应中验证某些项目，以告知您其工作正常。

由于Xcode控制台不显示对信标的响应，因此您应使用另一个确实显示响应的调试器／数据包嗅探器，例如Charles Proxy（我将在下面的屏幕截图中显示）。

1. 打开调试器并筛选 `b/ss`器，这将限制您看到的Adobe Analytics请求
1. 构建和运行前几个练习中的示例应用程序
1. 对于任何Analytics请求，请查看响应。 它应包含一 `dcs_region` 个参数、一 `uuid` 个参数，并应包含一个“stuff”对象。 此对象是AAM区段ID将发送回浏览器（对于用户所属的任何区段，在AAM中分配给cookie目标的区段）的位置。 如果您有“stuff”对象，SSF正在工作！

   ![AA响应——素材对象](images/mobile-aam-AAresponseCharles.png)

>[!WARNING] 谨防错误的“成功”—如果有反应，而一切似乎都在起作用，请 **确保** “物品”对象。 如果不这样做，您可能会在回复中看到一条消息，说“status”:“SUCCESS”。 尽管听起来很疯狂，但这实际上证明它 **不能正确** 工作。 如果您看到这一点，则表示您已完成Launch中转发到AAM的步骤，但Analytics Admin Console中的转发尚未完成。 在这种情况下，您需要验证是否已在Analytics Admin Console中启用SSF。 如果你有，而且还没有4小时，请耐心点。

![AA响应——错误成功](images/mobile-aam-unsuccessful-SSF.png)

[下一个“发布您的属性”&gt;](publish.md)