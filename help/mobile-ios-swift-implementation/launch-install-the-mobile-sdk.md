---
title: 在Mobile iOS Swift应用程序中安装Adobe Mobile SDK
description: 了解如何获取Launch属性的嵌入代码并在您的网站中实施它们。 本课程是在Mobile iOS Swift应用程序中实施Experience cloud教程的一部分。
seo-description: null
seo-title: 在Mobile iOS Swift应用程序中安装Adobe Mobile SDK
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: d669338b0e298c44c1ef2ed1a4491b8451d45f7e

---


# 安装 Mobile SDK

在本课中，您将使用与Launch属性的“开发”环境相对应的扩展和设置来实施Mobile SDK。

## 学习目标

在本课程结束后，您将能够：

* 获取移动启动属性的安装说明
* 了解开发、暂存和生产环境之间的差异
* 创建和编辑播客文件
* 将Mobile SDK导入您的AppDelegate文件
* 验证SDK是否已成功实施

## 获取安装说明

移动启动属性的安装说明是您在终端中运行或添加到移动应用程序中特定位置的代码片段的集合。

单击顶部导 `Environments` 航中的选项卡，以转到环境页面。 请注意，开发、暂存和生产环境已经为您预先创建。 这些代码与代码开发和发布过程中的典型环境相对应。 代码首先由开发人员在开发环境中编写。 完成工作后，开发人员会将代码发送到暂存环境，供 QA 和其他团队审查。满足QA和其他团队的要求后，该代码将发布到生产环境，该环境是访客下载应用程序时体验到的面向公众的环境。

Launch允许额外的开发环境，这对于多个开发人员同时处理不同项目的大型组织非常有用。

开发、暂存和生产是完成本教程所需的唯一环境。

![单击顶部导航中的“环境”](images/mobile-launch-environments.png)

在“开 **[!UICONTROL 发]** ”行中，单击“安装”图标“ ![安装”图标](images/mobile-launch-installIcon.png) ，打开嵌入代码模式。

![单击该图标以打开嵌入代码模式](images/mobile-launch-openEmbedCode.png)

我们逐步完成说明。

## 创建播客文件并安装窗格

如果您之前在网站中使用过Launch，您首先会注意到的是，与Web属性相比，此模式中的信息要多得多。

适用于iOS的Adobe Mobile SDK使用CocoaPods管理其各个组件之间的依赖关系。 如果您的开发环境中尚未安 [装CocoaPod](https://cocoapods.org/) ，请按照其网站上的安装说明进行操作。 此外，如果尚未下载“ [Bus Booking”（巴士预订）应用程序](https://github.com/Adobe-Marketing-Cloud/busbooking-mobileapps)，请将其保存到本地计算机，然后将zip存档解压缩到桌面。

**创建播客文件**

1. 在Mac® `Terminal` 上打开应用程序

1. 导航到保存Bus Booking Swift应用程序的项目文件夹(例如， `cd Desktop/busbooking-mobileapps-master/Swift/`)

   ![导航到项目目录](images/ios/swift/mobile-launch-install-goToProjectDirectory.png)

1. 在启动界面中，将操作系统更改为 `iOS`

1. 通过单击“复制”图 `pod init`标复制第一个iOS ![说明](images/mobile-launch-copyIcon.png) 。

   ![在启动界面中将窗格初始化复制到剪贴板](images/ios/mobile-launch-install-copyPodInit.png)

1. 在您的终端应用程序中，运 `pod init` 行命令并等待其完成

   ![运行窗格初始化](images/ios/swift/mobile-launch-install-runPodInit.png)

1. 在您的终端应用程序中，使用命令打开播客文 `open podfile` 件

   ![运行打开的播客文件](images/ios/swift/mobile-launch-install-openPodfile.png)

1. 您的计算机可能会打开一个对话框，询问您要打开播客文件的应用程序。 选择任何文本编辑器，如 `TextEdit`

1. 在启动项界面中，通过单击复制图标复制依赖项 ![列表](images/mobile-launch-copyIcon.png) 。 请注意，如何为您在上一课中添加的每个扩展添加一行对应的代码。 每个扩展都有其自己的一组代码，这些代码在Mobile Core扩展上构建，并且只能通过应用程序更新添加或删除：

   ![在启动界面中将依赖关系复制到剪贴板](images/ios/mobile-launch-install-copyDependencies.png)

1. 在文本编辑器中，将从剪贴板中的依赖项粘贴到行的正后面 `# Pods for BusBookingSwift`

1. 在文本编辑器中保存对播客文件的更新

   ![添加依赖关系并保存](images/ios/swift/mobile-launch-install-addDependenciesAndSave.png)

1. 您现在可以关闭文本编辑器

1. 在启动界面中，通过单击复制图标 `pod repo update`复制下一个iOS ![说明](images/mobile-launch-copyIcon.png)

   ![复制窗格存储库更新](images/ios/mobile-launch-install-copyPodRepoUpdate.png)

1. 在您的终端应用程序中，运 `pod repo update` 行命令并等待其完成（这可能需要几分钟）

   ![运行窗格存储库更新](images/ios/swift/mobile-launch-install-podRepoUpdate.png)

1. 在启动界面中，通过单击复制图标 `pod install`复制下一个iOS ![说明](images/mobile-launch-copyIcon.png)

   ![将窗格安装复制到启动界面中的剪贴板](images/ios/mobile-launch-install-copyPodInstall.png)

1. 在您的终端应用程序中，运 `pod install` 行命令并等待其完成

   ![运行窗格安装](images/ios/swift/mobile-launch-install-podInstall.png)

1. 您现在可以关闭终端窗口

1. 打开Finder窗口，导览至保存“总线预订”应用程序的文件夹，确认已创建BusBookingSwift.xcworkspace文件、Podfile、Podfile.lock文件以及Pods文件夹

   ![在查找器中确认窗格](images/ios/swift/mobile-launch-install-podsInFinder.png)

## 更新AppDelegate

现在是时候更新应用程序以导入SDK了

1. 在Xcode中 `BusBookingSwift.xcworkspace` 打开文件
1. Open the `AppDelegate.swift` file

   ![打开AppDelegate文件](images/ios/swift/mobile-launch-install-openAppDelegate.png)

1. 在启动界面中，滚动到添 **[!UICONTROL 加初始化代码部分]** ，然后选择 **[!UICONTROL Swift]** ，作为所使用的iOS语言。
1. 通过单击“添加初始化代码”部分中的第一个“复 ![制](images/mobile-launch-copyIcon.png) ”图标， **[!UICONTROL 复制导入语句]** :

   ![将Swift导入语句复制到剪贴板](images/ios/swift/mobile-launch-install-copyImports.png)

1. 在Xcode中，将这些导入语句粘贴 `AppDelegate.swift` 到 `UIKit`

   ![将Swift导入语句粘贴到您的AppDelegate文件中](images/ios/swift/mobile-launch-install-pasteImports.png)

1. 在启动界面中，通过单击添加初始化代码部分中的第二个复制图标，复制与核心扩展相 ![关的两](images/mobile-launch-copyIcon.png) 行 **** 。 第一行打开控制台日志记录语句（可用选项为“debug”、“verbose”、“warning”和“error”）。 第二行指向启动环境的唯一标识符。 这很重要，因为当我们准备好将应用程序部署到生产环境时，您需要更新此值。

   ![将Core语句复制到剪贴板](images/ios/swift/mobile-launch-install-copyCore.png)

1. 在Xcode中，将这些Core语句粘贴到方法顶部的AppDelegate文 `application(_:didFinishLaunchingWithOptions:)` 件中：

   ![将Core语句粘贴到AppDelegate文件中](images/ios/swift/mobile-launch-install-pasteCore.png)

1. 在启动界面中，通过单击添加初始化代码部分中的第三个复制 ![图标](images/mobile-launch-copyIcon.png) ，复制 [!UICONTROL 扩展语句] :

   ![将Extension语句复制到剪贴板](images/ios/swift/mobile-launch-install-copyExtensions.png)

1. 在Xcode中，将这些扩展语句粘贴到AppDelegate文件中，就 `return true` 在方法行 `application(_:didFinishLaunchingWithOptions:)` 前：

   ![将Extension语句粘贴到AppDelegate文件中](images/ios/swift/mobile-launch-install-pasteExtension.png)

>[!NOTE] 启动界面中提供的移动安装说明包括标识、生命周期和信号扩展的导入和注册语句以及生命周期指标的初始化。 这些扩展被视为移动核心扩展的一部分。 如果您不希望在应用程序中使用这些扩展，则无需导入、注册或实现与这些扩展关联的其他代码。
>
> 此外，使用这些扩展时还应考虑其他实施选项（例如，当用户背景／预先启动应用程序时，可以暂停／重新启动生命周期集合）。 您可以在Mobile Core扩展文档中 [阅读有关此的更多信息](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core)

## 验证实施

1. 保存Xcode项目
1. 运行应用程序并在模拟器中启动它。 如果尚未配置任何模拟器设备，请立即配置一个，确保配置运行iOS 10+的设备。 我们喜欢使用iPhone 8模拟器，因为用鼠标单击按钮 `Home` 很容易。

   ![运行应用程序并在模拟器中启动它](images/ios/swift/mobile-launch-install-buildAndLaunch.png)

1. 等待模拟器启动并完全打开应用程序到预订屏幕（这可能需要几分钟）

   ![等待应用程序完全打开](images/ios/mobile-launch-install-simulator.png)

1. 确认正在Xcode控制台中向Adobe服务器发出调用

   ![在控制台中查找调用](images/ios/swift/mobile-launch-install-console.png)

以下是一些可查找的特定调用的示例：

1. **调用以检索启动项配置** (将控制台筛选为 `adobedtm.com`)。 请注意您在上一课中输入的扩展配置。 虽然添加扩展需要对应用程序进行更新，但可以在Launch中对这些设置进行外部管理并随时更改：

   ```swift
   2019-01-15 12:11:44.518220-0500 BusDemoSwift[52399:5056293] [AMSDK DEBUG <RulesDownloader>]: Successfully downloaded Rules from 'https://assets.adobedtm.com/launch-EN360aefc739b04410816f751a95861744-development-rules.zip'
   
   {"target.propertyToken":"","target.timeout":5,"global.privacy":"optedin","analytics.backdatePreviousSessionInfo":true,"analytics.offlineEnabled":true,"build.environment":"dev","rules.url":"https://assets.adobedtm.com/launch-EN360aefc739b04410816f751a95861744-development-rules.zip","target.clientCode":"techmarketingdemos","experienceCloud.org":"7ABB3E6A5A7491460A495D61@AdobeOrg","target.autoFetch":true,"target.fetchBackground":true,"lifecycle.sessionTimeout":300,"target.environmentId":"busbookingapp","analytics.server":"tmd.sc.omtrdc.net","analytics.rsids":"tmd-mobile-dev1","analytics.batchLimit":0,"property.id":"PRb4881271498b4f2cbaf67d38a8f3891a","global.ssl":true,"analytics.aamForwardingEnabled":true}
   ```

1. **向Identity service请求** (将控制台过滤为 `demdex.net`)在此示例中，ID(`d_mid`)已设置，且正在重新报告)

   ```swift
   2019-01-15 12:11:45.164590-0500 BusDemoSwift[52399:5056322] [AMSDK DEBUG <com.adobe.module.identity>]:
   
   Sending request (https://dpm.demdex.net/id?d_rtbd=json&d_ver=2&d_orgid=7ABB3E6A5A7491460A495D61@AdobeOrg&d_mid=17179986463578698626041670574784107777&d_blob=j8Odv6LonN4r3an7LhD3WZrU1bUpAkFkkiY1ncBR96t2PTI&dcs_region=9)
   ```

1. **来自Identity service的响应** (将控制台过滤为 `ID Service`)。 请注意该 `mid` 值如何与上述请 `d_mid` 求中的值相匹配：

   ```swift
   2019-01-15 12:11:45.681821-0500 BusDemoSwift[52399:5056322] [AMSDK DEBUG <com.adobe.module.identity>]:
   
   ID Service - Got ID Response (mid: 17179986463578698626041670574784107777, blob: j8Odv6LonN4r3an7LhD3WZrU1bUpAkFkkiY1ncBR96t2PTI, hint: 9, ttl: "604800000 ms")
   ```

1. **分析请求** (将控制台筛选到 `Analytics request`)

   ```swift
   2019-01-15 12:11:45.828465-0500 BusDemoSwift[52399:5056336] [AMSDK DEBUG <AnalyticsHitDatabase>]: Analytics request was sent with body
   
   (ndh=1&c.&a.&AppID=BusDemoSwift%201%20%281.0%29&CarrierName=%28null%29&DayOfWeek=3&DaysSinceFirstUse=0&DaysSinceLastUse=0&DeviceName=x86_64&HourOfDay=12&LaunchEvent=LaunchEvent&Launches=3&OSVersion=iOS%2012.1&Resolution=828x1792&RunMode=Application&TimeSinceLaunch=0&ignoredSessionLength=-1547572244&internalaction=Lifecycle&locale=en-US&.a&.c&aamb=j8Odv6LonN4r3an7LhD3WZrU1bUpAkFkkiY1ncBR96t2PTI&aamlh=9&ce=UTF-8&cp=foreground&mid=17179986463578698626041670574784107777&pageName=BusDemoSwift%201%20%281.0%29&pe=lnk_o&pev2=ADBINTERNAL%3ALifecycle&t=00%2F00%2F0000%2000%3A00%3A00%200%20300&ts=1547572305)
   ```

祝贺您，您已经将SDK添加到移动应用程序！

[下一个“添加Adobe Experience Platform Identity Service”&gt;](id-service.md)