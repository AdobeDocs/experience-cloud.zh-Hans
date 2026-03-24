---
title: 发布管理API
description: Experience Rollout版本管理API的API参考，包括用于获取、创建和编辑版本以及跨团队功能组的端点。
source-git-commit: 8a92b7a3e8c52da8bb2474f52c831e159420b878
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 13%

---


# 发布管理API {#release-management-apis}

版本管理API允许您以编程方式检索、创建和编辑版本和跨团队功能组(CTFG)。 这些API使用v2管理端点。

**基本路径：** `/m/api/v2/mgmt/release`

所有请求都需要[常见要求](feature-management-apis-overview.md#common-requirements)中所述的标头，以及下面列出的其他标头。

## 其他必填标题 {#additional-header}

| 标头 | 描述 | 必需 |
|---|---|---|
| `x-user-context-org` | 您组织的数字团队ID。 您可以在团队设置下的体验转出控制台中找到此值。 | 是 |

## 按ID获取版本 {#get-release}

按数字ID检索单个版本或跨团队功能组。

| | |
|---|---|
| **终结点** | `GET /m/api/v2/mgmt/release/{id}` |
| **方法** | GET |

### 查询参数 {#get-query-params}

| 参数 | 类型 | 描述 | 默认 |
|---|---|---|---|
| `includePermissions` | 布尔值 | 包含更新或删除此版本的权限。 | `true` |
| `includeOrg` | 布尔值 | 包括此版本的组织信息。 | `true` |
| `includeAnalyzeInfo` | 布尔值 | 包括分析信息。 | `false` |

### 响应 {#get-response}

| 状态 | 描述 |
|---|---|
| `200` | 成功。 响应正文是一个发布对象 — 请参阅[发布对象引用](#release-object)。 |
| `400` | 版本ID无效或请求格式错误。 |

## 创建版本 {#create-release}

创建新版本或跨团队功能组。

| | |
|---|---|
| **终结点** | `POST /m/api/v2/mgmt/release` |
| **方法** | POST |

### 请求正文 {#create-request-body}

请求正文使用[释放对象](#release-object)。 对于创建，跨团队功能组（`CROSS_TEAM_FEATURE_GROUP`类型）的`status`必须设置为`"SAVED"`，对于标准版本（`RELEASE`类型）则必须设置为`"DRAFT"`。

**示例 — 创建跨团队功能组：**

```json
{
  "params": {
    "rolloutType": "manual",
    "cohortingType": "guid",
    "tags": [],
    "canContextOverridePUP": false,
    "label": "my-cross-team-group"
  },
  "status": "SAVED",
  "type": "CROSS_TEAM_FEATURE_GROUP",
  "name": "my-cross-team-group",
  "description": null,
  "meta": "",
  "variations": [{ "variantPercentage": 100, "variantName": "Variant 1", "features": [] }],
  "audience": [{}],
  "clients": [],
  "pollInterval": 300,
  "org": { "id": "95" },
  "comment": ""
}
```

### 响应 {#create-response}

| 状态 | 描述 |
|---|---|
| `200` | 成功。 响应正文是创建的发布对象。 |
| `400` | 有效负载无效。 |

## 编辑版本 {#edit-release}

更新现有版本或跨团队功能组。 传递包含`id`字段的完整发布对象。

| | |
|---|---|
| **终结点** | `PUT /m/api/v2/mgmt/release/{id}` |
| **方法** | PUT |

### 响应 {#edit-response}

| 状态 | 描述 |
|---|---|
| `200` | 成功。 响应正文是更新的发行对象。 |
| `417` | 并发更新冲突。 该版本已在GET调用和PUT调用之间修改。 获取当前版本并重试。 |

## 发行对象引用 {#release-object}

| 字段 | 类型 | 描述 | 必需 |
|---|---|---|---|
| `id` | 整数 | 版本ID。 仅对于更新调用是必需的。 | 条件 |
| `name` | 字符串 | 版本名称。 最多50个字符。 模式： `^[a-zA-Z0-9_ ,.:()-]*$`。 必须是唯一的。 | 是 |
| `description` | 字符串 | 可选描述。 最多255个字符。 | 否 |
| `type` | 字符串 | 标准版本为`"RELEASE"`；跨团队功能组为`"CROSS_TEAM_FEATURE_GROUP"`。 | 是 |
| `status` | 字符串 | 发布状态。 对于IMS：创建时`"DRAFT"`；更新时`"DRAFT"`、`"SAVED"`、`"PUBLISHED"`。 对于CTFG： `"SAVED"`，在创建时；`"SAVED"`，`"PUBLISHED"`，更新时。 | 是 |
| `clients` | 数组 | 与此版本关联的应用程序。 每个条目需要`id` （数字）和`imsClientId` （字符串）。 | 否 |
| `audience` | 数组 | 受众规则的列表。 查看[条件对象](feature-flags-management-api.md#condition-object)。 | 否 |
| `variations` | 数组 | 变体列表。 提交期间仅支持1个变体。 | 提交所需 |
| `params` | 对象 | 版本参数。 请参阅[支持的参数字段](#supported-params)。 | 提交所需 |
| `org` | 对象 | 组织对象。 必须包括`id`。 | 否 |

### 支持的参数字段 {#supported-params}

| 字段 | 类型 | 描述 | 必需 |
|---|---|---|---|
| `label` | 字符串 | 显示名称。 最多50个字符。 | 是 |
| `tags` | 数组\&lt;字符串\> | 可选标记。 最多50个字符。 | 否 |
| `canContextOverridePUP` | 布尔值 | 如果`true`，则上下文规则将覆盖配置文件规则。 默认值： `false`。 | 是 |
| `isBetaRelease` | 布尔值 | 如果`true`，则将此版本标记为测试版。 默认值： `false`。 | 否 |

### 变量对象 {#variation-object}

| 字段 | 类型 | 描述 | 必需 |
|---|---|---|---|
| `id` | 整数 | 变量ID。 仅对于更新调用是必需的。 | 条件 |
| `variantName` | 字符串 | 变体名称。 最多50个字符。 | 是 |
| `variantPercentage` | 双精度 | 接收此变体的受众百分比。 范围： [0,100]。 | 是 |
| `features` | 数组 | 此变量中包含的功能。 每个条目必须包括`id`、`name`、`clientId`和`state`。 | 否 |

## 另请参阅 {#see-also}

* [功能管理API概述](feature-management-apis-overview.md)
* [功能标记管理API](feature-flags-management-api.md)
* [功能组管理API](feature-group-management-api.md)
* [创建跨团队功能组](../guides/feature-flags/create-cross-team-feature-group.md)
