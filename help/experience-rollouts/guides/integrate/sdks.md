---
title: SDK
description: 了解Adobe Experience Rollout中的SDK架构以及适用于Java和Node.js的可用SDK。
exl-id: 110a440d-b52a-4e1e-a94f-86f9741a223a
source-git-commit: 2a946868f58e25f8aafbf3ccfcf6571e7d0d8d20
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 2%

---

# SDK {#sdks}

Experience转出为后端服务集成提供了服务器端SDK。 本页介绍SDK架构和可用选项。

## SDK架构 {#architecture}

所有Experience Rollout SDK共享相同的核心架构：

* **初始化** — SDK是通过返回单个对象的`createInstance()`调用配置的。
* **功能检索** — `getFeatures()`方法从SDK中检索功能标志数据。
* **缓存** — SDK将缓存来自Experience Rollout服务的响应。 高速缓存管理器以可配置的轮询间隔(TTL)刷新高速缓存。
* **错误处理** — 如果服务返回503，则缓存管理器将保留现有的缓存数据并继续提供功能标志评估。 如果自上次调用(304)以来数据没有改变，则不更新缓存。

## 先决条件 {#prerequisites}

在集成SDK之前，请确保您具备以下条件：

1. **应用程序ID** — 已载入体验转出控制台中的每个应用程序的客户端ID。
2. **服务令牌** — SDK用于在后台调用Experience Rollout API。
3. **API密钥** — 与用于API身份验证的服务令牌一起使用。

## 可用SDK {#available-sdks}

### Java SDK {#java-sdk}

Java SDK通过Maven进行分发。 将依赖项添加到项目的`pom.xml`以进行集成。 对于基于Spring的应用程序，Maven依赖关系会在应用程序完全加载之前自动设置SDK缓存。

Java SDK的关键规范：

* **支持的JDK：** JDK 8及更高版本
* **不可缓存的客户端：**&#x200B;从SDK版本0.8开始支持。 对于不可缓存的客户端，`getFeature()`会进行实时API调用，而不是从缓存中读取。 SDK继续在后台轮询，如果客户端变为可缓存，则切换到基于缓存的服务。

有关设置说明，请参阅[Java SDK集成指南](../sdk-releases/java/java-sdk-integration-guide.md)。

### Node.js SDK {#nodejs-sdk}

Node.js SDK通过npm进行分发。

有关设置说明，请参阅[Node.js SDK集成指南](../sdk-releases/nodejs/nodejs-sdk-integration-guide.md)。

## 另请参阅 {#see-also}

* [Web 服务](web-services.md)
* [集成步骤](integration-steps.md)
* [Java SDK集成指南](../sdk-releases/java/java-sdk-integration-guide.md)
* [Node.js SDK集成指南](../sdk-releases/nodejs/nodejs-sdk-integration-guide.md)
