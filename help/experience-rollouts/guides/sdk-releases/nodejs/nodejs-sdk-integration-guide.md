---
title: Node.js SDK集成指南
description: 了解如何将Experience Rollouts Node.js SDK集成到您的后端服务中，以检索和评估功能标记。
source-git-commit: 9bfe0e55e89c1d7fbd77cde63831a6a186820e24
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 1%

---


# Node.js SDK集成指南 {#nodejs-sdk-integration-guide}

Experience Rollouts Node.js SDK是适用于Node.js服务的服务器端库。 它可以在本地缓存功能标记数据，并在每个请求上评估标记，而无需同步API调用。

>[!NOTE]
>
>Node.js SDK仅供服务器端使用。 对于客户端Web应用程序，直接调用功能API V3 REST端点。

## 先决条件 {#prerequisites}

在集成Node.js SDK之前，请确保您已：

* Node.js服务器端应用程序
* 通过Adobe Developer Console获得的&#x200B;**API密钥**&#x200B;和&#x200B;**服务令牌** — 请参阅[订阅API应用程序](../../integrate/subscribe-to-api-application.md)
* 您的&#x200B;**应用程序客户端ID**&#x200B;已在Experience Rollout控制台中注册 — 请参阅[将您的应用程序载入](../../applications/onboard-your-application.md)

## 安装SDK {#install}

将SDK添加到您项目的`package.json`：

```json
"@floodgate/fg-client-sdk": "~1.0.10"
```

然后在您的代码中需要它：

```javascript
const { floodgateClient } = require('@floodgate/fg-client-sdk');
```

## 初始化SDK {#initialize}

应用程序启动时调用`createInstance()`一次：

```javascript
floodgateClient.createInstance(
  {
    adobeIoApiKey: "<YOUR_API_KEY>",
    clientIds: ["<CLIENT_ID_1>", "<CLIENT_ID_2>"],
    env: "PRD",    // Use "STG" for Stage
    featureRequestHttpParams: {
      timeout: 60 * 1000  // Optional: request timeout in ms
    },
    ingestAnalyticsHttpParams: {
      timeout: 5 * 1000   // Optional: analytics timeout in ms
    }
  },
  function(cb) {
    // Fetch a fresh service token from IMS and pass it in the callback
    cb(null, SERVICE_TOKEN);
  },
  function() {
    return true;  // Return false to disable analytics
  },
  function(response) {
    // Called when the SDK initializes successfully
    console.log("SDK initialized");
  },
  function(err) {
    // Called if initialization fails
    console.error("SDK init error:", err);
  }
);
```

## 检索功能标志 {#retrieve-features}

功能标志在回调中异步返回。 根据用户上下文选择适当的方法。

### 经过身份验证的用户 {#authenticated-user}

```javascript
floodgateClient.getFeatures(
  {
    userAccessToken: "<USER_ACCESS_TOKEN>",
    visitorId: "<VISITOR_ID>",
    clientId1: "<CLIENT_ID>",
    meta: true
  },
  function(err, features) {
    if (err) {
      // Handle error and serve default experience
      return;
    }
    const isEnabled = floodgateClient.isFeatureEnabled(features, "MY_FEATURE_FLAG");
    // Serve experience based on isEnabled
  }
);
```

### 匿名用户 {#anonymous-user}

当没有可用的用户访问令牌时，使用版本标记或忽略该令牌以接收完整转出版本：

```javascript
floodgateClient.getFeatures(
  {
    releaseFlag: "<RELEASE_FLAG>",
    visitorId: "<VISITOR_ID>",
    clientId1: "<CLIENT_ID>",
    meta: false
  },
  callback
);
```

### 默认完全转出版本 {#default-releases}

如果既未提供访问令牌也未提供发布标志，则SDK将返回处于&#x200B;**完全转出**&#x200B;或&#x200B;**基线**&#x200B;状态的功能：

```javascript
floodgateClient.getFeatures(
  {
    clientId1: "<CLIENT_ID>",
    visitorId: "<VISITOR_ID>",
    meta: false
  },
  callback
);
```

## 检查功能是否已启用 {#check-feature}

```javascript
const isEnabled = floodgateClient.isFeatureEnabled(features, "MY_FEATURE_FLAG");

if (isEnabled) {
  // Serve the new experience
} else {
  // Serve the default experience
}
```

## 启用调试日志记录 {#debug-logging}

要启用详细的SDK日志，请在调用`createInstance()`时传递调试级别日志程序实例：

```javascript
const bunyan = require('bunyan');
const logger = bunyan.createLogger({ name: "fg", sourceType: "SDK", level: "debug" });

floodgateClient.createInstance(
  { ..., log: logger },
  ...
);
```

## 另请参阅 {#see-also}

* [Node.js SDK发行说明](nodejs-sdk-release-notes.md)
* [SDK](../../integrate/sdks.md)
* [订阅API应用程序](../../integrate/subscribe-to-api-application.md)
* [集成步骤](../../integrate/integration-steps.md)
