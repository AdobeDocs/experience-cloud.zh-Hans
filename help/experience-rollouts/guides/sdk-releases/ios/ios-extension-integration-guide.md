---
title: 适用于iOS集成指南的Experience Rollout扩展
description: 了解如何将Experience Rollout扩展与iOS上的Adobe Experience Platform Mobile SDK集成。
source-git-commit: a9f6746c2b470377d2fd58de18e984d1ec404a77
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 7%

---

# 适用于iOS的Experience Rollout扩展 {#ios-extension-integration-guide}

本指南介绍如何将Experience Rollout扩展与iOS上的Adobe Experience Platform Mobile SDK集成。

## 先决条件 {#prerequisites}

在实施Experience Rollout扩展之前，请确保您已：

* 在[Adobe Experience Platform数据收集](https://experience.adobe.com/#/data-collection)中配置的移动属性
* 在您的移动资产中安装和配置的Experience Rollout扩展
* Adobe Experience Cloud组织ID
* 最低部署目标： iOS 12.0
* Xcode 14.1或更高版本

## 扩展依赖关系 {#extension-dependencies}

Experience Rollout扩展需要以下Adobe Experience Platform扩展：

| 扩展 | 描述 | 必需 |
|---|---|---|
| Mobile Core | 提供核心功能，包括配置和事件处理 | 是 |
| 生命周期 | 为Mobile SDK收集应用程序生命周期和会话数据 | 是 |
| Edge Network | 启用与Adobe Experience Platform Edge Network的通信 | 是 |
| Edge标识 | 管理Edge Network的用户身份 | 是 |

确保这些扩展已安装在数据收集移动资产中并包含在应用程序依赖项中。

## 在数据收集中配置Experience Rollout扩展 {#configure}

### 安装扩展 {#install-extension}

1. 登录到[Adobe Experience Platform数据收集](https://experience.adobe.com/#/data-collection)。
1. 选择&#x200B;**标记**&#x200B;选项卡并选择您的移动属性。
1. 导航到&#x200B;**扩展** > **目录**。
1. 搜索&#x200B;**Experience Rollout扩展**&#x200B;并选择&#x200B;**安装**。
1. 配置扩展设置：

   | 设置 | 描述 |
   |---|---|
   | 沙盒 | 包含您的Experience Rollout配置的Adobe Experience Platform沙盒 |
   | 应用程序Id | 您的应用程序在体验转出中的唯一标识符 |
   | 数据集 ID | 分析事件数据的Adobe Experience Platform数据集ID |

1. 选择&#x200B;**保存**。
1. 按照[发布流程](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/tags/publish/overview)更新您的配置。

### 获取环境文件ID {#environment-file-id}

1. 在移动资产中，导航到&#x200B;**环境**。
1. 为您的环境选择&#x200B;**Install**&#x200B;列下的框图标。
1. 在&#x200B;**移动设备安装说明**&#x200B;对话框中，复制&#x200B;**环境文件ID**。

## 将Experience Rollout扩展添加到应用程序 {#add-to-app}

### 添加依赖项 {#add-dependencies}

将Mobile SDK依赖项添加到您的项目中。 Experience Rollout扩展需要使用Mobile Core以及下面列出的与Edge相关的扩展。

#### 使用Swift Package Manager（推荐） {#swift-package-manager}

1. 在Xcode中，导航到&#x200B;**文件** > **添加包依赖项**。
1. 输入Adobe Experience Platform Mobile SDK存储库URL：

   ```
   https://github.com/adobe/aepsdk-core-ios
   ```

1. 添加以下包：

   | 包 | 存储库 |
   |---|---|
   | AEPCore， AEPLifecycle | `https://github.com/adobe/aepsdk-core-ios` |
   | AEPEdge | `https://github.com/adobe/aepsdk-edge-ios` |
   | AEPEdgeIdentity | `https://github.com/adobe/aepsdk-edgeidentity-ios` |
   | AEPRollout | `https://github.com/adobe/aepsdk-rollout-ios` |

#### 使用CocoaPods {#cocoapods}

将以下pod添加到您的`Podfile`：

```ruby
pod 'AEPCore'
pod 'AEPLifecycle'
pod 'AEPEdge'
pod 'AEPEdgeIdentity'
pod 'AEPRollout'
```

然后运行：

```bash
pod install
```

>[!IMPORTANT]
>
>对于生产应用程序，Adobe建议固定到显式版本号，而不是使用`~>`或开放范围。 有关详细信息，请参阅[CocoaPods版本控制指南](https://guides.cocoapods.org/using/the-podfile.html)。

### 初始化SDK {#initialize-sdk}

在调用任何Experience Rollout扩展API之前，在`AppDelegate`（或`SceneDelegate`）中初始化Mobile SDK。 使用您的移动资产中的环境文件ID，以便应用程序会选取您在Data Collection中发布的转出设置。

**Swift**

```swift
import AEPCore
import AEPLifecycle
import AEPEdge
import AEPEdgeIdentity
import AEPRollout

@main
class AppDelegate: UIResponder, UIApplicationDelegate {

    func application(
        _ application: UIApplication,
        didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
    ) -> Bool {

        MobileCore.setLogLevel(.error)

        MobileCore.registerExtensions(
            [Lifecycle.self, Edge.self, Identity.self, Rollout.self]
        ) {
            // Initialize with your Environment File ID from Data Collection
            MobileCore.configureWith(appId: "YOUR_ENVIRONMENT_FILE_ID")
        }

        return true
    }
}
```

**Objective-C**

```objc
@import AEPCore;
@import AEPLifecycle;
@import AEPEdge;
@import AEPEdgeIdentity;
@import AEPRollout;

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application
    didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    [AEPMobileCore setLogLevel:AEPLogLevelError];

    NSArray *extensions = @[
        AEPMobileLifecycle.class,
        AEPMobileEdge.class,
        AEPMobileEdgeIdentity.class,
        AEPMobileRollout.class
    ];

    [AEPMobileCore registerExtensions:extensions completion:^{
        // Initialize with your Environment File ID from Data Collection
        [AEPMobileCore configureWithAppId:@"YOUR_ENVIRONMENT_FILE_ID"];
    }];

    return YES;
}

@end
```

>[!IMPORTANT]
>
>对于生产应用，仅使用`LogLevel.error`。 请勿在版本内部版本中使用`.debug`或`.verbose`。

## 评估上下文 {#evaluation-context}

`FeatureEvaluationContext`包括定位属性（用于转出规则匹配）和可选标识（用于analytics）。

| 方法 | 必需 | 描述 |
|---|---|---|
| `withIdentity(namespace:id:)` | 否 | 第一个参数：身份命名空间（请参阅[Adobe身份命名空间](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/identity/features/namespaces)）。 第二个参数：标识值。 当您希望该命名空间和ID在Analytics中用于此评估时，请包括此项。 如果未提供，则Analytics默认使用ECID。 这不会用于制定功能启用决策。 |
| `withAttributes(_:)` | 否 | `[String: [String]]`. 键值是转出规则使用的上下文属性名称（例如`locale`、`platform`、`appVersion`、`deviceType`）。 值是当前用户/会话的该键的候选属性值列表（例如`["en_US"]`或`["phone"]`）。 |

**Swift**

```swift
import AEPRollout

let attrs: [String: [String]] = [
    "locale": ["en_US"],
    "platform": ["IOS"],
    "appVersion": ["3.0.0"]
]

let ctx = FeatureEvaluationContext.builder()
    .withIdentity(namespace: "Email", id: "customer@example.com")
    .withAttributes(attrs)
    .build()
```

**Objective-C**

```objc
@import AEPRollout;

NSDictionary<NSString *, NSArray<NSString *> *> *attrs = @{
    @"locale": @[@"en_US"],
    @"platform": @[@"IOS"],
    @"appVersion": @[@"3.0.0"]
};

AEPFeatureEvaluationContext *ctx = [[[AEPFeatureEvaluationContextBuilder builder]
    withIdentityNamespace:@"Email" id:@"customer@example.com"]
    withAttributes:attrs]
    .build;
```

### 定位属性示例 {#sample-attributes}

| 属性 | 描述 | 示例值 |
|---|---|---|
| `locale` | 用户的区域设置/语言 | `["en_US"]`, `["fr_FR"]` |
| `platform` | 平台标识符 | `["IOS"]` |
| `appVersion` | 应用程序版本 | `["3.0.0"]` |
| `deviceType` | 设备类型 | `["phone"]`, `["tablet"]` |

## API 参考 {#api-reference}

### isFeatureEnable {#is-feature-enabled}

`isFeatureEnabled`返回给定上下文的体验转出功能是打开还是关闭。 传递`featureKey`、`FeatureEvaluationContext`（可选的定位属性和可选的标识，适用于Analytics）和完成处理程序。 查看[评估上下文](#evaluation-context)。

**签名**

*Swift*

```swift
Rollout.isFeatureEnabled(
    featureKey: String,
    evaluationContext: FeatureEvaluationContext,
    completion: @escaping (Bool) -> Void
)
```

*Objective-C*

```objc
[AEPMobileRollout isFeatureEnabled:(NSString *)featureKey
               evaluationContext:(AEPFeatureEvaluationContext *)evaluationContext
                      completion:(void (^)(BOOL))completion];
```

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `featureKey` | 字符串 | 要在Experience转出中评估的功能键 |
| `evaluationContext` | FeatureEvaluationContext | 根据需要包括目标属性和分析的可选标识；将`FeatureEvaluationContext.builder().build()`用于空上下文。 查看[评估上下文](#evaluation-context)。 |
| `completion` | `(Bool) -> Void` | 如果功能已启用，则通过`true`调用，否则通过`false`调用。 |

**示例**

*Swift*

```swift
import AEPRollout

Rollout.isFeatureEnabled(
    featureKey: "new-checkout-experience",
    evaluationContext: ctx
) { isEnabled in
    if isEnabled {
        showNewCheckout()
    } else {
        showDefaultCheckout()
    }
}
```

*Objective-C*

```objc
@import AEPRollout;

[AEPMobileRollout isFeatureEnabled:@"new-checkout-experience"
               evaluationContext:ctx
                      completion:^(BOOL isEnabled) {
    if (isEnabled) {
        [self showNewCheckout];
    } else {
        [self showDefaultCheckout];
    }
}];
```

### getFeature {#get-feature}

`getFeature`针对提供的上下文返回已评估的功能有效负载。 当您需要启用/禁用以外的功能，并且需要功能元数据或值时，请使用此API。

**签名**

*Swift*

```swift
Rollout.getFeature(
    featureKey: String,
    evaluationContext: FeatureEvaluationContext,
    completion: @escaping (FeatureEvaluationResult?) -> Void
)
```

*Objective-C*

```objc
[AEPMobileRollout getFeature:(NSString *)featureKey
         evaluationContext:(AEPFeatureEvaluationContext *)evaluationContext
                completion:(void (^)(AEPFeatureEvaluationResult * _Nullable))completion];
```

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `featureKey` | 字符串 | 要在Experience转出中评估的功能键 |
| `evaluationContext` | FeatureEvaluationContext | 根据需要包括目标属性和分析的可选标识；将`FeatureEvaluationContext.builder().build()`用于空上下文。 查看[评估上下文](#evaluation-context)。 |
| `completion` | `(FeatureEvaluationResult?) -> Void` | 使用评估的功能有效负载调用；当未找到该功能时，可能为`nil`。 |

**响应**

*FeatureEvaluationResult*

| 字段 | 类型 | 描述 |
|---|---|---|
| `id` | 整数 | 数字功能标识符 |
| `key` | 字符串 | 功能键 |
| `releaseKey` | 字符串？ | 此功能的发行密钥（可用时） |
| `meta` | 字符串？ | 在可用时以JSON字符串形式提供功能元数据 |
| `analyticsParam` | AnalyticsParam？ | 已评估功能的Analytics详细信息 |

*AnalyticsParam*

| 字段 | 类型 | 描述 |
|---|---|---|
| `releaseId` | 整数 | 数字发行标识符 |
| `featureId` | 整数 | 数字功能标识符 |
| `variantId` | 字符串？ | 变量标识符 |

**示例**

*Swift*

```swift
import AEPRollout

Rollout.getFeature(
    featureKey: "new-checkout-experience",
    evaluationContext: ctx
) { feature in
    if let meta = feature?.meta, !meta.isEmpty {
        applyMetaDrivenExperience(meta)
    } else {
        showFallbackExperience()
    }
}
```

*Objective-C*

```objc
@import AEPRollout;

[AEPMobileRollout getFeature:@"new-checkout-experience"
         evaluationContext:ctx
                completion:^(AEPFeatureEvaluationResult * _Nullable feature) {
    NSString *meta = feature.meta;
    if (meta != nil && meta.length > 0) {
        [self applyMetaDrivenExperience:meta];
    } else {
        [self showFallbackExperience];
    }
}];
```

### refreshcache {#refresh-cache}

默认情况下，Experience Rollout扩展会按照您可以配置的计划定期从服务器同步最新转出规则和功能。 如果您需要比下一次计划同步更早的更新，请调用`refreshCache`以强制刷新。 典型案例包括登录后或应用程序状态发生变化而影响定位。

**语法**

*Swift*

```swift
Rollout.refreshCache()
```

*Objective-C*

```objc
[AEPMobileRollout refreshCache];
```

### extensionVersion {#extension-version}

返回Experience Rollout扩展的版本字符串。

**语法**

```swift
Rollout.extensionVersion(): String
```

**示例**

*Swift*

```swift
let version = Rollout.extensionVersion()
```

*Objective-C*

```objc
NSString *version = [AEPMobileRollout extensionVersion];
```

## API摘要 {#api-summary}

| API | 返回值 |
|---|---|
| `isFeatureEnabled(featureKey:evaluationContext:completion:)`. `FeatureEvaluationContext`携带规则的定位属性和analytics的可选标识。 请参阅[isFeatureEnabled](#is-feature-enabled)。 | 通过完成处理程序进行bool |
| `getFeature(featureKey:evaluationContext:completion:)`. 返回给定上下文的已评估功能有效负载。 请参阅[getFeature](#get-feature)。 | 功能评估结果？ 通过完成处理程序 |
| `refreshCache()` | 空白 |
| `extensionVersion()` | 字符串 |

## 另请参阅 {#see-also}

* [移动设备应用程序](../../integrate/mobile-applications.md)
* [集成步骤](../../integrate/integration-steps.md)
* [SDK](../../integrate/sdks.md)
* [Android扩展集成指南](../android/android-extension-integration-guide.md)
