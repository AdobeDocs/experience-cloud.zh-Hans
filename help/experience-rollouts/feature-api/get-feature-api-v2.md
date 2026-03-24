---
title: GET功能API V2
description: 体验转出功能API V2的API参考，用于检索桌面应用程序的功能标记。
source-git-commit: 6ecedbfc6c7de392f214f3f8f2e71aa18e1bacb9
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 11%

---


# GET功能API V2 {#get-feature-api-v2}

功能API V2专为桌面应用程序集成而设计。 它检索经过身份验证用户的功能标记和发行数据，除了标准客户端ID外，还支持产品代码和产品版本作为应用程序标识符。

**终结点：** `GET {HOST}/fg/api/v2/feature`

将`https://p13-stage.adobe.io`用于暂存，将`https://p13n.adobe.io`用于生产。

## 请求 {#request}

### 请求标头 {#request-headers}

| 标头 | 类型 | 描述 | 必需 |
|---|---|---|---|
| `x-api-key` | 字符串 | 来自Adobe Developer Console的应用程序API密钥。 必须为暂存和生产单独配置。 | 是 |
| `Authorization` | 字符串 | `Bearer <AccessToken>`或`Bearer <ServiceToken>`。 | 是 |
| `x-adobe-uuid` | 字符串 | 唯一的访客或设备ID。 用于在未经身份验证的情况下实现百分比转出，并维护会话粘性。 | 否 |

### 查询参数 {#query-parameters}

| 参数 | 类型 | 描述 | 必需 |
|---|---|---|---|
| `clientId` | 字符串 | 体验转出控制台中载入的应用程序客户端ID。 可以传递多个值： `clientId=C1&clientId=C2`。 | 否 |
| `p` | 字符串 | 产品、版本、平台、区域设置字符串（PVPL格式）。 示例：`PHSP:17.0:WIN:en_US`。 可以传递多个值： `p=PHSP:17.0:WIN:en_US&p=PPRO:8:WIN:en_US`。 评估中仅使用产品代码和产品版本。 | 否 |
| `meta` | 布尔值 | 如果为`true`，则为每个功能返回Base64编码的元数据。 默认值： `false`。 | 否 |
| *上下文参数* | 不适用 | 任何其他键值对均被视为用于受众规则评估的上下文变量。 示例：`clientLanguage=ja_JP&contractCurrency=JPY`。 | 否 |

>[!NOTE]
>
>至少需要`clientId`或`p`中的一个来标识应用程序。

## 响应 {#response}

### 响应状态代码 {#response-status}

| 状态代码 | 描述 |
|---|---|
| `200 OK` | 响应正文中返回的功能标志数据。 |
| `304 Not Modified` | ETag与当前服务器状态匹配。 视为免操作 — 不应用任何更改。 |
| `401 Unauthorized` | 授权令牌无效。 |

### 响应标头 {#response-headers}

| 标头 | 描述 |
|---|---|
| `x-request-id` | 用于调试的唯一请求标识符。 将此包含在任何支持请求中。 |
| `ETag` | 表示用户当前功能状态的令牌。 在后续请求中作为`If-None-Match`传递。 如果未更改，则返回`304`。 |
| `x-adobe-fg-poll-interval` | 客户端本地缓存的TTL（以秒为单位）。 仅在经过此间隔后才重新调用API。 |

### 响应正文 {#response-body}

响应是一个JSON对象，它具有以下顶级字段：

| 字段 | 类型 | 描述 |
|---|---|---|
| `api_version` | 字符串 | api版本。 内部字段 — 无需处理。 |
| `json_version` | 字符串 | JSON架构版本。 内部字段 — 无需处理。 |
| `ttl` | 整数 | 缓存TTL（以秒为单位）。 默认值：300。 |
| `clients` | 对象 | 客户端ID（或PVPL字符串）与其发布数据的映射。 每个键都包含如下所述的字段。 |

#### 每个客户端响应字段 {#per-client-fields}

| 字段 | 描述 |
|---|---|
| `releases` | 用户有资格使用的发行版数组。 请参阅下面的[释放字段](#releases-fields)。 |
| `client_analytics_params` | Analytics配置对象。 请参阅下面的[client_analytics_params字段](#analytics-fields)。 |

#### 版本字段 {#releases-fields}

| 字段 | 描述 |
|---|---|
| `release_name` | 版本或功能组的名称。 |
| `bit_index` | 释放位索引。 已弃用。 可能为`null`或负值，具体取决于发布状态。 |
| `features` | 用户有资格使用的功能标志键的数组。 只有在用户符合条件并且已启用标记时，才会显示功能键。 |
| `meta` | 可选的Base64编码元数据。 在使用之前解码。 |
| `release_analytics_params` | 适用于符合条件的功能的Analytics元数据。 在控制组方案中，`features`为空。 |

#### release_analytics_params字段 {#release-analytics-params}

| 字段 | 类型 | 描述 |
|---|---|---|
| `app_id` | 整数 | 应用程序ID。 |
| `release_id` | 整数 | 版本ID。 |
| `bit_index` | 整数 | 已弃用。 |
| `variant_id` | 整数 | 如果为对照组，则为`0`；否则为非零。 |
| `feature_id` | 整数 | 内部功能ID |
| `f_key` | 字符串 | 功能标志键。 |

#### client_analytics_params字段 {#analytics-fields}

| 字段 | 类型 | 描述 |
|---|---|---|
| `app_id` | 整数 | 应用程序ID。 |
| `safe_event_required` | 布尔值 | 如果启用了重定位事件，则为`true`。 |
| `analytics_required` | 布尔值 | 如果禁用Analytics或在默认流上，则为`false`；如果启用Kinesis流，则为`true`。 |

## 示例请求和响应 {#sample}

### 示例请求 {#sample-request}

```http
GET /fg/api/v2/feature?clientId=MyDesktopApp&p=PHSP:17.0:WIN:en_US&meta=true HTTP/1.1
Host: p13n.adobe.io
Authorization: Bearer <ACCESS_TOKEN>
x-api-key: <YOUR_API_KEY>
If-None-Match: <ETAG>
```

### 示例响应 {#sample-response}

```json
{
  "api_version": "0.1",
  "json_version": "0.1",
  "clients": {
    "PHSP:17.0:WIN:en_US": {
      "analyticsVersion": "1.0",
      "releases": []
    },
    "MyDesktopApp": {
      "analyticsVersion": "1.0",
      "client_analytics_params": {
        "app_id": 388,
        "safe_event_required": false,
        "analytics_required": false
      },
      "releases": [
        {
          "bit_index": 160,
          "release_name": "||features||",
          "features": ["feature_a", "feature_b"],
          "release_analytics_params": [
            {
              "app_id": 388,
              "release_id": -1,
              "bit_index": 160,
              "variant_id": 10031741,
              "feature_id": 2918,
              "f_key": "feature_a"
            }
          ],
          "meta": []
        }
      ]
    }
  },
  "ttl": 300
}
```

## 另请参阅 {#see-also}

* [GET功能API V3](get-feature-api-v3.md)
* [桌面应用程序](../guides/integrate/desktop-applications.md)
* [集成步骤](../guides/integrate/integration-steps.md)
