---
title: SDK
description: 了解Flags中的SDK架构以及可用的AEP Web SDK和AEP Mobile SDK扩展。
hide: true
exl-id: 110a440d-b52a-4e1e-a94f-86f9741a223a
source-git-commit: b3e13a42c19eb7b8b7d5d402bf9a56f89f573044
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 4%

---

# SDK {#sdks}

标记提供用于将功能标记集成到应用程序中的SDK。 通过AEP Web SDK和AEP Mobile SDK部署标记。

## SDK架构 {#architecture}

所有Flags SDK共享相同的核心架构：

* **初始化** — SDK在启动时配置，并使用Flags服务注册。
* **功能检索** — SDK检索功能标志数据并在本地评估标志。
* **正在缓存** — SDK将缓存功能标志数据，并在可配置的轮询间隔(TTL)上刷新该数据。
* **错误处理** — 如果该服务不可用，则SDK将继续从本地缓存为功能标志评估提供服务。

## 可用SDK {#available-sdks}

### AEP Web SDK {#web-sdk}

Web的Flags扩展与Adobe Experience Platform Web SDK集成，从而支持在Web应用程序中评估标记。

### Android扩展 {#android-extension}

Android的Flags扩展可与Adobe Experience Platform Mobile SDK集成。

有关设置说明，请参阅[Android扩展集成指南](../sdk-releases/android/android-extension-integration-guide.md)。

### iOS扩展 {#ios-extension}

iOS的Flags扩展可与Adobe Experience Platform Mobile SDK集成。

有关设置说明，请参阅[iOS扩展集成指南](../sdk-releases/ios/ios-extension-integration-guide.md)。

## 另请参阅 {#see-also}

* [Android扩展集成指南](../sdk-releases/android/android-extension-integration-guide.md)
* [Web 服务](web-services.md)
* [集成步骤](integration-steps.md)

<!-- -->
