---
title: 桌面应用程序
description: 了解如何使用功能API V2将Adobe体验转出集成到桌面应用程序中。
source-git-commit: b82520eebe0070b5f76e0f7daeb2bb79a4bccca0
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 1%

---


# 桌面应用程序 {#desktop-applications}

通过直接进行REST API调用，桌面应用程序可与体验转出集成。 对桌面客户端使用&#x200B;**功能API V2**。

有关完整API参考，请参阅本指南的功能API部分中的&#x200B;**GET功能API V2**。

## 集成要求 {#requirements}

桌面客户端必须：

* **执行API响应中返回的TTL值**。 TTL定义在再次调用API之前，客户端应缓存功能标志数据的时间。 实施一个测试案例，验证此行为，以确保在没有提供功能标记时，较旧的应用程序版本能够正确进入休眠。
* **正常处理HTTP错误方案**。 在后备功能集中构建，以便在API暂时不可用时，应用程序仍能正常运行。
* **维护一个详细的集成测试计划**，该计划涵盖上述TTL和错误处理要求。

## 应用程序Id {#app-id}

在调用API时，桌面客户端可以使用&#x200B;**产品代码和产品版本**&#x200B;代替标准客户端ID作为应用程序标识符。

## 另请参阅 {#see-also}

* [集成步骤](integration-steps.md)
* [启动指南](startup-guide.md)
