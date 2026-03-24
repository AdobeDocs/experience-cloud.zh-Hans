---
title: 功能组管理API
description: 体验转出功能组管理API的API参考，包括用于获取、创建、更新、删除和控制功能组的转出计划的端点。
source-git-commit: db719ba7b9db91aea818d8ef216a28fcedc6aa65
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 14%

---


# 功能组管理API {#feature-group-management-api}

功能组管理API允许您以编程方式创建、读取、更新和删除体验转出中的功能组，包括自动化和A/B测试转出计划。

**基本路径：** `/m/api/v1/mgmt/group`

所有请求都需要[常见要求](feature-management-apis-overview.md#common-requirements)中所述的标头。

## 获取所有功能组 {#get-all-groups}

检索您组织的所有功能组。

| | |
|---|---|
| **终结点** | `GET /m/api/v1/mgmt/group` |
| **方法** | GET |

### 查询参数 {#get-all-query-params}

| 参数 | 类型 | 描述 | 必需 |
|---|---|---|---|
| `myOrg` | 布尔值 | 设置为`true`以包含组织信息。 | 是 |
| `includeClientInfo` | 布尔值 | 设置为`true`以包含每个组的应用程序信息。 | 是 |

### 响应 {#get-all-response}

| 状态 | 描述 |
|---|---|
| `200` | 成功。 响应正文是一个功能组对象数组。 |

## 按ID获取功能组 {#get-group-by-id}

按数字ID检索单个特征组。

| | |
|---|---|
| **终结点** | `GET /m/api/v1/mgmt/group/{groupId}` |
| **方法** | GET |
| **查询参数** | `includeAnalyzeInfo=true` （可选 — 将analytics数据添加到响应） |

### 响应 {#get-by-id-response}

| 状态 | 描述 |
|---|---|
| `200` | 成功。 响应正文是一个功能组对象。 |
| `400` | 功能组ID无效。 |

## 创建功能组 {#create-group}

创建具有手动、自动或A/B测试转出类型的新功能组。

| | |
|---|---|
| **终结点** | `POST /m/api/v1/mgmt/group` |
| **方法** | POST |

### 请求正文 {#create-request-body}

请求正文使用[功能组对象](#feature-group-object)。 `params`中的`rolloutType`是必需的，它决定了有效负荷的结构。

**示例 — 手动转出：**

```json
{
  "params": {
    "rolloutType": "manual",
    "label": "my-feature-group",
    "tags": [],
    "canContextOverridePUP": false
  },
  "status": "SAVED",
  "type": "group",
  "name": "my.feature.group",
  "description": "A manual feature group",
  "variations": [{ "variantPercentage": 100, "variantName": "Variant 1", "features": [] }],
  "audience": [{ "criteria": { "and": [{ "operator": "EQ", "attr": "COUNTRY", "val": "US", "ruleId": 1, "category": "default" }] } }],
  "clients": [],
  "org": { "id": 95 }
}
```

### 响应 {#create-response}

| 状态 | 描述 |
|---|---|
| `200` | 成功。 响应正文是创建的功能组对象。 |
| `400` | 有效负载无效 — 有关详细信息，请参阅[错误消息](#error-messages)。 |
| `403` | 权限不足。 |

## 更新功能组 {#update-group}

更新现有的功能组。 传递与创建请求正文相同的结构，包括`id`字段。

| | |
|---|---|
| **终结点** | `PUT /m/api/v1/mgmt/group` |
| **方法** | PUT |

### 响应 {#update-response}

| 状态 | 描述 |
|---|---|
| `200` | 成功。 响应正文是更新的功能组对象。 |
| `400` | 有效负载无效。 |
| `403` | 权限不足。 |

## 删除功能组 {#delete-group}

按数字ID删除功能组。

| | |
|---|---|
| **终结点** | `DELETE /m/api/v1/mgmt/group/{groupId}` |
| **方法** | DELETE |

### 响应 {#delete-response}

| 状态 | 描述 |
|---|---|
| `204` | 成功。 无响应正文。 |
| `403` | 权限不足。 |

## 功能组对象引用 {#feature-group-object}

| 字段 | 类型 | 描述 | 必需 |
|---|---|---|---|
| `id` | 整数 | 功能组ID。 仅对于更新调用是必需的。 | 条件 |
| `name` | 字符串 | 功能组密钥。 最多50个字符。 模式： `^[a-zA-Z0-9_.-]*$` | 是（创建） |
| `clients` | 数组 | 与组关联的应用程序。 每个条目必须包括`id`和`imsClientId`。 | 是 |
| `status` | 字符串 | `"SAVED"` 或 `"PUBLISHED"` | 是 |
| `type` | 字符串 | 功能组始终为`"group"`。 | 是 |
| `org` | 对象 | 组织详细信息。 必须包括`id`。 | 是 |
| `params` | 对象 | 组参数。`rolloutType` 是必需的（`"manual"`、`"automated"`或`"ab-testing"`）。 还支持`label`和`tags`。 | 是 |
| `audience` | 数组 | 适用于手动转出类型的受众规则。 | 否 |
| `variations` | 数组 | 变量列表。 查看[FeatureGroupVariation对象](#featuregroupvariation-object)。 | 否 |
| `phaseRollOutPlan` | 对象 | 阶段转出计划。 对于自动化和A/B测试类型是必需的。 查看[PhaseRollOutPlan对象](#phaserolloutplan-object)。 | 条件 |
| `description` | 字符串 | 可选显示说明。 最多225个字符。 | 否 |

### FeatureGroupVariation对象 {#featuregroupvariation-object}

| 字段 | 类型 | 描述 | 必需 |
|---|---|---|---|
| `id` | 整数 | 变量ID。 仅对于更新调用是必需的。 | 条件 |
| `variantName` | 字符串 | 变体名称。 硬编码为`"Variant 1"`。 | 是 |
| `variantPercentage` | 小数 | 接收此变体的受众百分比。 必须大于0且不得大于100。 | 是 |

### PhaseRollOutPlan对象 {#phaserolloutplan-object}

| 字段 | 类型 | 描述 | 必需 |
|---|---|---|---|
| `phaseRollOutBlocks` | 数组 | 阶段块和等待块的有序列表。 最后一个块必须是相位块。 | 是 |
| `rollOutPlanState` | 字符串 | `"DRAFT"`、`"RUNNING"`、`"PAUSED"`或`"ABORTED"` | 是 |

`phaseRollOutBlocks`中的每个块都是包含具有受众条件的`phaseRule`的&#x200B;**阶段块** (`isPhaseBlock: true`)，或者是包含具有`waitDuration` （相对）或`executionDate` （固定时间戳）的`waitRule`的&#x200B;**等待块** (`isPhaseBlock: false`)。

## 错误消息 {#error-messages}

| 条件 | 状态 | 错误消息 |
|---|---|---|
| 名称无效或为空 | 400 | `Error: Invalid value for release name.` |
| 空受众条件 | 400 | `Error: Release is not valid` |
| 自动化类型的多个变量 | 400 | `Error: Feature variation is not valid. Variation name should be unique across variations` |
| 已发布不含客户端的组 | 400 | `Error: At least one client must be associated with enabled feature group.` |
| 计划中的最后一个块不是阶段块 | 400 | `Error: The last block in the Phase Rollout plan should be phase block` |
| 等待块时间不正常 | 400 | `Error: Wait block timings are not in order in the phase rollout plan` |
| 等待块类型不一致 | 400 | `Error: Wait block should be of same type.` |
| 编辑激活的阶段块 | 400 | `Error: Activated phase block should not be changed` |
| 转出类型为空 | 400 | `Error: Rollout type cannot be empty while feature group creation` |
| 已通过手动类型的阶段计划 | 400 | `Error: PhaseRollOutPlan can't be added with manual rollout type while feature group creation` |
| 计划通过，状态为“已发布” | 400 | `Error: Schedule can't be added in published state while release/group creation` |

## 另请参阅 {#see-also}

* [功能管理API概述](feature-management-apis-overview.md)
* [功能标记管理API](feature-flags-management-api.md)
* [管理修补程序API](management-patch-api.md)
