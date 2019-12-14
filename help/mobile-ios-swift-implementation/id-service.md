---
title: 通过Launch实施Adobe Experience Platform Identity Service
description: 了解如何添加Adobe Experience Platform Identity service扩展并使用“设置客户ID”动作收集客户ID。 本课程是在Mobile iOS Swift应用程序中实施Experience cloud教程的一部分。
seo-description: null
seo-title: 通过Launch实施Adobe Experience Platform Identity Service
solution: Experience Cloud
translation-type: tm+mt
source-git-commit: e9dee6d0aa3b775d0ce617e2b2c57b56de491b8d

---


# 添加Adobe Experience Platform Identity Service

Adobe [Experience Platform Identity Service](https://docs.adobe.com/content/help/en/id-service/using/home.html) (Adobe Experience Platform Identity Service)可在所有Adobe解决方案中设置一个通用访客ID，以便支持Experience cloud功能，如在解决方案之间共享受众。  您还可以将您自己的客户ID发送到服务，以实现跨设备定位以及与客户关系管理(CRM)系统的集成。

Identity service是Mobile Core扩展的一部分， ***因此您在安装Mobile SDK时已实施它***! 目前，本教程不包含设置客户ID的说明。 有关如何设置客户ID的 [详细信息，请参阅文档](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference)。

## 验证步骤

要验证对Identity service的调用，请在Xcode或Developer studio中运行示例应用程序，打开调试控制台并查找请求和响应：

1. **向Identity service请求** (将控制台过滤为 `demdex.net`)在此示例中，ID(`d_mid`)已设置，且正在重新报告)

   ```swift
   2019-01-15 12:11:45.164590-0500 BusDemoSwift[52399:5056322] [AMSDK DEBUG <com.adobe.module.identity>]: Sending request (https://dpm.demdex.net/id?d_rtbd=json&d_ver=2&d_orgid=7ABB3E6A5A7491460A495D61@AdobeOrg&d_mid=17179986463578698626041670574784107777&d_blob=j8Odv6LonN4r3an7LhD3WZrU1bUpAkFkkiY1ncBR96t2PTI&dcs_region=9)
   ```

1. **来自Identity service的响应** (将控制台过滤为 `ID Service`)。 请注意该 `mid` 值如何与上述请 `d_mid` 求中的值相匹配：

   ```swift
   2019-01-15 12:11:45.681821-0500 BusDemoSwift[52399:5056322] [AMSDK DEBUG <com.adobe.module.identity>]: ID Service - Got ID Response (mid: 17179986463578698626041670574784107777, blob: j8Odv6LonN4r3an7LhD3WZrU1bUpAkFkkiY1ncBR96t2PTI, hint: 9, ttl: "604800000 ms")
   
[下一个“添加Adobe Target VEC支持”&gt;](target-vec.md)
