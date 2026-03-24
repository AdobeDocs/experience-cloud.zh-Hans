---
title: Java SDK集成指南
description: 了解如何将Experience Rollouts Java SDK集成到您的后端服务中，以检索和评估功能标记。
source-git-commit: 9bfe0e55e89c1d7fbd77cde63831a6a186820e24
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 1%

---


# Java SDK集成指南 {#java-sdk-integration-guide}

Experience Rollouts Java SDK是一个服务器端库，它可以在本地缓存功能标志数据并评估标志，而无需在每个请求上同步API调用。 本指南涵盖当前的SDK (4.x)。

## 先决条件 {#prerequisites}

在集成Java SDK之前，请确保您已：

* JDK 11或更高版本（从SDK版本3.0.0开始，需要；以前的版本支持JDK 8+）
* 基于Maven的构建系统
* 您的Adobe Developer Console项目中的&#x200B;**API密钥**&#x200B;和&#x200B;**服务令牌**&#x200B;客户端ID — 请参阅[订阅API应用程序](../../integrate/subscribe-to-api-application.md)
* 您的&#x200B;**应用程序客户端ID**&#x200B;已在Experience Rollout控制台中注册 — 请参阅[将您的应用程序载入](../../applications/onboard-your-application.md)

## 添加Maven依赖项 {#maven-dependency}

将体验转出Java SDK添加到您项目的`pom.xml`：

```xml
<dependency>
  <groupId>com.adobe.cloudtech</groupId>
  <artifactId>fg-client-sdk</artifactId>
  <version>4.0.6</version>
</dependency>
```

## 初始化SDK {#initialize}

使用`FloodgateClient.createInstance()`在应用程序启动时初始化SDK一次。 该方法采用您使用配置生成器生成的`FloodgateConfiguration`对象。

### 实施服务令牌回调 {#service-token-callback}

SDK在运行时使用回调接口检索新的服务令牌：

```java
private class FgConfigCallBack implements FGConfigBaseCallBack {

  @Override
  public String getIMSServiceToken() {
    // Fetch and return a valid service token
  }

  @Override
  public boolean isAnalyticsEnabled() {
    return false; // Set to true to enable analytics
  }
}
```

### 创建配置对象 {#configuration}

使用配置生成器设置SDK：

```java
FloodgateConfiguration configuration = FloodgateConfiguration.FloodgateConfigurationBuilder
    .aFloodgateConfiguration(
        FgEnv.PRD,                   // Use FgEnv.STG for Stage
        "<YOUR_API_KEY>",
        Set.of("<CLIENT_ID_1>", "<CLIENT_ID_2>"),
        new FgConfigCallBack(),
        CallType.ASYNC
    )
    .withRetryPolicy(retryPolicy)    // Optional: defaults to 5 retries, 10s interval
    .build();
```

将`FgEnv.STG`用于暂存环境，将`FgEnv.PRD`用于生产。

### 创建客户端实例 {#client-instance}

```java
FloodgateClient fgClient = FloodgateClient.createInstance(configuration);
```

## 检索功能标志 {#retrieve-features}

### 经过身份验证的用户 {#authenticated-user}

使用IMS访问令牌检索当前用户的功能标记：

```java
GetFeatureRequest request = GetFeatureRequestBuilder
    .aGetFeatureRequest("<CLIENT_ID>")
    .withAccessToken("<USER_ACCESS_TOKEN>")
    .withContext(context)
    .build();

FeaturesResponse[] features = fgClient.getFeatures(request);
```

### 匿名用户 {#anonymous-user}

对于未经身份验证的用户，请传递访客ID和服务令牌：

```java
GetFeatureRequest request = GetFeatureRequestBuilder
    .aGetFeatureRequest("<CLIENT_ID>")
    .withServiceToken("<SERVICE_TOKEN>")
    .withVisitorId("<VISITOR_ID>")
    .withContext(context)
    .build();

FeaturesResponse[] features = fgClient.getFeatures(request);
```

### 检索特定功能标志或版本 {#specific-feature}

要按键检索单个功能标记，请执行以下操作：

```java
GetFeatureRequest request = GetFeatureRequestBuilder
    .aGetFeatureRequest("<CLIENT_ID>")
    .withAccessToken("<ACCESS_TOKEN>")
    .withFeatureKey("<FEATURE_KEY>")
    .build();
```

要按发行版密钥检索，请将`.withFeatureKey()`替换为`.withReleaseKey()`。

## 检查功能是否已启用 {#check-feature}

```java
boolean isEnabled = FloodgateClient.isFeatureEnabled(features, "MY_FEATURE_FLAG");

if (isEnabled) {
  // Serve the new experience
} else {
  // Serve the default experience
}
```

对于基于发行版的检查：

```java
boolean isEnabled = FloodgateClient.isFeatureEnabled(features, "MY_RELEASE", "MY_FEATURE_FLAG");
```

## 缓存管理 {#cache-management}

SDK将缓存功能标志数据，并在控制台中为每个应用程序设置的轮询间隔内刷新该数据。 要触发按需缓存刷新，请执行以下操作：

```java
fgClient.refreshClientCache("<CLIENT_ID>");
```

### 不可缓存的客户端 {#non-cacheable}

对于不可缓存的客户端，`getFeature()`每次都进行实时API调用。 当客户端变得可缓存时，SDK会继续后台轮询并切换到基于缓存的服务。 从SDK版本0.8开始支持。

## 配置选项 {#configuration-options}

生成器上提供了以下可选配置方法：

| 选项 | 方法 | 描述 |
|---|---|---|
| 始终使用缓存 | `.alwaysCache()` | 绕过来自API的缓存响应；用于没有受众规则的标记 |
| 禁用缓存 | `.neverCache()` | 禁用默认缓存；对自定义缓存刷新逻辑很有用 |
| 自定义HTTP客户端 | `.withHttpClient(client)` | 使用您自己的HTTP客户端 |
| 自定义执行器 | `.withScheduledExecutorService(executor)` | 使用您自己的计划执行器进行后台轮询 |
| 包括对照组 | `.includeControlGroup()` | 在功能响应中返回控制组数据 |

## 处理错误 {#error-handling}

自动换行`getFeatures()`调用以捕获SDK异常：

```java
try {
  features = fgClient.getFeatures(request);
} catch (FgClientException e) {
  int statusCode = e.getStatusCode();
  // Handle error and serve default experience
} catch (FgInitException e) {
  e.printStackTrace();
}
```

## 另请参阅 {#see-also}

* [Java SDK发行说明](java-sdk-release-notes.md)
* [SDK](../../integrate/sdks.md)
* [订阅API应用程序](../../integrate/subscribe-to-api-application.md)
* [集成步骤](../../integrate/integration-steps.md)
