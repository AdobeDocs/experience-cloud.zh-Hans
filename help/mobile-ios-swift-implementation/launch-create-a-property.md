---
title: 为移动应用程序创建启动属性
description: 了解如何登录Launch界面并创建移动Launch属性。 本课程是在Mobile iOS Swift应用程序中实施Experience cloud教程的一部分。
seo-description: null
seo-title: 为移动应用程序创建启动属性
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: 7166d2933cc99bcbbd4713fba8f87fb0826b711e

---


# 创建启动项属性

Adobe Experience Platform Launch是新一代移动SDK和网站标签管理功能。 Launch为客户提供了部署和管理支持相关客户体验所需的所有分析、营销和广告解决方案的简单方法。 Launch不收取任何额外费用。 它可供任何Adobe Experience cloud客户使用。

在本课中，您将为移动应用程序创建一个Launch属性。

## 先决条件

要完成接下来的几个课程，您必须拥有在Launch中开发、批准、发布、管理扩展和管理环境的权限。 如果由于用户界面选项不可用而无法完成上述任何步骤，请联系您的Experience cloud管理员以请求访问权限。 For more information on Launch permissions, see [the documentation](https://docs.adobe.com/content/help/en/launch/using/reference/admin/user-permissions.html).

## 学习目标

在本课程结束后，您将能够：

* 登录Launch用户界面
* 创建新的Launch移动属性
* 配置启动项移动属性

## 转到 Launch

**要开始使用Launch**

1. 登录 [Adobe Experience Cloud](https://experiencecloud.adobe.com)

1. 单击“解决方 ![案切换器”图标](images/mobile-launch-solutionSwitcher.png) ，打开解决方案切换器

1. Select **[!UICONTROL Launch]** from the menu

   ![使用图标打开解决方案切换器，然后单击激活](images/mobile-launch-solutionSwitcherActivation.png)

1. 在 **[!UICONTROL Adobe Experience Cloud Launch下]**，单击“转 **[!UICONTROL 到启动”按钮]**

   ![单击“启动”按钮](images/mobile-launch-goToLaunch.png)

You should now see the `Properties` screen (if no properties have ever been created in the account, this screen might be empty):

![属性屏幕](images/mobile-launch-propertiesScreen.png)

如果您经常使用Launch，您还可以将以下URL加入书签并直接登录 [https://launch.adobe.com](https://launch.adobe.com)

## 创建资产

属性基本上是一个容器，在您向应用程序部署标记时，您会用扩展、规则、数据元素和库填充该容器。 单个移动属性可跨多个应用程序平台（例如iOS和Android）使用，前提是应用程序包含类似的功能并需要实施相同的解决方案。  有关创建属性的详细信息，请参 [阅产品文档中的](https://aep-sdks.gitbook.io/docs/getting-started/create-a-mobile-property) “设置移动属性”。

**创建属性**

1. 单击“新 **[!UICONTROL 建属性]** ”按钮：

   ![单击“新建属性”](images/mobile-launch-addNewProperty.png)

1. 命名您的属性(例如， `Mobile Tutorial`)
1. 作为平台，单击 **[!UICONTROL Mobile]**
1. 单击“保 **[!UICONTROL 存]** ”按钮

   ![创建新属性](images/mobile-launch-newProperty.png)

您的新属性应显示在“属性”页面上。 Note that if you check the box next to the property name, options to **[!UICONTROL Configure]** or **[!UICONTROL Delete]** the property appear above the property list. 单击您的属性的名称(例如， `Mobile Tutorial`)打开屏 `Overview` 幕。
![单击属性的名称以将其打开](images/mobile-launch-openProperty.png)

[下一个“添加扩展”&gt;](launch-add-extensions.md)
