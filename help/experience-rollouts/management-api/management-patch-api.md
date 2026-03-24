---
title: 管理修补程序API
description: 使用体验转出PATCH API更新功能标记、功能组或跨团队功能组的各个字段，而不传递完整对象。
source-git-commit: 6ecedbfc6c7de392f214f3f8f2e71aa18e1bacb9
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 3%

---


# 管理修补程序API {#management-patch-api}

PATCH API允许您更新功能标记、功能组或跨团队功能组的特定字段，而无需在请求正文中发送完整对象。 这对于目标更新非常有用，例如更改受众规则、切换状态或调整变量百分比。

## 功能标记PATCH {#feature-flag-patch}

更新功能标志的一个或多个字段。

| | |
|---|---|
| **终结点** | `PATCH /m/api/v1/mgmt/feature/{featureFlagId}` |
| **方法** | PATCH |

### 请求标头 {#ff-request-headers}

所有请求都需要[常见要求](feature-management-apis-overview.md#common-requirements)中所述的标头。

### Path参数 {#ff-path-param}

| 参数 | 类型 | 描述 | 必需 |
|---|---|---|---|
| `featureFlagId` | 整数 | 要更新的功能标志的数值ID。 | 是 |

### 请求正文 {#ff-request-body}

仅传递要更新的字段。 响应将始终返回完整的更新功能标志对象。

**示例 — 仅更新描述：**

```json
{
  "description": "Updated description"
}
```

**示例 — 移除现有受众：**

```json
{
  "audience": null
}
```

**示例 — 在没有受众时添加新受众：**

```json
{
  "audience": [
    {
      "criteria": {
        "and": [
          { "operator": "EQ", "attr": "sandboxType", "val": "DEVELOPMENT", "ruleId": 1, "category": "contextual" }
        ]
      }
    }
  ]
}
```

**示例 — 更新现有的受众规则：**

```json
{
  "audience": [
    {
      "id": 10020035,
      "criteria": {
        "and": [
          { "operator": "EQ", "attr": "sandboxType", "val": "PRODUCTION", "ruleId": 1, "category": "contextual" }
        ]
      }
    }
  ]
}
```

**示例 — 更改状态和变量百分比：**

```json
{
  "state": "disabled",
  "variations": [
    {
      "id": 10017188,
      "variantName": "Variation 1",
      "variantPercentage": 80.0
    }
  ]
}
```

>[!NOTE]
>
>更新现有受众规则时，请包含规则的`id`（可从GET功能响应中获取）以就地更新该规则。 更新变体时，请包含变体的`id`以避免创建重复。

### 响应 {#ff-response}

| 状态 | 描述 |
|---|---|
| `200` | 成功。 响应正文是完整的更新功能标志对象。 |
| `400` | 有效负载无效。 |
| `403` | 权限不足。 |
| `417` | 并发更新冲突。 获取当前功能并重试。 |

## 功能组PATCH {#feature-group-patch}

更新功能组的一个或多个字段。 请求和响应结构与功能标记PATCH相同 — 只是端点不同。

| | |
|---|---|
| **终结点** | `PATCH /m/api/v1/mgmt/group/{featureGroupId}` |
| **方法** | PATCH |

## 跨团队功能组PATCH {#ctfg-patch}

更新跨团队功能组的一个或多个字段。 使用v2发布端点。

| | |
|---|---|
| **终结点** | `PATCH /m/api/v2/mgmt/release/{CTFGId}` |
| **方法** | PATCH |

## 另请参阅 {#see-also}

* [功能标记管理API](feature-flags-management-api.md)
* [功能组管理API](feature-group-management-api.md)
* [发布管理API](release-management-apis.md)
* [功能管理API概述](feature-management-apis-overview.md)
