---
title: GET功能API V3
description: 体验转出功能API V3的API参考，用于检索Web和移动应用程序的功能标记。
source-git-commit: 6ecedbfc6c7de392f214f3f8f2e71aa18e1bacb9
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 9%

---


# GET功能API V3 {#get-feature-api-v3}

功能API V3是Web和移动应用程序中用于检索功能标记的主要端点。 它会根据用户的身份和在控制台中配置的受众规则，返回用户有资格使用的功能和版本。

**终结点：** `GET {HOST}/fg/api/v3/feature`

将`https://p13-stage.adobe.io`用于暂存，将`https://p13n.adobe.io`用于生产。

## 请求 {#request}

### 请求标头 {#request-headers}

| 标头 | 类型 | 描述 | 必需 |
|---|---|---|---|
| `x-api-key` | 字符串 | 来自Adobe Developer Console的应用程序API密钥。 必须为暂存和生产单独配置。 | 是 |
| `Authorization` | 字符串 | **不需要**&#x200B;用于未经身份验证的情况。 对经过身份验证的用户使用`Bearer <AccessToken>`。 将`Bearer <ServiceToken>`用于服务器端SDK缓存方案。 | 否 |
| `x-adobe-uuid` | 字符串 | 唯一的访客或设备ID。 用于支持未经身份验证的用户使用百分比转出，并保持跨会话的粘性以及未经身份验证到经过身份验证的过渡。 | 否 |

### 查询参数 {#query-parameters}

| 参数 | 类型 | 描述 | 必需 |
|---|---|---|---|
| `clientId` | 字符串 | 您的应用程序的客户端ID，已在体验转出控制台中载入。 | 是 |
| `ignore_rf` | 布尔值 | 如果`true`，则忽略版本标志，并返回客户端的所有版本。 默认值： `false`。 | 否 |
| `rf` | 字符串 | 释放标记。 仅在`ignore_rf`为`false`时使用。 | 否 |
| `meta` | 布尔值 | 如果`true`，则每个功能的元数据都包含在响应中，作为键值对返回，其中值为Base64编码。 默认值： `false`。 | 否 |
| `userId` | 字符串 | 需要服务令牌。 您要为其检索功能标志的用户的GUID。 | 否 |
| *上下文参数* | 不适用 | 以上未列出的任何查询参数均被视为上下文变量，并用于评估受众规则。 将多个值作为`?key1=val1&key2=val2`传递。 示例：`?clientLanguage=ja_JP&contractCurrency=JPY`。 | 否 |

## 响应 {#response}

### 响应状态代码 {#response-status}

| 状态代码 | 描述 |
|---|---|
| `200 OK` | 响应正文中返回的功能标志数据。 |
| `304 Not Modified` | 客户端传递的ETag与最新的服务器状态匹配。 将此视为无操作 — 不应用任何更改。 |
| `400 Bad Request` | `clientId`未载入或请求格式错误。 |
| `403 Forbidden` | API密钥无效，或应用程序未订阅到Adobe Developer Console中的Experience Rollout API。 |

### 响应标头 {#response-headers}

| 标头 | 描述 |
|---|---|
| `x-request-id` | 用于调试的唯一请求标识符。 将此包含在任何支持请求中。 |
| `ETag` | 表示此用户功能的当前服务器状态的令牌。 在后续请求中将此值作为`If-None-Match`传递。 如果状态未更改，则API返回`304`。 |
| `x-adobe-fg-poll-interval` | 客户端本地缓存的TTL（秒）。 仅在经过此间隔后才重新调用API。 |

### 响应正文 {#response-body}

响应是一个JSON对象，它具有以下顶级字段：

| 字段 | 类型 | 描述 |
|---|---|---|
| `api_version` | 字符串 | api版本。 内部字段 — 无需处理。 |
| `json_version` | 字符串 | JSON架构版本。 内部字段 — 无需处理。 |
| `ttl` | 整数 | 缓存TTL（以秒为单位）。 与`x-adobe-fg-poll-interval`响应标头的值相同。 默认值：300。 |
| `caching_enabled` | 布尔值 | 如果`true`，则在客户端本地进行功能评估。 如果`false`，则对每个请求都将在服务器端进行评估。 |
| `client_analytics_params` | 对象 | 应用程序的Analytics配置。 请参阅下面的[client_analytics_params字段](#client-analytics-params)。 |
| `releases` | 数组 | 版本列表和功能标记表示用户符合条件。 请参阅下面的[释放字段](#releases-fields)。 |

#### client_analytics_params字段 {#client-analytics-params}

| 字段 | 描述 |
|---|---|
| `app_id` | 应用程序的数值ID。 |
| `safe_event_required` | 如果为此客户端启用了重定位事件，则为`true`。 |
| `analytics_required` | V3响应中始终为`false`。 |

#### 版本字段 {#releases-fields}

| 字段 | 描述 |
|---|---|
| `release_name` | 用户有资格使用的版本或功能组的名称。 |
| `bit_index` | 发行位索引。 负值表示完全转出状态。 |
| `features` | 用户有资格使用的功能标志键的数组。 仅当用户符合条件并且标记处于启用状态时，才会返回功能键。 这是应围绕其构建应用程序逻辑的主要字段。 |
| `meta` | 与该功能关联的可选Base64编码元数据。 在使用之前解码。 |
| `release_analytics_params` | 每个符合条件的功能的分析元数据对象数组。 请参阅下面的[release_analytics_params字段](#release-analytics-params)。 在控制组方案中，`features`为空。 |

#### release_analytics_params字段 {#release-analytics-params}

| 字段 | 类型 | 描述 |
|---|---|---|
| `app_id` | 整数 | 应用程序ID。 |
| `release_id` | 整数 | 版本ID。 |
| `bit_index` | 整数 | 释放位索引。 已弃用。 |
| `variant_id` | 整数 | 如果用户在控制组中，则为`0`；否则为非零。 |
| `feature_id` | 整数 | 内部功能ID |
| `f_key` | 字符串 | 功能标志键。 |

## 示例请求和响应 {#sample}

### 示例请求 {#sample-request}

```http
GET /fg/api/v3/feature?clientId=MyWebApp&meta=true HTTP/1.1
Host: p13n.adobe.io
Authorization: Bearer <ACCESS_TOKEN>
x-api-key: <YOUR_API_KEY>
If-None-Match: <ETAG>
```

### 示例响应 — 测试组中的用户 {#sample-response-test}

```json
{
  "api_version": "0.1",
  "json_version": "0.1",
  "clients": {
    "MyWebApp": {
      "analyticsVersion": "2.0",
      "client_analytics_params": {
        "app_id": 1378,
        "safe_event_required": false,
        "analytics_required": false
      },
      "releases": [
        {
          "bit_index": -160,
          "release_name": "||features||",
          "features": ["ff1", "ff2", "ff3"],
          "release_analytics_params": [
            {
              "app_id": 1378,
              "release_id": -1,
              "bit_index": -160,
              "variant_id": 10040476,
              "feature_id": 26059,
              "f_key": "ff1",
              "analytics_required": true
            }
          ]
        }
      ]
    }
  },
  "ttl": 60
}
```

### 示例响应 — 控制组中的用户 {#sample-response-control}

当用户在控制组中时，`features`数组为空，`variant_id`为`0`：

```json
{
  "api_version": "0.1",
  "json_version": "0.1",
  "clients": {
    "MyWebApp": {
      "releases": [
        {
          "bit_index": -160,
          "release_name": "||features||",
          "features": [],
          "release_analytics_params": [
            {
              "app_id": 1378,
              "release_id": -1,
              "bit_index": -160,
              "variant_id": 0,
              "feature_id": 26059,
              "f_key": "ff1"
            }
          ]
        }
      ]
    }
  },
  "ttl": 60
}
```

## 另请参阅 {#see-also}

* [GET功能API V2](get-feature-api-v2.md)
* [Web 应用程序](../guides/integrate/web-applications.md)
* [移动设备应用程序](../guides/integrate/mobile-applications.md)
* [集成步骤](../guides/integrate/integration-steps.md)
