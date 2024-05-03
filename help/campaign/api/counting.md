---
title: 计数
description: 了解如何执行计数操作。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
source-git-commit: 84b72258789ba61016deb813e93bdca0ea142712
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 2%

---

# 计数

Adobe Campaign REST API可以计算请求中的记录数。 要实现此目的，请使用返回的URL **count** 节点。

<br/>

***示例请求***

计算所有具有 **messageType** 等于“sms”的值，使用执行GET请求 **byChannel** 筛选。

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/service/byChannel?channel=sms \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

它会返回与过滤器对应的服务。

```
{
    "content": [
        {
            ...
            "messageType": "sms",
            "mode": "newsletter",
            "name": "SVC6",
            ...
        },
        ...
    ],
    "count": {
        "href": "https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/service/byChannel/_count?channel=sms&_lineStart=@iKTZ2q3IiSEDqZ5Nw1vdoGnQCqF-8DAUJRaVwR9obqqTxhMy"
    },
    "serverSidePagination": true
}
```

对执行GET **count** 用于检索结果数的节点的URL。

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/service/byChannel/_count?channel=sms&_lineStart=@iKTZ2q3IiSEDqZ5Nw1vdoGnQCqF-8DAUJRaVwR9obqqTxhMy \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

它返回记录数。

```
{
    "count": 26
}
```
