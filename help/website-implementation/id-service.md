---
title: 通过Launch实施Adobe Experience Platform Identity Service
description: 了解如何添加Adobe Experience Platform Identity service扩展并使用“设置客户ID”动作收集客户ID。 本课程是在包含Launch教程的网站中实施Experience cloud的一部分。
seo-description: null
seo-title: 通过Launch实施Adobe Experience Platform Identity Service
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: 7166d2933cc99bcbbd4713fba8f87fb0826b711e

---


# 添加Adobe Experience Platform Identity Service

本课程将指导您完成实施 [Adobe Experience Platform Identity service扩展和发送客户ID所需的步骤](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html) 。

Adobe [Experience Platform Identity Service](https://docs.adobe.com/content/help/en/id-service/using/home.html) (Adobe Experience Platform Identity Service)可在所有Adobe解决方案中设置一个通用访客ID，以便支持Experience cloud功能，如在解决方案之间共享受众。  您还可以将您自己的客户ID发送到服务，以实现跨设备定位以及与客户关系管理(CRM)系统的集成。

## 学习目标

在本课程结束后，您将能够：

* 添加Identity service扩展
* 创建数据元素以收集您的客户ID
* 创建使用“设置客户ID”操作将客户ID发送到Adobe的规则
* 使用规则排序功能对同一事件中触发的规则进行排序

## 先决条件

You should have already completed the lessons in the [Configure Launch](launch.md) section.

## 添加Identity Service Extension

由于这是您要添加的第一个扩展，因此此处是扩展的快速概述。 扩展是Launch的核心功能之一。 扩展是由Adobe、Adobe合作伙伴或任何Adobe客户构建的集成，它为可部署到网站的标记添加了新的、无穷的选项。 如果您认为Launch是一个操作系统，则扩展是您安装的应用程序，因此Launch可以完成您需要的任务。

**添加Identity Service Extension**

1. In the top navigation, click **[!UICONTROL Extensions]**

1. 单击 **[!UICONTROL 目录]** ，转到“扩展目录”页

   ![转到扩展目录](images/extensions-goToExtensionsCatalog.png)

1. 请注意目录中提供的各种扩展

1. 在顶部的过滤器中，键入“id”以过滤目录

1. 在Adobe Experience Platform Identity service的卡片上，单击“安 **[!UICONTROL 装”]**

   ![安装Identity Service Extension](images/idservice-install.png)

1. 请注意，您的Experience cloud组织ID已自动检测到。

1. 保留所有默认设置，然后单击“保 **[!UICONTROL 存到库并构建”]**

   ![保存扩展](images/idservice-save.png)

>[!NOTE] 每个版本的Identity service扩展都附带特定版本的VisitorAPI.js，扩展说明中对此进行了说明。 您可以通过更新Identity service扩展来更新VisitorAPI.js版本。

### 验证扩展

Identity service扩展是少数几个无需使用规则操作即可发出请求的启动扩展之一。 在首次访问网站时，扩展将在第一页加载时自动向Identity service发出请求。 请求ID后，它将存储在以“AMCV_”开头的第一方Cookie中。

**验证Identity service扩展**

1. Open the [Luma site](https://luma.enablementadobe.com/content/luma/us/en.html)

1. Make sure the Debugger is mapping the Launch property to *your* Development environment, as described in the [earlier lesson](launch-switch-environments.md).

1. 在调试器的“摘要”选项卡上，“启动”部分应指示已实施Adobe Experience Platform Identity service扩展。

1. 此外，在“摘要”选项卡上，“标识服务”部分应填充与启动界面中扩展配置屏幕上相同的组织ID:

   ![检查是否已实施Adobe Experience Platform Identity service扩展](images/idservice-debugger-summary.png)

1. 检索访客ID的初始请求可能显示在调试器的“标识服务”选项卡中。 不过，它可能已经被请求了，所以如果您看不到它，请不要担心：
   ![检查是否存在对组织ID的Identity service的请求](images/idservice-idRequest.png)

1. 在发出获取访客 ID 的初始请求后，该 ID 会存储在名称以 `AMCV_` 开头的 Cookie 中。您可以通过执行以下操作确认已设置该 Cookie：
   1. 打开浏览器的开发人员工具
   1. Go to the `Application` tab
   1. Expand `Cookies` on the left side
   1. Click on the domain `https://luma.enablementadobe.com`
   1. 在右侧查找AMCV_ cookie。 您可能会看到几个这样的站点，它既使用硬编码的Launch属性，也映射到您自己的站点。
      ![验证AMCV_ cookie](images/idservice-AMCVCookie.png)

就这么简单！您已经添加了第一个扩展！ 有关Identity service配置选项的更多详细信息，请参 [阅文档](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/configurations/function-vars.html)。

## 发送客户ID

接下来，您将向 [Identity Service](https://docs.adobe.com/content/help/en/id-service/using/reference/authenticated-state.html) 发送客户ID。 This will allow you to [integrate your CRM](https://docs.adobe.com/content/help/en/core-services/interface/customer-attributes/attributes.html) with the Experience Cloud as well as track visitors across devices.

In the earlier lesson, [Add Data Elements, Rules, and Libraries](launch-data-elements-rules.md) you created a data element and used it in a rule. 现在，您将使用这些相同的技术在访客通过身份验证后发送客户ID。

### 为客户 ID 创建数据元素

首先，创建两个数据元素：

1. `Authentication State`—捕获访客是否登录
1. `Email (Hashed)`—从数据层捕获散列化版本的电子邮件地址（用作客户ID）

**为身份验证状态创建数据元素**

1. 单击 **[!UICONTROL 顶部导航中的]** “数据元素”
1. 单击“添 **[!UICONTROL 加数据元素”按钮]**

   ![单击“添加数据元素”](images/idservice-addDataElement1.png)

1. Name the data element `Authentication State`
1. 对于“数 **[!UICONTROL 据元素类型]**”，选择“自 **[!UICONTROL 定义代码”]**
1. 单击“打 **[!UICONTROL 开编辑器”按钮]**

   ![打开编辑器以添加数据元素的自定义代码](images/idservice-authenticationState.png)

1. 在“编 [!UICONTROL 辑代码] ”窗口中，使用以下代码根据Luma站点数据层中的属性返回“已登录”或“已注销”的值：

   ```javascript
   if (digitalData.user[0].profile[0].attributes.loggedIn)
       return "logged in"
   else
       return "logged out"
   ```

1. Click **[!UICONTROL Save]** to save the custom code

   ![保存自定义代码](images/idservice-authenticationCode.png)

1. 将所有其他设置保留为其默认值。
1. 单击 **[!UICONTROL 保存到库并构建]** ，以保存数据元素并返回到数据元素页面

   ![保存数据元素](images/idservice-authenticationStateFinalSave.png)

通过了解用户的身份验证状态，您就可以知道何时应在要发送到标识服务的页面上存在客户ID。 下一步是为客户ID本身创建数据元素。 在Luma演示站点上，您将使用访客电子邮件地址的哈希版本。

**为散列电子邮件添加数据元素**

1. 单击“添 **[!UICONTROL 加数据元素”按钮]**

   ![添加数据元素](images/idservice-addDataElement2.png)

1. Name the data element `Email (Hashed)`
1. 对于“数 **[!UICONTROL 据元素类型]**”，选择 **[!UICONTROL JavaScript变量]**
1. 作为 **[!UICONTROL JavaScript变量名]**，请使用以下指向Luma站点数据层中的变量的指针： `digitalData.user.0.profile.0.attributes.username`
1. 将所有其他设置保留为其默认值。
1. 单击 **[!UICONTROL 保存到库并构建]** ，以保存数据元素

   ![保存数据元素](images/idservice-emailHashed.png)

### 添加用于发送客户 ID 的规则

Adobe Experience Platform Identity service使用称为“设置客户ID”的操作在规则中传递客户ID。您现在将创建一个规则，以在访客通过身份验证后触发此操作。

**创建用于发送客户ID的规则**

1. In the top navigation, click **[!UICONTROL Rules]**
1. 单击 **[!UICONTROL 添加规则]** ，以打开规则生成器

   ![添加规则](images/idservice-addRule.png)

1. Name the rule `All Pages - Library Loaded - Authenticated - 10`

   >[!TIP] 此命名约定表示当用户通过身份验证且其顺序为“10”时，您将在所有页面顶部触发此规则。 使用这样的命名约定（而不是为操作中触发的解决方案命名）可以最大限度地减少实施所需的规则总数。

1. Under **[!UICONTROL Events]** click **[!UICONTROL Add]**

   ![添加活动](images/idservice-customerId-addEvent.png)

   1. For the **[!UICONTROL Event Type]** select **[!UICONTROL Library Loaded (Page Top)]**
   1. For the  **[!UICONTROL Order]** enter `10`. 顺序控制由同一事件触发的规则序列。顺序较低的规则在顺序较高的规则之前触发。 In this case, you want to set the customer ID before you fire the Target request, which you will do in the next lesson with a rule with an order of `50` .
   1. 单击“ **[!UICONTROL 保留更改]** ”按钮以返回到规则生成器
   ![保存活动](images/idservice-customerId-saveEvent.png)

1. 在“条 **[!UICONTROL 件”下]** ，单击“添 **[!UICONTROL 加”]**

   ![向规则添加条件](images/idservice-customerId-addCondition.png)

   1. 对于条件 **[!UICONTROL 类型]** ，选择 **[!UICONTROL 值比较]**
   1. Click the ![data element icon](images/icon-dataElement.png) icon to open the Data Element modal

      ![打开数据元模式](images/idservice-customerId-valueComparison.png)

   1. 在“数据元素模式”中，单击“身份验 **[!UICONTROL 证状态]** ”，然后单击“选 **[!UICONTROL 择”]**

      ![设置身份验证状态](images/idservice-customerId-authStateCondition.png)

1. Make sure `Equals` is the operator
1. 在文本字段中键入“logged in”，当数据元素“身份验证状态”的值为“logged in”时，将触发规则

1. Click **[!UICONTROL Keep Changes]**

   ![保存条件](images/idservice-customerId-loggedIn.png)

1. 在“操 **[!UICONTROL 作”下]** ，单击“添 **[!UICONTROL 加”]**

   ![添加新操作](images/idservice-customerId-addAction.png)

   1. 对于扩 **[!UICONTROL 展]** ，请选 **[!UICONTROL 择Adobe Experience Platform Identity Service]**
   1. 对于“操 **[!UICONTROL 作类型]** ”，选 **[!UICONTROL 择“设置客户ID”]**
   1. 对于集 **[!UICONTROL 成代码]** , `crm_id`
   1. 对于“ **[!UICONTROL 值]** ”，输入打开“数据元素”选择器模式，然后选择 `Email (Hashed)`
   1. 对于身份验证 **[!UICONTROL 状态]** ，选择已验 **[!UICONTROL 证]**
   1. Click the **[!UICONTROL Keep Changes]** button to save the action and return to the Rule Builder

      ![配置操作并保存更改](images/idservice-customerId-action.png)

1. 单击“ **[!UICONTROL 保存到库并构建]** ”按钮以保存规则

   ![保存规则](images/idservice-customerId-saveRule.png)

您现在已创建规则，在访客通过身份验证后，将客户ID `crm_id` 作为变量发送。 由于您将“顺序”指定为 `10` 此规则，因此在您在“添加数据元素、规则和库”课程中创建的规则之前将触发 `All Pages - Library Loaded` ，该课程使用默认的“顺序”值 [](launch-data-elements-rules.md)`50`。

### 验证客户ID

要验证您的工作，您将登录Luma站点以确认新规则的行为。

**登录Luma站点**

1. Open the [Luma site](https://luma.enablementadobe.com/content/luma/us/en.html)

1. Make sure the Debugger is mapping the Launch property to *your* Development environment, as described in the [earlier lesson](launch-switch-environments.md)

   ![调试器中显示的启动开发环境](images/switchEnvironments-debuggerOnWeRetail.png)

1. 单击 **[!UICONTROL Luma站点右上角的]** LOGIN链接

   ![单击顶部导航中的登录](images/idservice-loginNav.png)

1. 输入 `test@adobe.com` 用户名
1. 输入 `test` 密码
1. 单击“ **[!UICONTROL LOGIN]** ”按钮

   ![输入凭据并单击登录](images/idservice-login.png)

1. 返回主页

现在，使用调试器扩展确认客户ID已发送到服务。

**验证Identity service是否正在传递客户ID**

1. 确保Luma站点的选项卡处于焦点
1. 在调试器中，转到Adobe Experience Platform Identity service选项卡
1. 展开您的组织ID
1. Click on the cell with the `Customer ID - crm_id` value
1. In the modal, note the customer id value and that the `AUTHENTICATED` state is reflected:

   ![在调试器中确认客户ID](images/idservice-debugger-confirmCustomerId.png)

1. 请注意，您可以通过查看Luma页面的源代码并查看username属性来确认哈希化的电子邮件值。 它应与您在调试器中看到的值相匹配：

   ![在源代码中散列电子邮件](images/idservice-customerId-inSourceCode.png)

### 其他验证提示

Launch还具有丰富的控制台日志记录功能。 要打开它们，请转到调试器中的 **[!UICONTROL 工具]** ，然后打开启动控制台日志 **[!UICONTROL 记录切换]** 。

![打开启动项的控制台日志记录](images/idservice-debugger-logging.png)

此操作将在浏览器控制台和调试器的“日志”选项卡中打开控制台日志记录。 您应当看到您创建的所有规则的记录！ 请注意，新日志条目将添加到列表顶部，因此您的规则“所有页面——已加载库——已验证- 10”应在“所有页面——已加载库”规则之前触发，并显示在调试器的控制台日志记录中它的下方：

![调试器的“日志”选项卡](images/idservice-debugger-loggingStatements.png)

[下一个“添加Adobe Target”&gt;](target.md)
