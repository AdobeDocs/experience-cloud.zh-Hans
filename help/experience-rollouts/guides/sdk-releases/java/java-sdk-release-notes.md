---
title: Java SDK发行说明
description: Experience Rollout Java SDK的发行说明，其中包括所有已发布版本中的新增功能、改进和错误修复的更改日志。
source-git-commit: 9bfe0e55e89c1d7fbd77cde63831a6a186820e24
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 2%

---


# Java SDK发行说明 {#java-sdk-release-notes}

本页列出了Experience Rollout Java SDK的发行历史记录。 有关集成设置，请参阅[Java SDK集成指南](java-sdk-integration-guide.md)。

## 版本4.0.6 {#v4-0-6}

**响应中的控制组数据**

您现在可以在SDK响应中检索变量和控制组数据，匹配REST功能API的行为。 要启用此功能，请将`.includeControlGroup()`添加到您的`FloodgateConfiguration`生成器。

## 版本4.0.5 {#v4-0-5}

**稳定性和性能改进**

对缓存刷新可靠性和连接处理进行了一些内部改进。

## 版本4.0.4 {#v4-0-4}

**重试策略改进**

改进了临时服务错误时的默认重试行为。

## 版本4.0.3 {#v4-0-3}

**错误修复**

修复了异步初始化中边缘用例的常规稳定性。

## 版本4.0.1 (Beta) {#v4-0-1-beta}

4.x SDK的&#x200B;**Beta版本**

引入了DX客户端支持、DX区域配置和AEP（沙盒）支持。

## 版本 3.1.0 {#v3-1-0}

**对DX客户端的流支持**

添加了基于SSE的流功能，可近乎实时地通知SDK客户端标志更新。

## 版本3.0.x {#v3-0-x}

已引入&#x200B;**Java 11要求**

从版本3.0.0开始，SDK要求使用JDK 11或更高版本。 早期的主要版本支持JDK 8+。

引入了对DX客户端的逐个引用受众支持，允许可重用的受众定义由功能实体中的ID引用。

## 版本2.x {#v2-x}

**不可缓存的客户端支持（来自0.8）**

不可缓存的客户端可以调用`getFeature()` live而不是从SDK缓存中读取。 SDK继续在后台轮询，并在客户端变为可缓存时切换到基于缓存的服务。

其他2.x改进包括新的生成器选项（`alwaysCache()`、`neverCache()`、自定义HTTP客户端和执行器支持）、功能和发行密钥筛选以及模拟用户检索。

## 版本1.x {#v1-x}

初始版本系列。 支持的JDK 8+、Maven依赖项集成以及基本的已验证和匿名功能标志检索。

## 另请参阅 {#see-also}

* [Java SDK集成指南](java-sdk-integration-guide.md)
* [Node.js SDK发行说明](../../sdk-releases/nodejs/nodejs-sdk-release-notes.md)
* [SDK](../../integrate/sdks.md)
