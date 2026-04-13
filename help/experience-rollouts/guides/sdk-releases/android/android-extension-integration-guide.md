---
title: 适用于Android集成指南的Experience Rollout扩展
description: 了解如何将Experience Rollout扩展与Android上的Adobe Experience Platform Mobile SDK集成。
hide: true
exl-id: 683ef4d4-e637-4b7b-b694-689c7e65a99e
source-git-commit: 12032cbed45e694a3f25f16afe80308b3eb82924
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 7%

---

# 适用于Android的Experience Rollout扩展 {#android-extension-integration-guide}

本指南介绍如何将Experience Rollout扩展与Android上的Adobe Experience Platform Mobile SDK集成。

## 先决条件 {#prerequisites}

在实施Experience Rollout扩展之前，请确保您已：

* 在[Adobe Experience Platform数据收集](https://experience.adobe.com/#/data-collection)中配置的移动属性
* 在您的移动资产中安装和配置的Experience Rollout扩展
* Adobe Experience Cloud组织ID
* 最小SDK：API 21 (Android 5.0 Lollipop)

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
1. 按照[发布流程](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/overview)更新您的配置。

### 获取环境文件ID {#environment-file-id}

1. 在移动资产中，导航到&#x200B;**环境**。
1. 为您的环境选择&#x200B;**Install**&#x200B;列下的框图标。
1. 在&#x200B;**移动设备安装说明**&#x200B;对话框中，复制&#x200B;**环境文件ID**。

## 将Experience Rollout扩展添加到应用程序 {#add-to-app}

### 添加依赖项 {#add-dependencies}

将Mobile SDK依赖项添加到您的项目中。 Experience Rollout扩展需要使用Mobile Core以及下面列出的与Edge相关的扩展。

#### 将Gradle与BOM结合使用（推荐） {#gradle-bom}

将以下依赖项添加到应用程序的`build.gradle.kts`文件中：

```kotlin
dependencies {
    // Adobe Experience Platform Mobile SDK BOM
    implementation(platform("com.adobe.marketing.mobile:sdk-bom:3.+"))

    // Required extensions
    implementation("com.adobe.marketing.mobile:core")
    implementation("com.adobe.marketing.mobile:lifecycle")
    implementation("com.adobe.marketing.mobile:edge")
    implementation("com.adobe.marketing.mobile:edgeidentity")

    // Experience Rollout extension
    implementation("com.adobe.marketing.mobile:rollout")
}
```

#### 使用Gradle (Groovy) {#gradle-groovy}

```groovy
dependencies {
    // Adobe Experience Platform Mobile SDK BOM
    implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')

    // Required extensions
    implementation 'com.adobe.marketing.mobile:core'
    implementation 'com.adobe.marketing.mobile:lifecycle'
    implementation 'com.adobe.marketing.mobile:edge'
    implementation 'com.adobe.marketing.mobile:edgeidentity'

    // Experience Rollout extension
    implementation 'com.adobe.marketing.mobile:rollout'
}
```

>[!IMPORTANT]
>
>对于生产应用程序，Adobe建议使用显式版本号而不是动态版本。 有关详细信息，请参阅[管理Gradle依赖项](https://docs.gradle.org/current/userguide/dependency_management.html)。

### 添加权限 {#add-permissions}

向您的`AndroidManifest.xml`文件添加以下权限：

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

### 初始化SDK {#initialize-sdk}

在调用任何Experience Rollout扩展API之前，初始化`Application`类中的Mobile SDK。 将移动属性中的环境文件ID与`MobileCore.initialize`一起使用，以便应用程序选取您在数据收集中发布的转出设置。

#### 使用MobileCore.initialize {#mobile-core-initialize}

从Android BOM版本3.8.0开始提供此API，它自动注册扩展并启用生命周期跟踪。

>[!IMPORTANT]
>
>对于生产应用，仅使用`LoggingMode.ERROR`。 请勿在版本内部版本中使用`DEBUG`或`VERBOSE`。

**Kotlin**

```kotlin
import android.app.Application
import com.adobe.marketing.mobile.LoggingMode
import com.adobe.marketing.mobile.MobileCore

class MainApplication : Application() {

    override fun onCreate() {
        super.onCreate()

        MobileCore.setLogLevel(LoggingMode.ERROR)

        // Initialize with your Environment File ID from Data Collection
        MobileCore.initialize(this, "YOUR_ENVIRONMENT_FILE_ID")
    }
}
```

**Java**

```java
import android.app.Application;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;

public class MainApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();

        MobileCore.setLogLevel(LoggingMode.ERROR);

        // Initialize with your Environment File ID from Data Collection
        MobileCore.initialize(this, "YOUR_ENVIRONMENT_FILE_ID", null);
    }
}
```

### 注册Application类 {#register-application}

在`AndroidManifest.xml`中注册您的`Application`类：

```xml
<application
    android:name=".MainApplication"
    ... >
</application>
```

## 评估上下文 {#evaluation-context}

`FeatureEvaluationContext`包括定位属性（用于转出规则匹配）和可选标识（用于analytics）。

| 方法 | 必需 | 描述 |
|---|---|---|
| `withIdentity(namespace, id)` | 否 | 第一个参数：身份命名空间（请参阅[Adobe身份命名空间](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/identity/features/namespaces)）。 第二个参数：标识值。 当您希望该命名空间和ID在Analytics中用于此评估时，请包括此项。 如果未提供，则Analytics默认使用ECID。 这不会用于制定功能启用决策。 |
| `withAttributes(map)` | 否 | `Map<String, List<String>>`. 键值是转出规则使用的上下文属性名称（例如`locale`、`platform`、`appVersion`、`deviceType`）。 值是当前用户/会话的该键的候选属性值列表（例如`["en_US"]`或`["phone"]`）。 |

**Kotlin**

```kotlin
import com.adobe.marketing.mobile.rollout.FeatureEvaluationContext

val attrs = mapOf(
    "locale" to listOf("en_US"),
    "platform" to listOf("ANDROID"),
    "appVersion" to listOf("3.0.0")
)

val ctx = FeatureEvaluationContext.builder()
    .withIdentity("Email", "customer@example.com")
    .withAttributes(attrs)
    .build()
```

**Java**

```java
import com.adobe.marketing.mobile.rollout.FeatureEvaluationContext;
import java.util.Arrays;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

Map<String, List<String>> attrs = new HashMap<>();
attrs.put("locale", Arrays.asList("en_US"));
attrs.put("platform", Arrays.asList("ANDROID"));
attrs.put("appVersion", Arrays.asList("3.0.0"));

FeatureEvaluationContext ctx = FeatureEvaluationContext.builder()
        .withIdentity("Email", "customer@example.com")
        .withAttributes(attrs)
        .build();
```

### 定位属性示例 {#sample-attributes}

| 属性 | 描述 | 示例值 |
|---|---|---|
| `locale` | 用户的区域设置/语言 | `["en_US"]`, `["fr_FR"]` |
| `platform` | 平台标识符 | `["ANDROID"]` |
| `appVersion` | 应用程序版本 | `["3.0.0"]` |
| `deviceType` | 设备类型 | `["phone"]`, `["tablet"]` |

## API 参考 {#api-reference}

### isFeatureEnable {#is-feature-enabled}

`isFeatureEnabled`返回给定上下文的体验转出功能是打开还是关闭。 传递`featureKey`、`FeatureEvaluationContext`（可选定位属性和可选标识，适用于Analytics）和回调。 查看[评估上下文](#evaluation-context)。

**签名**

*Kotlin*

```kotlin
Rollout.isFeatureEnabled(
    featureKey: String,
    evaluationContext: FeatureEvaluationContext,
    callback: AdobeCallback<Boolean>
)
```

*Java*

```java
Rollout.isFeatureEnabled(
    String featureKey,
    FeatureEvaluationContext evaluationContext,
    AdobeCallback<Boolean> callback);
```

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `featureKey` | 字符串 | 要在Experience转出中评估的功能键 |
| `evaluationContext` | FeatureEvaluationContext | 根据需要包括目标属性和分析的可选标识；将`FeatureEvaluationContext.builder().build()`用于空上下文。 查看[评估上下文](#evaluation-context)。 |
| `callback` | AdobeCallback&lt;布尔值> | 如果功能已启用，则通过`true`调用，否则通过`false`调用。 您还可以传递`AdobeCallbackWithError<Boolean>`以处理`fail(...)`。 |

**示例**

*Kotlin*

```kotlin
import com.adobe.marketing.mobile.AdobeCallback
import com.adobe.marketing.mobile.rollout.Rollout

Rollout.isFeatureEnabled(
    "new-checkout-experience",
    ctx,
    object : AdobeCallback<Boolean> {
        override fun call(isEnabled: Boolean?) {
            if (isEnabled == true) {
                showNewCheckout()
            } else {
                showDefaultCheckout()
            }
        }
    }
)
```

*Java*

```java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.rollout.Rollout;

Rollout.isFeatureEnabled(
    "new-checkout-experience",
    ctx,
    new AdobeCallback<Boolean>() {
        @Override
        public void call(Boolean isEnabled) {
            if (Boolean.TRUE.equals(isEnabled)) {
                showNewCheckout();
            } else {
                showDefaultCheckout();
            }
        }
    }
);
```

### getFeature {#get-feature}

`getFeature`针对提供的上下文返回已评估的功能有效负载。 当您需要启用/禁用以外的功能，并且需要功能元数据或值时，请使用此API。

**签名**

*Kotlin*

```kotlin
Rollout.getFeature(
    featureKey: String,
    evaluationContext: FeatureEvaluationContext,
    callback: AdobeCallback<FeatureEvaluationResult>
)
```

*Java*

```java
Rollout.getFeature(
    String featureKey,
    FeatureEvaluationContext evaluationContext,
    AdobeCallback<FeatureEvaluationResult> callback);
```

**参数**

| 参数 | 类型 | 描述 |
|---|---|---|
| `featureKey` | 字符串 | 要在Experience转出中评估的功能键 |
| `evaluationContext` | FeatureEvaluationContext | 根据需要包括目标属性和分析的可选标识；将`FeatureEvaluationContext.builder().build()`用于空上下文。 查看[评估上下文](#evaluation-context)。 |
| `callback` | AdobeCallback&lt;功能评估结果> | 使用评估的功能有效负载调用；当未找到该功能时，可能为`null`。 您还可以传递`AdobeCallbackWithError<FeatureEvaluationResult>`以处理`fail(...)`。 |

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

*Kotlin*

```kotlin
import com.adobe.marketing.mobile.AdobeCallback
import com.adobe.marketing.mobile.rollout.FeatureEvaluationResult
import com.adobe.marketing.mobile.rollout.Rollout

Rollout.getFeature(
    "new-checkout-experience",
    ctx,
    object : AdobeCallback<FeatureEvaluationResult> {
        override fun call(feature: FeatureEvaluationResult?) {
            val meta = feature?.meta
            if (!meta.isNullOrEmpty()) {
                applyMetaDrivenExperience(meta)
            } else {
                showFallbackExperience()
            }
        }
    }
)
```

*Java*

```java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.rollout.FeatureEvaluationResult;
import com.adobe.marketing.mobile.rollout.Rollout;

Rollout.getFeature(
    "new-checkout-experience",
    ctx,
    new AdobeCallback<FeatureEvaluationResult>() {
        @Override
        public void call(FeatureEvaluationResult feature) {
            String meta = feature != null ? feature.getMeta() : null;
            if (meta != null && !meta.isEmpty()) {
                applyMetaDrivenExperience(meta);
            } else {
                showFallbackExperience();
            }
        }
    }
);
```

### refreshcache {#refresh-cache}

默认情况下，Experience Rollout扩展会按照您可以配置的计划定期从服务器同步最新转出规则和功能。 如果您需要比下一次计划同步更早的更新，请调用`refreshCache`以强制刷新。 典型案例包括登录后或应用程序状态发生变化而影响定位。

**语法**

*Kotlin*

```kotlin
Rollout.refreshCache()
```

*Java*

```java
Rollout.refreshCache();
```

### extensionVersion {#extension-version}

返回Experience Rollout扩展的版本字符串。

**语法**

```kotlin
Rollout.extensionVersion(): String
```

**示例**

*Kotlin*

```kotlin
val version = Rollout.extensionVersion()
```

*Java*

```java
String version = Rollout.extensionVersion();
```

## API摘要 {#api-summary}

| API | 返回值 |
|---|---|
| `isFeatureEnabled(featureKey, evaluationContext, callback)`. `FeatureEvaluationContext`携带规则的定位属性和analytics的可选标识。 请参阅[功能评估](#is-feature-enabled)。 | 通过回调的布尔值 |
| `getFeature(featureKey, evaluationContext, callback)`. 返回给定上下文的已评估功能有效负载。 请参阅[getFeature](#get-feature)。 | 通过回调的FeatureEvaluationResult |
| `refreshCache()` | 空白 |
| `extensionVersion()` | 字符串 |

## 另请参阅 {#see-also}

* [移动设备应用程序](../../integrate/mobile-applications.md)
* [集成步骤](../../integrate/integration-steps.md)
* [SDK](../../integrate/sdks.md)

<!-- -->
