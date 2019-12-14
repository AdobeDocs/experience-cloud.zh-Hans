---
title: 通过Launch实施Experience cloud集成
description: 了解如何验证Adobe Experience cloud实施中的受众、A4T和客户属性集成。 本课程是在包含Launch教程的网站中实施Experience cloud的一部分。
seo-description: null
seo-title: 通过Launch实施Experience cloud集成
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: e9dee6d0aa3b775d0ce617e2b2c57b56de491b8d

---


# Experience Cloud 集成

在本课中，您将回顾您刚刚实施的解决方案之间的关键集成。 好消息是，通过完成之前的课程，您已经实施了集成的代码部分！ 除了阅读和验证，您无需在本课程中做任何其他工作。

## 学习目标

在本课程结束后，您将能够：

1. 解释受众共享、Analytics for Target(A4T)和客户属性集成的基本使用案例
1. 验证这些集成的基本客户端实施方面

## 先决条件

在按照本课程中的说明操作之前，您应完成本教程中的所有以前的课程。

>[!NOTE]  要充分使用这些集成，需要满足许多用户权限要求并完成相应的帐户配置和置备步骤，而这些内容都不在本教程的涵盖范围内。如果您尚未在Experience Cloud的当前实施中使用这些集成，您应考虑以下事项：
>
> * 查看[核心服务集成](https://docs.adobe.com/content/help/en/core-services/interface/about-core-services/core-services.html)的完整要求
> * 查看 [Analytics for Target 集成](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/before-implement.html)的完整要求
> * Have an Administrator of your Experience Cloud Organization [request provisioning of these integrations](https://www.adobe.com/go/audiences)


## 受众

[受众](https://docs.adobe.com/content/help/en/core-services/interface/audiences/audience-library.htm) 是People Core service的一部分，允许您在解决方案之间共享受众。 例如，您可以在Audience manager中创建受众，然后使用它通过Target提供个性化内容。

实施A4T（您已经做过）的主要要求是：

1. 实施Adobe Experience Platform Identity Service
1. 实施Audience Manager
1. 实施您希望接收或创建受众的其他解决方案，如Target和Analytics

### 验证受众集成

验证受众集成的最佳方法是实际构建受众，将其共享到另一个解决方案，然后在另一个解决方案中充分使用它（例如，确认符合AAM区段资格的访客可以获得针对该区段的Target活动）。 但是，这不在本教程的涵盖范围内。

这些验证步骤将侧重于客户端实施中可见的关键部分——访客ID。

1. Open the [Luma site](https://luma.enablementadobe.com/content/luma/us/en.html)

1. Make sure the Debugger is mapping the Launch property to *your* Development environment, as described in the [earlier lesson](launch-switch-environments.md)

   ![调试器中显示的启动开发环境](images/switchEnvironments-debuggerOnWeRetail.png)

1. 转到调试器的“网络”选项卡

1. 单击 **[!UICONTROL “清除所有请求]** ”，只是清理事项

1. 重新加载Luma页面，确保您在调试器中同时看到Target和Analytics请求

1. 再次重新加载Luma页面

1. 现在，您应该会在调试器的“网络”选项卡中看到四个请求——两个用于Target，两个用于Analytics

1. 在标有“Experience Cloud访客ID”的行中查找。 每个解决方案对应的每个请求中的 ID 应始终相同。

   ![确认匹配的SDID](images/integrations-matchingECIDs.png)

1. 每个访客的 ID 均是唯一的，您可以通过请求同事重复执行上述步骤来进行确认。

## Analytics for Target (A4T)

The [Analytics for Target (A4T)](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html) integration allows you to leverage your Analytics data as the source for reporting metrics in Target.

实施A4T（您已经做过）的主要要求是：

1. 实施Adobe Experience Platform Identity Service
1. 在分析页面查看信标之前触发目标页面加载请求

A4T的工作方式是将从Target到Analytics的服务器端请求与Analytics页面视图信标拼接在一起，我们称之为“点击拼接”。  点击拼接要求提交活动的Target请求（或增加基于Target的目标量度）具有与Analytics页面视图信标中的参数相匹配的参数。 此参数称为补充数据id(SDID)。

### 验证 A4T 实施

验证A4T集成的最佳方法是使用A4T实际构建Target活动并验证报告数据，但这超出了本教程的范围。 本教程将向您介绍如何确认补充数据ID在解决方案调用之间匹配。

**验证SDID**

1. Open the [Luma site](https://luma.enablementadobe.com/content/luma/us/en.html)

1. Make sure the Debugger is mapping the Launch property to *your* Development environment, as described in the [earlier lesson](launch-switch-environments.md)

   ![调试器中显示的启动开发环境](images/switchEnvironments-debuggerOnWeRetail.png)

1. 转到调试器的“网络”选项卡

1. 单击 **[!UICONTROL “清除所有请求]** ”，只是清理事项

1. 重新加载Luma页面，确保您在调试器中同时看到Target和Analytics请求

1. 再次重新加载Luma页面

1. 现在，您应该会在调试器的“网络”选项卡中看到四个请求——两个用于Target，两个用于Analytics

1. 查看标记为“Supplemental Data ID”的行。第一页加载中的ID应在Target和Analytics之间匹配。 第二次页面加载所产生的 ID 也应该相匹配，但与首次页面加载所产生的 ID 不相同。

   ![确认匹配的SDID](images/integrations-matchingSDIDs.png)

如果您在属于A4T活动的页面加载范围（不包括单页应用程序）中发出其他Target请求，则最好为这些请求指定唯一名称（而非target-global-mbox），以便它们继续具有初始Target和Analytics请求的相同SDID。

## 客户属性

[客户属性](https://docs.adobe.com/content/help/en/core-services/interface/customer-attributes/attributes.html) 是People Core service的一部分，它允许您从客户关系管理(CRM)数据库上传数据并在Adobe Analytics和Adobe Target中利用它。

实施客户属性（您已经这样做）的主要要求是：

1. 实施Adobe Experience Platform Identity Service
1. Set Customer Ids via the Id Service *before* Target and Analytics fire their requests (which you accomplished using the rule ordering feature in Launch)

### 验证客户属性实施

您已经验证，客户ID已在先前的课程中传递给Identity service和Target。 您还可以在Analytics点击中验证客户ID。
目前，客户ID是Experience Cloud调试器中未显示的少数参数之一，因此您将使用浏览器的JavaScript控制台查看它。

1. 打开Luma站点
1. 打开浏览器的开发人员工具
1. 转到“网络”选项卡
1. 在筛选器字段中，键 `b/ss` 入将您看到的内容限制在Adobe Analytics请求中的类型

   ![打开开发人员工具并过滤网络选项卡，以仅显示Analytics请求](images/aam-openTheJSConsole.png)

1. 单击 **[!UICONTROL 站点右上角的]** LOGIN链接

   ![单击顶部导航中的登录](images/idservice-loginNav.png)

1. 输入 `test@adobe.com` 用户名
1. 输入 `test` 密码
1. 单击“ **[!UICONTROL LOGIN]** ”按钮

   ![输入凭据并单击登录](images/idservice-login.png)

1. 它应将您返回到主页，该主页还将触发可在开发人员工具中看到的信标。 如果您被带到帐户信息页面，请单击WE.RETAIL徽标以返回主页。
1. 单击请求，然后选择“标题”选项卡
1. 向下滚动直到您看到一些嵌套参数
   1. cid —— 这是请求的客户ID部分的标准分隔符
   1. crm_id —— 这是您在Identity service课程中指定的自定义集成代码
   1. id - The Customer ID value coming from your `Email (Hashed)` data element
   1. as —— 身份验证状态，含“1”个含义的登录
   ![分析客户ID验证](images/integrations-analyticsCustomerIDValidation.png)

[下一个“发布您的属性”&gt;](publish.md)