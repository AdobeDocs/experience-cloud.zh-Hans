---
title: 功能标记管理API
description: 体验转出功能标记管理API的API引用，包括用于获取、创建、更新和删除应用程序的功能标记的端点。
source-git-commit: 8a92b7a3e8c52da8bb2474f52c831e159420b878
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 12%

---


# 功能标记管理API {#feature-flags-management-api}

功能标记管理API允许您以编程方式为Experience Rollout中的应用程序创建、读取、更新和删除功能标记。

**基本路径：** `/m/api/v1/mgmt/feature`

所有请求都需要[常见要求](feature-management-apis-overview.md#common-requirements)中所述的标头。

## 获取所有功能标志 {#get-all-features}

检索指定应用程序的所有功能标志。

| | |
|---|---|
| **终结点** | `GET /m/api/v1/mgmt/feature` |
| **方法** | GET |

### 查询参数 {#get-all-query-params}

| 参数 | 类型 | 描述 | 必需 |
|---|---|---|---|
| `clientId` | 整数 | 应用程序的数值ID。 请参阅[获取客户端ID](get-client-id.md)。 如果未提供`imsClientId`，则此为必填字段。 | 条件 |
| `imsClientId` | 字符串 | 应用程序的字符串格式客户端ID。 如果未提供`clientId`，则此为必填字段。 | 条件 |
| `nonReleaseFeature` | 布尔值 | 设置为`true`以包含与任何组或版本无关的独立功能标记。 对于基于API的工作流，此变量是必需的。 | 是 |

### 响应 {#get-all-response}

| 状态 | 描述 |
|---|---|
| `200` | 成功。 响应正文包含功能标志对象的列表。 |

响应正文包含`features`数组。 每个元素都是一个功能标志对象，其字段在[FeatureDTO对象引用](#featuredto-object)中描述。

**示例响应：**

```json
{
  "features": [
    {
      "id": 22079,
      "name": "new.FF.1",
      "clientId": 1191,
      "state": "enabled",
      "description": "first feature flag",
      "release": { "id": 2631, "name": "FF.group", "status": "SAVED" },
      "audience": null,
      "params": { "label": "new FF 1", "rolloutType": "manual" }
    },
    {
      "id": 22080,
      "name": "new.FF.2",
      "clientId": 1191,
      "state": "enabled",
      "description": "second feature flag",
      "audience": [
        {
          "id": 10034665,
          "criteria": { "and": [{ "operator": "EQ", "attr": "LOCALE", "val": "EN" }] }
        }
      ]
    }
  ]
}
```

## 按ID获取功能标志 {#get-feature-by-id}

按数字ID检索单个功能标记。

| | |
|---|---|
| **终结点** | `GET /m/api/v1/mgmt/feature/{featureId}` |
| **方法** | GET |

### 响应 {#get-by-id-response}

| 状态 | 描述 |
|---|---|
| `200` | 成功。 响应正文是单个[FeatureDTO对象](#featuredto-object)。 |
| `400` | 功能ID无效。 |

## 创建功能标记 {#create-feature}

创建新功能标记。

| | |
|---|---|
| **终结点** | `POST /m/api/v1/mgmt/feature` |
| **方法** | POST |

### 请求正文 {#create-request-body}

请求正文是[FeatureDTO对象](#featuredto-object)。 创建时需要以下字段：

| 字段 | 必需 | 注释 |
|---|---|---|
| `name` | 是 | 功能标志键。 最多50个字符。 模式： `^[a-zA-Z0-9_.-]*$` |
| `clientId` | 是 | 数值应用程序ID。 请参阅[获取客户端ID](get-client-id.md)。 |
| `state` | 是 | `"enabled"` 或 `"disabled"` |

### 响应 {#create-response}

| 状态 | 描述 |
|---|---|
| `200` | 成功。 响应正文包含`{ "generatedFeatureId": <id> }`。 |
| `400` | 有效负载无效。 |
| `403` | 此客户端或受众规则的权限不足。 |
| `417` | 具有开发人员角色的用户无法保存具有公共规则的功能 — 至少需要一个受众规则。 |

**示例请求：**

```json
{
  "name": "my-new-feature",
  "clientId": 1191,
  "state": "disabled",
  "description": "A new feature flag",
  "meta": "VGVzdA==",
  "audience": [
    {
      "criteria": {
        "and": [{ "operator": "EQ", "attr": "COUNTRY", "category": "default", "ruleId": 1, "val": "US" }]
      }
    }
  ],
  "variations": [{ "variantPercentage": 100, "variantName": "Variation 1" }],
  "params": { "label": "My New Feature", "tags": [] }
}
```

## 更新功能标记 {#update-feature}

更新现有的功能标记。 传递包含`id`字段的完整[FeatureDTO对象](#featuredto-object)。

| | |
|---|---|
| **终结点** | `PUT /m/api/v1/mgmt/feature` |
| **方法** | PUT |

### 响应 {#update-response}

| 状态 | 描述 |
|---|---|
| `200` | 成功。 响应正文是更新的FeatureDTO对象。 |
| `400` | 有效负载无效。 |
| `403` | 权限不足。 |
| `417` | 并发更新冲突。 请先获取当前功能，然后从`params`中使用最新的`version`值重试。 |

## 删除功能标志 {#delete-feature}

按数字ID删除功能标志。

| | |
|---|---|
| **终结点** | `DELETE /m/api/v1/mgmt/feature/{featureId}` |
| **方法** | DELETE |

### 响应 {#delete-response}

| 状态 | 描述 |
|---|---|
| `204` | 成功。 无响应正文。 |
| `403` | 权限不足。 |

## FeatureDTO对象引用 {#featuredto-object}

| 字段 | 类型 | 描述 | 必需 |
|---|---|---|---|
| `id` | 整数 | 功能标志ID。 仅对于更新调用是必需的。 | 条件 |
| `name` | 字符串 | 功能标志键（在API响应中返回）。 最多50个字符。 模式： `^[a-zA-Z0-9_.-]*$` | 是（创建） |
| `clientId` | 整数 | 数值应用程序ID。 | 是 |
| `state` | 字符串 | `"enabled"` 或 `"disabled"` | 是 |
| `meta` | 字符串 | API响应中随功能返回的Base64编码元数据。 最多1024个字符。 | 否 |
| `description` | 字符串 | 显示描述。 最多225个字符。 | 否 |
| `audience` | 数组 | 受众规则的列表。 请参阅[FeatureRule对象](#featurerule-object)。 使用[获取所需的受众条件](get-audience-criteria.md)生成此项。 | 否 |
| `variations` | 数组 | 变量列表。 最大3。 请参阅[FeatureVariation对象](#featurevariation-object)。 | 否 |
| `params` | 对象 | 其他元数据。 支持的键： `label` （UI中的显示名称）、`tags` （字符串数组）。 | 否 |
| `release` | 对象 | 版本/组关联。`null` 如果标志不在组中。 只读。 | 否 |

### FeatureVariation对象 {#featurevariation-object}

| 字段 | 类型 | 描述 | 必需 |
|---|---|---|---|
| `id` | 整数 | 变量ID。 仅对于更新调用是必需的。 | 条件 |
| `variantName` | 字符串 | 变体名称。 固定值： `"Variation 1"`、`"Variation 2"`、`"Variation 3"`。 | 是 |
| `variantPercentage` | 小数 | 接收此变体的受众百分比。 必须大于0且不超过100，最多小数位2个。 | 是 |

### FeatureRule对象 {#featurerule-object}

| 字段 | 类型 | 描述 | 必需 |
|---|---|---|---|
| `id` | 整数 | 规则ID。 仅对于更新调用是必需的。 添加新规则时设置为`null`。 | 条件 |
| `criteria` | 对象 | 定义受众规则的条件对象。 查看[条件对象](#condition-object)。 | 是 |

### 条件对象 {#condition-object}

| 字段 | 类型 | 描述 |
|---|---|---|
| `and` | 数组\&lt;条件\> | 所有条件都必须为true。 |
| `or` | 数组\&lt;条件\> | 必须至少有一个条件为true。 |
| `not` | 条件 | 此条件必须为false。 |
| `attr` | 字符串 | 要计算的用户属性（例如，`COUNTRY`，`LOCALE`）。 |
| `operator` | 字符串 | 比较运算符（例如，`EQ`，`IN`，`LT`）。 |
| `val` | 字符串 | 要与之比较的值。 |
| `meta` | 对象 | 可选条件元数据。`desc` 字段设置UI中的显示标签。 |

必须在每个条件中提供`and`、`or`或`not`之一，或者`attr`、`operator`和`val`的组合。

## 另请参阅 {#see-also}

* [功能管理API概述](feature-management-apis-overview.md)
* [管理修补程序API](management-patch-api.md)
* [获取应用程序的客户端ID](get-client-id.md)
* [获取所需的受众条件](get-audience-criteria.md)
