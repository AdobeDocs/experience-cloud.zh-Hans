---
title: SDK基准测试
description: 查看Adobe体验转出的Java SDK基准测试结果，包括在典型负载条件下跨各种数量功能标记的响应时间测量。
source-git-commit: 8b8b5db1a28af3a3ac29aecf26482f70eb84c714
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 7%

---


# SDK基准测试 {#sdk-benchmarking}

Experience Rollouts Java SDK已设定为基准，用于可靠估计当SDK在其基础架构内运行时集成团队的资源和响应时间。

## 测试环境 {#test-environment}

对具有以下固定配置的Spring Boot应用程序执行了基准测试：

* **CPU核心：** 8
* **JVM内存：** 4096 MB

## 测试假设 {#test-assumptions}

以下条件在所有基准运行中保持不变：

* 已测试功能标志：8到128
* 每个功能标志的上下文变量： 2（类型`STRING`，长度36个字符）
* 平均负载：每分钟15,000个请求(RPM)
* 活动线程：100

## 结果 {#results}

下表显示了随着功能标记数的增加，`getFeatures()`调用的第99.99百分位响应时间：

| 功能标志的数量 | 每个标志的上下文变量 | 响应时间（毫秒，p99.99） |
|---|---|---|
| 8 | 2 | &lt; 0.5 |
| 16 | 2 | &lt; 0.5 |
| 32 | 2 | &lt; 0.5 |
| 64 | 2 | &lt; 1 |
| 128 | 2 | &lt; 1 |

## 解释结果 {#interpretation}

上述基准程序代表了上述特定测试条件下的性能。 由于SDK在应用程序的基础架构中运行，因此实际响应时间会因特定于您环境的因素而异：

* 可用的CPU和内核数
* JVM栈大小和垃圾收集行为
* 线程可用性和上下文切换
* 请求时的当前系统加载

使用这些数字作为计划基线，而不是作为生产环境的保证性能目标。

## 另请参阅 {#see-also}

* [Java SDK集成指南](java/java-sdk-integration-guide.md)
* [Java SDK发行说明](java/java-sdk-release-notes.md)
* [SDK](../integrate/sdks.md)
