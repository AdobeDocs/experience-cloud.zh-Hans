---
title: Adobe Campaign Web用户界面
description: 64位表
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
source-git-commit: 47b06a42fad73254025d8e21d14724f6fe93345b
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 1%

---


# 64位架构 {#64-bit-tables}

为了便于从Campaign Standard过渡到Campaign v8，已将多个表从32位更改为64位。 事实上，Campaign Standard在多种现成架构中支持64位PK，而Campaign v8在大多数架构中支持32位PK。

## 限制

* 此技术更改仅适用于从Campaign Standard迁移的客户。
* 架构和broadlog扩展在64位中不受支持。 它将保持32位。
* 与发送给技术用户的投放相关的日志在Campaign v8中将不可用。
* 仅支持PostgreSQL。

## 修改后的架构

以下是已更改为64位的架构及其修改属性的列表。

| 架构名称 | 属性名称 |
|--- |--- |
| nms：broadLogRcp | id |
| nms：trackingLogRcp | id |
| nms：excludeLogRcp | id |
| nms：broadLogVisitor | id |
| nms：trackingLogVisitor | id |
| nms：propositionRcp | interactionId |
| nms：propositionVisitor | interactionId |
| nms：webTrackingLog | id |
| nms：tmpBroadcast | message-id |
| nms：tmpMarketingPressure | message-id |
| nms：tmpBroadcastExclusion | message-id |
| nms：tmpBroadcastPaper | message-id |
| nms：broadLogAppSubRcp | id |
| nms：trackingLogAppSubRcp | id |
| nms：excludeLogAppSubRcp | id |
| nms：webEvent | broadLogSrc-id、broadLogRemkt-id |
| nms：broadLogMid | mktBroadLogId |
| nms：mirrorPageSearch | remoteMessageId |


