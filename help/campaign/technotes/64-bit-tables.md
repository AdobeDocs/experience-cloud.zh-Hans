---
title: Adobe Campaign Web用户界面
description: 64位表
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard迁移的用户"
exl-id: ab5f01fd-4ad5-46e9-b132-011fe0f7bbd2
source-git-commit: 11c49b273164b632bcffb7de01890c6f9d7ae9c2
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 7%

---

# 64位架构 {#sixty-four-bit-tables}

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
| nms:broadLogRcp | ID |
| nms:trackingLogRcp | ID |
| nms:excludeLogRcp | ID |
| nms:broadLogVisitor | ID |
| nms:trackingLogVisitor | ID |
| nms:propositionRcp | interactionId |
| nms:propositionVisitor | interactionId |
| nms:webTrackingLog | ID |
| nms:tmpBroadcast | message-id |
| nms:tmpMarketingPressure | message-id |
| nms:tmpBroadcastExclusion | message-id |
| nms:tmpBroadcastPaper | message-id |
| nms:broadLogAppSubRcp | ID |
| nms:trackingLogAppSubRcp | ID |
| nms:excludeLogAppSubRcp | ID |
| nms:webEvent | broadLogSrc-id、broadLogRemkt-id |
| nms:broadLogMid | mktBroadLogId |
| nms:mirrorPageSearch | remoteMessageId |
