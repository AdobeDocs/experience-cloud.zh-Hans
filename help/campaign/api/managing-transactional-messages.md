---
title: 管理事务型消息
description: 了解如何使用API管理事务性消息。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
hidefromtoc: true
hide: true
role: Data Engineer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
exl-id: 00d39438-a232-49f1-ae5e-1e98c73397e3
source-git-commit: 3f4400f24b75e8e435610afbe49e9d9444dbf563
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 1%

---

# 管理事务型消息 {#managing-transactional-messages}

创建并发布事务型事件后，您需要将此事件的触发集成到网站中。

例如，您希望每当客户在购物车中购买产品之前离开您的网站时，都会触发“购物车放弃”事件。 要执行此操作，作为Web开发人员，您必须使用REST事务型消息API。

1. 根据POST方法发送请求，这会触发 [发送事务性事件](#sending-a-transactional-event).
1. 对POST请求的响应包含主键，该主键允许您通过GET请求发送一个或多个请求。 然后，您便可以获取 [事件状态](#transactional-event-status).

## 发送事务性事件 {#sending-a-transactional-event}

事务性事件通过具有以下URL结构的POST请求发送：

```
POST https://mc.adobe.io/<ORGANIZATION>/campaign/<transactionalAPI>/<eventID>
```

* **&lt;organization>**：您的个人组织ID。 请参阅[此小节](must-read.md)。

* **&lt;transactionalapi>**：事务型消息API端点。

  事务性消息API端点的名称取决于您的实例配置。 它与值“mc”相对应，后跟您的个人组织ID。 让我们以“geometrixx”作为其组织ID的Geometrixx公司为例。 在这种情况下，POST要求如下：

  `POST https://mc.adobe.io/geometrixx/campaign/mcgeometrixx/<eventID>`

  请注意，事务性消息API端点在API预览期间也可见。

* **&lt;eventid>**：要发送的事件类型。 此ID在创建事件配置时生成

### 请求标头POST

请求必须包含“Content-Type： application/json”标头。

例如，必须添加字符集 **utf-8**. 请注意，此值取决于您使用的REST应用程序。

```
-X POST \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>' \
-H 'Content-Type: application/json;charset=utf-8' \
-H 'Content-Length:79' \
```

### POST请求正文

事件数据包含在JSONPOST正文中。 事件结构取决于其定义。 资源定义屏幕中的API预览按钮提供了一个请求示例。

可以将以下可选参数添加到事件内容，以管理链接到事件的事务型消息的发送：

* **过期** （可选）：在此日期之后，事务性事件的发送将被取消。
* **已计划** （可选）：从此日期起，将处理事务型事件并发送事务型消息。

>[!NOTE]
>
>“expiration”和“scheduled”参数的值遵循ISO 8601格式。 ISO 8601指定使用大写字母“T”来分隔日期和时间。 但是，可以从输入或输出中删除它以提高可读性。

### 对POST请求的响应

POST响应将返回创建时的事务性事件状态。 要检索其当前状态（事件数据、事件状态……），请在GET请求中使用POST响应返回的主键：

`GET https://mc.adobe.io/<ORGANIZATION>/campaign/<transactionalAPI>/<eventID>/`

<br/>

***示例请求***

发送事件的POST请求。

```
-X POST https://mc.adobe.io/<ORGANIZATION>/campaign/mcAdobe/EVTcartAbandonment \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>' \
-H 'Content-Type: application/json;charset=utf-8' \
-H 'Content-Length:79'

{
  "email":"test@example.com",
  "scheduled":"2017-12-01 08:00:00.768Z",
  "expiration":"2017-12-31 08:00:00.768Z",
  "ctx":
  {
    "cartAmount": "$ 125",
    "lastProduct": "Leather motorbike jacket",
    "firstName": "Jack"
  }
}
```

对POST请求的响应。

```
{
  "PKey":"<PKEY>",
  "ctx":
  {
    "cartAmount": "",
    "lastProduct": "",
    "firstName": ""
  }
  "email":"",
  "scheduled":"2017-12-01 08:00:00.768Z",
  "expiration":"2017-12-31 08:00:00.768Z",
  "href": "mcAdobe/EVTcartAbandonment/<PKEY>",
  "serverUrl":" https://myserver.com ",
  "status":"pending",
  "type":""
}
```

### 事务性事件状态 {#transactional-event-status}

在响应中，“status”字段让您知道事件是否已处理：

* **待处理**：事件处于待处理状态 — 在刚刚触发时，事件会采用此状态。
* **正在处理**：事件正在等待投放 — 正在将其转换为消息并发送消息。
* **已暂停**：正在暂停事件进程。 它不再被处理，而是保留在Adobe Campaign数据库的队列中。
* **已处理**：事件已处理，消息已成功发送。
* **已忽略**：投放忽略了事件，通常在地址处于隔离状态时这样做。
* **deliveryFailed**：处理事件时出现投放错误。
* **routingFailed**：路由阶段失败 — 例如，当找不到指定的事件类型时，可能会发生此情况。
* **tooOld**：事件在处理之前过期 — 例如，由于多次发送失败（这会导致事件不再最新）或服务器在重载后无法再处理事件等原因，可能会发生这种情况。
* **定位失败**：Campaign Standard未能扩充用于消息定向的链接。
