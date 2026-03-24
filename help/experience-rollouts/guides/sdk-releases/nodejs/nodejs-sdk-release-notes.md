---
title: Node.js SDK发行说明
description: Experience Rollouts Node.js SDK的发行说明，其中包括所有已发布版本中的新增功能、改进和错误修复的更改日志。
source-git-commit: 9bfe0e55e89c1d7fbd77cde63831a6a186820e24
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 1%

---


# Node.js SDK发行说明 {#nodejs-sdk-release-notes}

本页列出了Experience Rollout Node.js SDK的发行历史记录。 有关集成设置，请参阅[Node.js SDK集成指南](nodejs-sdk-integration-guide.md)。

## 版本1.0.10 {#v1-0-10}

**错误修复和套接字改进**

* 修复了在计划的缓存刷新期间引发的`ESOCKETTIMEDOUT`异常。 已从`createInstance()`中的`featureRequestHttpParams`和`ingestAnalyticsHttpParams`删除`maxSockets`参数。
* 修复了在HTTP 304（未修改）响应后，可缓存客户端被错误地标记为不可缓存的错误。
* 已删除`isReleaseBitEnabled()` — 不再支持此方法。
* 改进了日志记录输出，提供了更好的诊断。
* 已发布的npm包中不再包含Test和Coverage文件夹。

## 版本1.0.5 {#v1-0-5}

**稳定性改进**

对缓存刷新处理和SDK初始化边缘案例的常规修复。

## 版本1.0.3 {#v1-0-3}

**初始稳定版本**

Node.js SDK的第一个生产版本支持经过身份验证的、匿名的和默认的完全转出功能标志检索。

## 另请参阅 {#see-also}

* [Node.js SDK集成指南](nodejs-sdk-integration-guide.md)
* [Java SDK发行说明](../../sdk-releases/java/java-sdk-release-notes.md)
* [SDK](../../integrate/sdks.md)
