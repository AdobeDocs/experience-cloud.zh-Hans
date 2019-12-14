---
title: 实施启动嵌入代码
description: 了解如何获取Launch属性的嵌入代码并在您的网站中实施它们。 本课程是在包含Launch教程的网站中实施Experience cloud的一部分。
seo-description: null
seo-title: 实施启动嵌入代码
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: 14e46fa7d806f2713a69fe5d3a0a8c326de26d23

---


# 添加 Launch 嵌入代码

在本课中，您将实现Launch属性的开发环境的异步嵌入代码。 在此过程中，您将了解Launch的两个主要概念——环境和嵌入代码。

## 学习目标

在本课程结束后，您将能够：

* 获取Launch属性的嵌入代码
* 了解开发、暂存和生产环境之间的差异
* 将启动项嵌入代码添加到HTML文档
* Explain the optimal location of the Launch embed code in relation to other code in the `<head>` of an html document

## 复制嵌入代码

The embed code is a `<script>` tag that you put on your webpages to load and execute the logic you build in Launch. 如果异步加载库，浏览器将继续加载页面，检索启动库并并行执行它。 在这种情况下，将只有一个嵌入代码，即放置在 `<head>` 中的代码。(When Launch is deployed synchronously, there are two embed codes, one which you put in the `<head>` and another which you put before the `</body>`).

在资产 Overview 屏幕中，单击 `Environments` 选项卡以转到环境页面。请注意，开发、暂存和生产环境已经为您预先创建。

![单击顶部导航中的“环境”](images/launch-environments.png)

开发、暂存和生产环境对应于代码开发和发布过程中的典型环境。代码首先由开发人员在开发环境中编写。 完成工作后，开发人员会将代码发送到暂存环境，供 QA 和其他团队审查。满足QA和其他团队的要求后，该代码将发布到生产环境，该环境是访客访问您的网站时体验到的面向公众的环境。

Launch允许额外的开发环境，这对于多个开发人员同时处理不同项目的大型组织非常有用。

这是完成本教程所需的唯一环境。 环境允许您在不同URL上托管不同的启动库工作版本，因此您可以安全地添加新功能并将这些功能提供给适当的用户（例如开发人员、QA工程师、公众等）在正确的时间。

现在，让我们复制嵌入代码：

1. In the **[!UICONTROL Development]** row, click the Install icon ![Install icon](images/launch-installIcon.png) to open the modal.

1. 请注意，Launch将默认采用异步嵌入代码

1. 单击复制图标 ![复制图标](images/launch-copyIcon.png) ，将嵌入代码复制到剪贴板。

1. Click **[!UICONTROL Close]** to close the modal.

   ![安装图标](images/launch-copyInstallCode.png)

## Implement the Embed Code in the `<head>` of the Sample HTML Page

The embed code should be implemented in the `<head>` element of all HTML pages that will share the property. You might have one or several template files which control the `<head>` globally across the site, making it a straightforward process to add Launch.

如果尚未下载示例html页 [面](https://www.enablementadobe.com/multi/web/basic-sample.html) （右键单击此链接，然后单击“将链接另存为”），然后在代码编辑器中将其打开。 [Brackets](http://brackets.io/) 是免费的开放源代码编辑器（如果需要）。

将第34行或第34行周围的现有嵌入代码替换为剪贴板上的嵌入代码并保存页面。 现在，在Web浏览器中打开页面。 If you are loading the page using the `file://` protocol, you will need to add "https:" at the beginning of the embed code URL in your code editor). 示例页面的第 33-36 行可能如下所示：

```html
    <!--Launch Header Embed Code: REPLACE LINE 39 WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="https://assets.adobedtm.com/launch-ENa21cfed3f06f4ddf9690de8077b39e81-development.min.js" async></script>
    <!--/Launch Header Embed Code-->
```

打开Web浏览器的开发人员工具并转到“网络”选项卡。 At this point you should see a 404 error for the Launch environment URL:
![404 error](images/samplepage-404.png)

应该出现404错误，因为您尚未在此启动环境中构建库。 您将在下一个课程中学习如何构建库。如果您看到“失败”消息而不是 404 错误，则您可能忘记在嵌入代码中添加 `https://` 协议。再次重申，仅当使用 `file://` 协议加载示例页面时，才需要指定 `https://` 协议。做出相应更改，然后重新加载页面，直到出现 404 错误。

## 启动实施最佳实践

让我们花点时间来查看一些Launch实施最佳实践，这些实践在示例页中进行了演示：

* **数据层**：

   * We *strongly* recommend creating a digital data layer on your site containing all of the attributes needed to populate variables in Analytics, Target, and other marketing solutions. 此示例页面仅包含一个非常简单的数据层，但实际的数据层可能包含更多与页面、访客、访客购物车详情及其他内容相关的详细信息。For more info on data layers, please see [Customer Experience Digital Data Layer 1.0](https://www.w3.org/2013/12/ceddl-201312.pdf)

   * 在启动嵌入代码之前定义数据层，以便最大化您在Target、客户属性和分析中的功能。

* **JavaScript帮助程序库**:如果页面中已实施JQuery等库，请在启动之前加 `<head>` 载它，以便在启动和目标中利用其语法

* **HTML5 doctype**:Target需要HTML5 doctype

* **preconnect 和 dns-prefetch**：可使用 preconnect 和 dns-prefetch 缩短页面加载时间。See also: [https://w3c.github.io/resource-hints/](https://w3c.github.io/resource-hints/)

* **异步Target实现的预隐藏代码片断**:您将在Target课程中进一步了解这一点，但是，当通过异步启动嵌入代码部署Target时，您应在启动嵌入代码之前在页面上硬编写预隐藏的代码片断，以便管理内容闪烁

下面按建议顺序总结了上述最佳实践。请注意，有一些占位符可用于查看帐户特定的详细信息：

```html
<!doctype html>
<html lang="en">
<head>
    <title>Basic Demo</title>
    <!--Preconnect and DNS-Prefetch to improve page load time. REPLACE "techmarketingdemos" WITH YOUR OWN AAM PARTNER ID, TARGET CLIENT CODE, AND ANALYTICS TRACKING SERVER-->
    <link rel="preconnect" href="//dpm.demdex.net">
    <link rel="preconnect" href="//fast.techmarketingdemos.demdex.net">
    <link rel="preconnect" href="//techmarketingdemos.demdex.net">
    <link rel="preconnect" href="//cm.everesttech.net">
    <link rel="preconnect" href="//techmarketingdemos.tt.omtrdc.net">
    <link rel="preconnect" href="//techmarketingdemos.sc.omtrdc.net">
    <link rel="dns-prefetch" href="//dpm.demdex.net">
    <link rel="dns-prefetch" href="//fast.techmarketingdemos.demdex.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.demdex.net">
    <link rel="dns-prefetch" href="//cm.everesttech.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.tt.omtrdc.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.sc.omtrdc.net">
    <!--/Preconnect and DNS-Prefetch-->
    <!--Data Layer to enable rich data collection and targeting-->
    <script>
    var digitalData = {
        "page": {
            "pageInfo" : {
                "pageName": "Home"
                }
            }
    };
    </script>
    <!--/Data Layer-->
    <!--jQuery or other helper libraries-->
    <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
    <!--/jQuery-->
    <!--prehiding snippet for Adobe Target with asynchronous Launch deployment-->
    <script>
        (function(g,b,d,f){(function(a,c,d){if(a){var e=b.createElement("style");e.id=c;e.innerHTML=d;a.appendChild(e)}})(b.getElementsByTagName("head")[0],"at-body-style",d);setTimeout(function(){var a=b.getElementsByTagName("head")[0];if(a){var c=b.getElementById("at-body-style");c&&a.removeChild(c)}},f)})(window,document,"body {opacity: 0 !important}",3E3);
    </script>
    <!--/prehiding snippet for Adobe Target with asynchronous Launch deployment-->
    <!--Launch Header Embed Code: REPLACE LINE 39 WITH THE INSTALL CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
    <!--/Launch Header Embed Code-->
</head>
<body>
    <h1>Launch by Adobe: Basic Demo</h1>
    <p>This is a very simple page to demonstrate basic concepts of Launch by Adobe</p>
</body>
</html>
```

现在您了解如何将启动项嵌入代码添加到您的站点！

[下一个“添加数据元素、规则和库”&gt;](launch-data-elements-rules.md)