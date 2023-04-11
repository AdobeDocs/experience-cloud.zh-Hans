---
title: 创建和管理 Experience Cloud 触发器
description: 探索 Adobe Experience Cloud 触发器 UI
hide: true
hidefromtoc: true
source-git-commit: ce0faf9fab45c931feb666ac0c77f5ab5c231746
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 25%

---

# 创建 Experience Cloud 触发器 {#create-triggers}

>[!NOTE]
>
> Experience Cloud触发器的新用户界面提供了一个直观的体验，用于管理消费者行为和个性化用户体验。 要切换回上一个界面，请单击 **[!UICONTROL 转到经典模式]** 按钮。

创建触发器并配置触发器的条件。例如，您可以指定访问期间触发器规则的条件，如量度（购物车放弃）或维度（产品名称）。当满足规则时，触发器会运行。

1. 在Experience Cloud中，选择高级菜单，然后选择触发器。

   ![](assets/triggers_7.png)

1. 在“触发器”主页上，单击 **[!UICONTROL 创建触发器]**，然后指定触发器类型。

   提供了三种类型的触发器：

   * **[!UICONTROL 放弃]**:您可以创建一个触发器，该触发器将在访客查看了产品但未将任何产品添加到购物车时触发。

   * **[!UICONTROL 操作]**:您可以创建触发器，例如，在新闻稿注册、电子邮件订阅或信用卡申请（确认）后触发的触发器。 如果您是零售商，则可以针对注册会员计划的访客创建一个触发器。在媒体和娱乐业中，可以为观看特定节目并且您可能想要收集调查结果的访客创建触发器。

   * **[!UICONTROL 会话开始和会话结束]**:为会话开始和会话结束事件创建触发器。

   ![](assets/triggers_1.png)

1. 添加 **[!UICONTROL 名称]** 和 **[!UICONTROL 描述]** 触发器。

1. 选择Analytics **[!UICONTROL 报表包]** 用于此触发器。 此设置标识要使用的报表数据。

   [了解有关报表包的更多信息](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite.html).

1. 选择 **[!UICONTROL 没有操作后触发]** 有效期。

1. 从 **[!UICONTROL 必须包括的访问]** 和 **[!UICONTROL 必须排除的访问]** 类别中，您可以定义希望或不希望发生的标准或访客行为。 您可以指定 **和** 或 **或** 条件内或条件之间的逻辑，具体取决于您确定的条件。

   例如，一个简单的购物车放弃触发器规则可以是：

   * **[!UICONTROL 必须包括的访问]**: `Carts (metric) Is greater or equal to 1` 以定位购物车中至少有一个项目的访客。
   * **[!UICONTROL 必须排除的访问]**: `Checkout (metric) Exists.` 以删除购物车中购买了商品的访客。

   ![](assets/triggers_2.png)

1. 单击 **[!UICONTROL 容器]** 以建立和保存定义触发器的规则、条件或过滤器。 要使事件同时发生，应将它们放置在同一容器中。

   每个容器在点击级别独立处理，这意味着如果两个容器与 **[!UICONTROL 和]** 运算符，则规则仅在两次点击满足要求时才符合条件。

1. 从 **[!UICONTROL 元数据]** 字段，单击 **[!UICONTROL +Dimension]** 选择与访客行为相关的特定促销活动维度或变量。

   ![](assets/triggers_3.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。

1. 选择新创建的 **[!UICONTROL 触发器]** 以访问触发器的详细报表。

   ![](assets/triggers_4.png)

1. 从触发器的详细视图中，您可以访问有关触发器数量的报表。 如果需要，您可以使用铅笔图标编辑触发器。

   ![](assets/triggers_5.png)
