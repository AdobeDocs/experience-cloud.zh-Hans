---
title: 发布启动项属性
description: 了解如何将Launch属性从开发环境发布到暂存和生产环境。 本课程是在包含Launch教程的网站中实施Experience cloud的一部分。
seo-description: null
seo-title: 发布启动项属性
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: aacd691c176da6ae5b247a19051de57289c128c5

---


# 发布启动项属性

现在，您已经在开发环境中实施了Adobe Experience cloud的一些关键解决方案，是时候学习发布工作流程了。

## 学习目标

在本课程结束后，您将能够：

1. 将开发库发布到暂存环境
1. 使用调试器将暂存库映射到生产网站
1. 将暂存库发布到生产环境

## 发布到暂存环境

既然您已在开发环境中创建并验证了库，现在该将其发布到暂存了。

1. Go to the **[!UICONTROL Publishing]** page

1. 打开库旁边的下拉框，然后选择“提 **[!UICONTROL 交以待批准”]**

   ![Submit for Approval](images/publishing-submitForApproval.png)

1. 单击对 **[!UICONTROL 话框中]** “提交”按钮：

   ![在Modal中单击“提交”](images/publishing-submit.png)

1. 您的库现在将以未构建状态 [!UICONTROL 显示在] “已提交”列中：

1. 打开下拉列表，然后选择 **[!UICONTROL 构建以进行升级]**:

   ![Build for Staging](images/publishing-buildForStaging.png)

1. 出现绿色圆点图标后，便可以在暂存环境中预览库。

在真实情景中，该过程的下一步通常是让您的 QA 团队验证暂存库中所做的更改。他们可以使用调试器执行此操作。

**验证暂存库中的更改**

1. 在“启动”属性中，打开“环 [!UICONTROL 境] ”页

1. 在“暂 [!UICONTROL 存] ”行中 ![，单击“安装”图标“](images/launch-installIcon.png) 安装”图标，打开模态

   ![转到“环境”页面并单击以打开模态](images/publishing-getStagingCode.png)

1. 单击复制图标 ![复制图标](images/launch-copyIcon.png) ，将嵌入代码复制到剪贴板

1. Click **[!UICONTROL Close]** to close the modal

   ![安装图标](images/publishing-copyStagingCode.png)

1. Open the [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html) in your Chrome browser

1. 单击“调 [试器图标”图标](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) ，打开 ![Experience Cloud调试器扩展](images/icon-debugger.png)

   ![单击“调试器”图标](images/switchEnvironments-openDebugger.png)

1. 转到工具选项卡

1. 单击 **[!UICONTROL Adobe Launch &gt; Dynamically Insert Launch &gt; Embed Code]** （动态插入启动项）按钮以打开文本输入字段（该字段当前可能包含您的开发嵌入代码的URL）:

   ![单击“Adobe Launch”&gt;“动态插入启动项”&gt;“嵌入代码”按钮](images/switchEnvironments-debugger-editEmbedCode.png)

1. 粘贴剪贴板中的暂存嵌入代码

1. 单击磁盘图标以保存

   ![调试器中显示的启动环境](images/switchEnvironments-debugger-save.png)

1. 重新加载并检查调试器的“摘要”选项卡。 在“启动”部分下，您现在应该可以看到已实施暂存属性，显示您的属性名称(即“启动教程”或您为您的属性命名的任何内容)!

   ![调试器中显示的启动环境](images/publishing-debugger-staging.png)

在实际操作中，一旦QA团队通过查看暂存环境中的更改注销，就是时候发布到生产了。

## 发布到生产环境

1. Go to the [!UICONTROL Publishing] page

1. 从下拉列表中，单击 **[!UICONTROL 批准发布]**:

   ![Approve for Publishing](images/publishing-approveForPublishing.png)

1. 单击对 **[!UICONTROL 话框]** 中的“批准”按钮：

   ![单击批准](images/publishing-approve.png)

1. 库现在将显示在未构建状 [!UICONTROL 态] （黄点）的“已批准”列中：

1. 打开下拉框，然 **[!UICONTROL 后选择**构建并发布到生产]**:

   ![单击“构建并发布到生产”](images/publishing-buildAndPublishToProduction.png)

1. 单击对 **[!UICONTROL 话框中的]** “发布”:

   ![单击“发布”](images/publishing-publish.png)

1. 库现在将显示在“已发布 [!UICONTROL ”列] :

   ![已发布](images/publishing-published.png)

就是这样！ 您已经完成了教程，并在Launch中发布了您的第一个属性！