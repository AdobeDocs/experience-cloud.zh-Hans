---
title: SDK
description: 了解Adobe Experience Rollout中的SDK架构以及Android可用的移动SDK扩展。
exl-id: 110a440d-b52a-4e1e-a94f-86f9741a223a
source-git-commit: fcb1d36fc92b3954a902d818a98f579672c577e9
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 3%

---

# SDK {#sdks}

Experience Rollout提供了用于将功能标记集成到应用程序中的SDK。 本页介绍SDK架构和可用选项。

## SDK架构 {#architecture}

所有Experience Rollout SDK共享相同的核心架构：

* **初始化** — SDK在启动时配置，并向Experience Rollout服务注册。
* **功能检索** — SDK检索功能标志数据并在本地评估标志。
* **正在缓存** — SDK将缓存功能标志数据，并在可配置的轮询间隔(TTL)上刷新该数据。
* **错误处理** — 如果该服务不可用，则SDK将继续从本地缓存为功能标志评估提供服务。

## 可用SDK {#available-sdks}

### Android扩展 {#android-extension}

Android的Experience Rollout扩展与Adobe Experience Platform Mobile SDK集成。

有关设置说明，请参阅[Android扩展集成指南](../sdk-releases/android/android-extension-integration-guide.md)。

>[!NOTE]
>
>适用于Web和其他移动平台的其他SDK选项正在准备中，不久将会推出。 有关抢先体验的指导，请联系您的Adobe代表。

## 另请参阅 {#see-also}

* [Android扩展集成指南](../sdk-releases/android/android-extension-integration-guide.md)
* [Web 服务](web-services.md)
* [集成步骤](integration-steps.md)
