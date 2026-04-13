---
title: 在受众规则中使用上下文
description: 了解如何在受众规则中将上下文变量用于Adobe Experience转出中的功能标记和功能组。
hide: true
exl-id: 0367f475-9209-4d53-86b4-a739a73a23a7
source-git-commit: 12032cbed45e694a3f25f16afe80308b3eb82924
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# 在受众规则中使用上下文 {#context-in-audience-rules}

上下文变量是客户端应用程序在运行时提供的值。 利用这些功能，可根据动态的会话级别信息（如用户的活动语言、设备类型或应用程序状态）定位用户。

上下文变量与Web客户端和移动客户端相关。

## 上下文变量的工作方式 {#how-context-works}

在评估功能标记时，您的应用程序会将上下文变量传递到体验转出。 您可以在控制台中定义检查这些值的规则，平台在评估时使用它们来确定用户是否符合条件。

## 上下文变量类型 {#variable-types}

### 预定义（列表）类型 {#predefined-type}

上下文变量具有一组固定的允许值，例如语言或国家/地区列表。

可用运算符： **Is**，**Is Not Equal To**，**Exists**，**In**

### 整数类型 {#integer-type}

保存数字值的上下文变量。

可用运算符： **大于**、**大于或等于**、**是**、**小于**、**小于或等于**

### 字符串类型 {#string-type}

保存自由格式文本值的上下文变量。

可用运算符： **Is**，**不等于**

## 添加上下文变量 {#adding-context-variable}

要将上下文变量添加到受众规则，请执行以下操作：

1. 在控制台中打开功能标志或功能组。
2. 转到&#x200B;**受众**&#x200B;选项卡。
3. 在&#x200B;**上下文**&#x200B;下，添加新条件。
4. 选择上下文变量、运算符和值。

如果所需的上下文变量未显示在列表中，则可以从控制台的上下文变量管理部分以自助方式创建新上下文变量。

## 另请参阅 {#see-also}

* [功能标志和功能组中的受众](audience-in-feature-flags-and-feature-groups.md)
* [在受众条件中添加百分比规则](adding-percentage-rules.md)

<!-- -->
