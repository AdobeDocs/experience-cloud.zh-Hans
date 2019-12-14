---
title: 通过Launch实施Adobe Analytics
description: 了解如何使用Adobe Analytics Launch扩展实施Adobe Analytics、发送屏幕视图信标、添加变量、跟踪事件和添加插件。 本课程是在Mobile android应用程序中实施Experience cloud教程的一部分。
seo-description: null
seo-title: 通过Launch实施Adobe Analytics
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: e9dee6d0aa3b775d0ce617e2b2c57b56de491b8d

---


# 添加 Adobe Analytics

在本课中，您将在应用程序中启用Adobe Analytics跟踪。

[Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/landing/home.html) 是一款行业领先的解决方案，可帮助您充分了解客户的行为和需求，并根据客户情报掌控自己的业务发展方向。

在“添 [加扩展](launch-add-extensions.md) ”和“安 [装Mobile SDK](launch-install-the-mobile-sdk.md) ”课程中，您将Adobe Analytics扩展添加到您的Launch属性中，并将其导入到示例应用程序中。  现在，您只需添加代码来跟踪应用程序中的状态和操作！

## 学习目标

在本课程结束后，您将能够：

* 验证是否将生命周期指标发送到Adobe Analytics
* 添加代码以使用其他数据跟踪应用程序中的状态
* 添加代码以跟踪应用程序中的操作并包含其他数据

在Launch中，可以为Analytics实施许多内容。 本课程并非详尽无遗，但应为您提供在您自己的应用程序中实施所需的主要技术的可靠概述。

## 先决条件

You should have already completed the lessons in the [Configure Launch](launch-create-a-property.md) section. 在该部分中，您添加了Analytics扩展并配置了跟踪服务器和报表包ID。

## 生命周期指标和Adobe Analytics

生命周期指标是基于环境的指标和维度，可以使用Experience Platform Mobile SDK在应用程序中轻松启用这些指标和维度。

在将核心扩展添加到您的属性中并遵循界面中提供的移动安装说明时，您已经启用了生命周期指标。 这些指标和维度，包括特定于环境和应用程序的指标，如应用程序版本、参与用户数、操作系统版本、分时段、上次使用后的天数等。 在应用程序分析中非常有用，尤其是当您从中构建Analytics区段以应用于所有报告时。 文档中提供了完整的指标 [列表](https://docs.adobe.com/content/help/en/mobile-services/android/metrics.htmlh)。

## 导入ACPCore库

在前面的课程“安 [装Mobile SDK”中](launch-install-the-mobile-sdk.md)，您添加了一个import语句，以使AdobeCore库在BusBookingActivity文件中可用。 此库将用于本课程中活动的其他API调用。 在下一个练习中，您将使用API跟踪应用程序中的状态(“trackState”)和操作(“trackAction”)，这些操作在AdobeCore库中定义。  在新的Experience Cloud Platform Mobile SDK中，trackState和trackAction API已从Analytics库移动到核心库，这使得可以将这些API用于除Adobe Analytics跟踪之外的其他用途。

## 跟踪状态

在您的应用程序中，您可能有许多不同的内容屏幕，供您的用户使用。 这些是网站上的页面。 Adobe Analytics为您提供了一种方法，允许您在这些“页面查看点击”中发送，并在用于Web属性的相同报告中查看这些点击。 此方法称为“trackState”。

在本教程中，您将将trackState调用的代码仅放置到应用程序中的一个屏幕（页面）中。 在现实生活中，您将在应用程序中的所有其他屏幕／状态上复制此项。

下面是文档中的语法和代码示例，您可以在本教程中或您自己的应用程序中复制并粘贴。

**语法：**

```java
public static void trackState(final String state, final Map<String, String> contextData)
```

**示例：**

```java
HashMap cData = new HashMap<String, String>();
contextData.put("key", "value");
MobileCore.trackState("state name",contextData);
```

### 跟踪无数据状态

1. 在Android studio中打开范例应用程序，转到BusBookingActivity，然后在底部附近向下滚动到onResume函数
1. 添加trackState方法调用
1. 将“预 `state name` 订屏幕”设置为
1. 添加API调用中的占位符，而不 `null` 是添加任何额外数据
1. 或复制并粘贴到以下位置：

   ```java
   MobileCore.trackState("Booking Screen", null);
   ```

![基本trackState调用](images/android/mobile-analytics-basicTrackStateCall2.png)

**验证trackState**

1. 保存、构建和运行项目
1. 当模拟器运行并打开应用程序的主屏幕时，请查看Android Studio Logcat调试控制台
1. 在控制台中搜索 `pageName=Booking%20Screen`
1. 请注意，pageName变量设置为( `Booking Screen` 将%20作为编码空间)，并且没有其他自定义数据对。 虽然从技术上讲，您是在设置“状态名称”而不是“页面名称”，但使用的参数名称是为了 `pageName` 提供与网站实施的一致性。

   ![基本trackState结果](images/android/mobile-analytics-basicTrackStateResult.png)

### 使用数据跟踪状态

1. 返回BusBookingActivity，并在现有导入下向文件顶部添 `import java.util.HashMap;` 加一个导入
1. 在函 `onResume()` 数中，注释掉（或删除）上一个练习中的基本trackState调用
1. 添加新的trackState方法调用，这次通过创建和命名HashMap来调用数据，使用“put”命令包含一些键／值对，然后在调用trackState时调用该HashMap
1. 保留 `state name` 为“预订屏幕”
1. 或复制并粘贴到：

   ```java
   HashMap cData = new HashMap<String, String>();
   cData.put("cd.section", "Bus Booking");
   cData.put("cd.subSection", "Booking");
   cData.put("cd.conversionType", "Landing");
   MobileCore.trackState("Booking Screen", cData);
   ```

   ![trackState调用与数据](images/android/mobile-analytics-trackStateWithData.png)

**用数据验证trackState**

1. 再次保存、构建和运行项目
1. 当模拟器运行并打开应用程序的主屏幕时，请查看Android Studio Logcat调试控制台
1. 搜索 `subSection` （或您在代码中输入的任何键或值）
1. 现在，除了设置pageName之外，您还有在点击时发送的键／值对

   ![trackState与数据结果](images/android/mobile-analytics-trackStateWithDataResult.png)

>[!NOTE] 如果您熟悉Analytics中的“prop和eVar”，您会注意到这些变量名称不在SDK中。 来自SDK的所有关键／值数据将作为 [contextData变量发送](https://docs.adobe.com/content/help/en/analytics/implementation/javascript-implementation/variables-analytics-reporting/context-data-variables.html)，因此，需要使用Analytics UI中的处理规则将其映射到prop或eVar [](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules.html) （或其他变量）。

## 跟踪操作

与跟踪网站上的非页面加载操作类似，您通常希望跟踪用户在您的应用程序中执行的操作，例如单击不加载其他屏幕的项。 这的处理方式与上述方法的trackState非常相似，只是调用了此方法 `trackAction`。

以下是文档中的语法和代码示例。

**语法：**

```java
public static void trackAction(final String action, final Map<String, String> contextData) data;
```

**示例：**

```java
HashMap<String, String> contextData = new HashMap<String, String>();
contextData.put("key", "value");
MobileCore.trackAction("action taken", contextData);
```

### 跟踪与目标切换程序的交互

在此示例巴士预订应用程序中，您可以通过单击这两个值之间的箭头，将原始城市与目标城市切换。 您已决定要跟踪Adobe Analytics中与此功能的交互。

![目标切换器](images/android/mobile-analytics-destinationSwitcher.png)

此切换程序在示例项目的BusBookingActivity文件中进行控制。 在本练习中，每当人们单击trackAction时，您都会发送该点击。

#### 添加trackAction代码

1. 在Android studio中打开示例项目，转到BusBookingActivity
1. 在第57行或第57行附近找到“mBtnFlip.setOnClickListener”函数
1. 根据需要展开函数，以便您能够看到所有代码
1. 在onClick函数中，在调用的下 `flipSourceDesti()`面添加调 `trackAction()` 用
1. 将操作名称设置为“Flip Destination”，并为contextData参数添加“null”（因为我们此时实际上不需要发送任何其他信息）
1. 您可以复制并粘贴以下代码

   ```java
   MobileCore.trackAction("Flip Destination", null);
   ```

该函数现在如下：

![目标切换器代码](images/android/mobile-analytics-destinationSwitcherCode.png)

#### 验证trackAction代码

1. 添加代码后，保存项目，运行并构建
1. 单击垃圾图标以清除日志控制台
1. 单击模拟器中的“目标切换器”箭头，注意到控制台中出现了新请求（或更多请求）。
1. 在Logcat中搜 `Flip%20Destination` 索
1. 注意，action和pev2参数Flip%20Destination（带有编码空间）
1. 注意同 `pe=lnk_o` 一行上的键／值，表明这是由trackAction触发的“自定义链接”点击

   <!--![trackAction Result in Debugger](images/android/mobile-analytics-trackActionResult1.png)-->

干得好！ 您已完成Analytics课程。 当然，您可以做许多其他事情来增强我们的Analytics实施，但希望这为您提供了满足其余需求所需的一些核心技能。

## trackState和trackAction的其他优点

在上一个练习中，您能够通过使用trackState和trackAction API将数据从应用程序发送到Adobe Analytics。 由于Experience Platform Mobile SDK植根于Launch，因此您可以在Launch界面中利用刚才添加的代码完成更多工作。

在Launch中，您可以创建由trackState和trackAction API触发的规则，并让它们执行其他操作，如向其他Adobe解决方案或外部合作伙伴发出请求。

[下一个“添加Adobe Audience Manager”&gt;](audience-manager.md)
