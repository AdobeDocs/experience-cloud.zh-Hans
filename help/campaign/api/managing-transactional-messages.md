---
title: 管理事务型消息
description: 了解如何使用API管理事务性消息。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard迁移的用户"
exl-id: 00d39438-a232-49f1-ae5e-1e98c73397e3
source-git-commit: 110fcdcbefef53677cf213a39f45eb5d446807c2
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 1%

---

# 管理事务型消息 {#managing-transactional-messages}

>[!AVAILABILITY]
>
>目前，使用REST API的事务型消息传递可用于电子邮件和短信渠道。 它仅适用于事务事件(扩充数据仅通过有效负荷可用，与Adobe Campaign V8的操作方式类似)。

创建并发布事务型事件后，您需要将此事件的触发集成到网站中。

例如，您希望每当客户在购物车中购买产品之前离开您的网站时，都会触发“购物车放弃”事件。 要执行此操作，作为Web开发人员，您必须使用REST事务型消息API。

1. 根据POST方法发送请求，这会触发事务性事件的[发送](#sending-a-transactional-event)。
1. 对POST请求的响应包含一个主键，用于通过GET请求发送一个或多个请求。 然后，即可获取[事件状态](#transactional-event-status)。

## 发送事务性事件 {#sending-a-transactional-event}

事务性事件通过具有以下URL结构的POST请求发送：

```
POST https://mc.adobe.io/<ORGANIZATION>/campaign/<transactionalAPI>/<eventID>
```

* **&lt;组织>**：您的个人组织ID。 请参阅[此小节](must-read.md)。

* **&lt;transactionalAPI>**：事务性消息API端点。

  事务性消息API端点的名称取决于您的实例配置。 它与值“mc”相对应，后跟您的个人组织ID。 让我们以Geometrixx公司为例，其组织ID为“geometrixx”。 在这种情况下，POST请求如下：

  `POST https://mc.adobe.io/geometrixx/campaign/mcgeometrixx/<eventID>`

* **&lt;eventID>**：要发送的事件类型。 此ID在创建事件配置时生成

### POST请求标头

请求必须包含“Content-Type： application/json”标头。

您必须添加字符集，例如&#x200B;**utf-8**。 请注意，此值取决于您使用的REST应用程序。

```
-X POST \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>' \
-H 'Content-Type: application/json;charset=utf-8' \
-H 'Content-Length:79' \
```

### post请求正文

事件数据包含在JSON POST正文中。 事件结构取决于其定义。

可以将以下可选参数添加到事件内容，以管理链接到事件的事务型消息的发送：

* **过期**（可选）：在此日期之后，将取消发送事务性事件。
* **已计划**（可选）：从此日期起，将处理事务型事件并发送事务型消息。

>[!NOTE]
>
>“expiration”和“scheduled”参数的值遵循ISO 8601格式。 ISO 8601指定使用大写字母“T”来分隔日期和时间。 但是，可以从输入或输出中删除它以提高可读性。

### 通信信道参数

根据要使用的渠道，有效负载应包含以下参数：

* 电子邮件渠道：“mobilePhone”
* 短信渠道：“电子邮件”

如果有效负载仅包含“mobilePhone”，则将触发短信通信渠道。 如果有效负载只包含“电子邮件”，则将触发电子邮件通信渠道。

以下示例显示了将触发短信通信的有效负载：

```
curl --location 'https://mc.adobe.io/<ORGANIZATION>/campaign/mcAdobe/EVTcartAbandonment' \
--header 'Authorization: Bearer <ACCESS_TOKEN>' \
--header 'Cache-Control: no-cache' \
--header 'X-Api-Key: <API_KEY>' \
--header 'Content-Type: application/json;charset=utf-8' \
--header 'Content-Length: 79' \
--data '
{
  "mobilePhone":"+9999999999",
  "scheduled":"2017-12-01 08:00:00.768Z",
  "expiration":"2017-12-31 08:00:00.768Z",
  "ctx":
  {
    "cartAmount": "$ 125",
    "lastProduct": "Leather motorbike jacket",
    "firstName": "Jack"
  }
}'
```

如果有效负载同时包含“email”和“mobilePhone”，则默认通信方法为email。 要在两个字段都存在时发送短信，您必须使用“widedChannel”参数在有效载荷中明确指定该短信。

### 对POST请求的响应

POST响应会返回创建时的事务性事件状态。 要检索其当前状态（事件数据、事件状态……），请在GET请求中使用POST响应返回的主键：

`GET https://mc.adobe.io/<ORGANIZATION>/campaign/<transactionalAPI>/<eventID>/`

<br/>

***示例请求***

用于发送事件的POST请求。

```
-X POST https://mc.adobe.io/<ORGANIZATION>/campaign/mcAdobe/EVTcartAbandonment \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>' \
-H 'Content-Type: application/json;charset=utf-8' \
-H 'Content-Length:79'

{
  "
  
  
  ":"test@example.com",
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

* **pending**：事件正在挂起 — 该事件在刚刚触发时具有此状态。
* **正在处理**：该事件正在等待投放 — 正在将其转换为消息，并且正在发送该消息。
* **已暂停**：事件进程正在暂停。 它不再被处理，而是保留在Adobe Campaign数据库的队列中。
* **已处理**：事件已处理，消息已成功发送。
* **ignored**：该事件已被投放忽略，通常是在地址处于隔离状态时。
* **deliveryFailed**：处理事件时出现传递错误。
* **routingFailed**：路由阶段失败 — 例如，当找不到指定的事件类型时，可能会发生这种情况。
* **tooOld**：事件在处理之前已过期 — 这可能是由于各种原因造成的，例如，发送多次失败（这会导致事件不再最新），或者服务器在过载后无法再处理事件。
