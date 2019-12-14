---
title: 通过Launch实施Adobe Experience Platform Identity Service
description: 了解如何添加Adobe Experience Platform Identity service扩展并使用“设置客户ID”动作收集客户ID。 本课程是在Mobile android应用程序中实施Experience cloud教程的一部分。
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

要验证对Identity service的调用，请在Android studio中运行示例应用程序，打开调试控制台并查找请求和响应：

1. **向Identity Service** (过滤日志到 `IdentityExtension`)请求在此示例中，ID(`d_mid`)已设置，且正在重新报告)

   ```java
   03-14 17:01:18.526 7743-7803/com.adobe.busbooking D/ADBMobile: IdentityExtension - Sending request (https://dpm.demdex.net/id?d_mid=59651426340521082405908216148091920022&d_ver=2&d_orgid=7ABB3E6A5A7491460A495D61%40AdobeOrg)
   ```

1. **来自Identity service的响应** (将Logcat过滤为 `IdentityExtension`)。 请注意该 `mid` 值如何与上述请 `d_mid` 求中的值相匹配：

   ```java
   03-14 17:01:19.033 7743-7803/com.adobe.busbooking D/ADBMobile: IdentityExtension - Received ID response (mid: 59651426340521082405908216148091920022, blob: j8Odv6LonN4r3an7LhD3WZrU1bUpAkFkkiY1ncBR96t2PTI, hint: 9, ttl: 604800
   ```

[下一个“添加Adobe Target VEC支持”&gt;](target-vec.md)
