---
title: 使用Adobe Experience Cloud调试器切换启动环境
description: 了解如何使用Experience Cloud调试器加载不同的启动嵌入代码。 本课程是在包含Launch教程的网站中实施Experience cloud的一部分。
seo-description: null
seo-title: 使用Adobe Experience Cloud调试器切换启动环境
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: 79d5274d09d66b80a49aba5db3e0a997d0f0ff61

---


# 使用Experience Cloud调试器切换启动环境

In this lesson you will use the [Adobe Experience Cloud Debugger extension](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) to replace the Launch property hardcoded on the [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html) with your own property.

此技术称为环境切换，在您以后在自己的网站上使用Launch时会很有帮助。 您可以在浏览器中加载生产网站，但可以在开发 *Launch环境中* 加载。 这使您能够放心地独立于常规代码版本进行和验证Launch更改。  毕竟，将营销标签版本与常规代码版本分开是客户最初使用Launch的主要原因之一！

## 学习目标

在本课程结束后，您将能够：

* 使用调试器加载替代的启动环境
* 使用调试器验证是否已加载替代的启动环境

## 获取开发环境的URL

1. In your Launch property, open the `Environments` page

1. In the **[!UICONTROL Development]** row, click the Install icon ![Install icon](images/launch-installIcon.png) to open the modal

1. 单击复制图标 ![复制图标](images/launch-copyIcon.png) ，将嵌入代码复制到剪贴板

1. Click **[!UICONTROL Close]** to close the modal

   ![安装图标](images/launch-copyInstallCode.png)

## 替换Luma演示站点上的启动项URL

1. Open the [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html) in your Chrome browser

1. 单击“调 [试器图标”图标](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) ，打开 ![Experience Cloud调试器扩展](images/icon-debugger.png)

   ![单击“调试器”图标](images/switchEnvironments-openDebugger.png)

1. 请注意，“摘要”选项卡上显示了当前实施的启动项属性

   ![调试器中显示的启动环境](images/switchEnvironments-debuggerOnWeRetail-prod.png)

1. 转到“工具”选项卡

1. 滚动到替换启动 **[!UICONTROL 嵌入代码部分]**

1. 确保具有Luma站点的Chrome选项卡位于调试器后面（而非本教程中的选项卡或具有启动界面的选项卡）。  将剪贴板中的嵌入代码粘贴到输入字段中

1. 打开“跨luma.enablementadobe.com应用”功能，以便Luma站点上的所有页面都将映射到您的“启动”属性

1. 单击“保 **[!UICONTROL 存]** ”按钮

   ![调试器中显示的启动环境](images/switchEnvironments-debugger-save.png)

1. 重新加载Luma站点并检查调试器的“摘要”选项卡。 在“启动项”部分下，您现在应会看到正在使用您的开发属性。 确认该属性的名称与您的名称匹配，并且该环境显示“development”。

   ![调试器中显示的启动环境](images/switchEnvironments-debuggerOnWeRetail.png)

>[!NOTE] 每当您返回Luma站点时，调试器将保存此配置并替换启动嵌入代码。 它不会影响您在其他打开的选项卡中访问的其他站点。 To stop the Debugger from replacing the embed code, click the **[!UICONTROL Remove]** button next to the embed code in the Tools tab of the Debugger.

在继续教程时，您将使用此技术将Luma站点映射到您自己的Launch属性，以验证您的Launch实施。 在生产网站上开始使用Launch时，您可以使用同一技术验证更改。

[下一个“添加Adobe Experience Platform Identity Service”&gt;](id-service.md)