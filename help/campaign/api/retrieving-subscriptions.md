---
title: 检索订阅
description: 了解如何使用API检索订阅
role: Data Engineer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
source-git-commit: 84b72258789ba61016deb813e93bdca0ea142712
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 使用API检索订阅 {#retrieving-subscriptions-api}

## 检索订阅服务的用户档案

此过程分为两步。

1. 检索所需服务的订阅URL。
1. 对预订URL执行GET请求。 它会返回服务的订阅列表，以及每个关联的配置文件。

>[!CAUTION]
>
>REST API返回“href”属性，该属性包含要使用的URL。 <b>始终使用响应中包含的URL发出后续API请求</b>.

<br/>

***示例请求***

执行GET请求以检索服务。

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/service/<PKEY> \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

它会返回服务的订阅URL。

```
  {
    ...
    "messageType": "email",
    "name": "SVC1",
    "subscriptions": {
                "href": "https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/service/<PKEY>/subscriptions/"
    },
    ...
  },
```

对预订URL执行GET请求。

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/service/<PKEY>/subscriptions \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

此时将显示服务订阅列表，其中包含每个关联的配置文件。

```
  {
    ...
    "service": ...,
    "serviceName": "SVC3",
    "subscriber": {
        "PKey": "<PKEY>",
        "email": "",
        "firstName": "John",
        "href": "https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile/<PKEY>",
        "lastName": "Doe",
    },
  }
```

## 检索用户档案订阅的服务

此过程分为两步。

1. 检索给定配置文件的订阅URL。
1. 对URL执行GET请求。 它会返回用户档案的订阅列表，以及每个关联的服务。

<br/>

***示例请求***

执行GET请求以检索配置文件。

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile/<PKEY> \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

它会返回用户档案的订阅URL。

```
  {
    ...
    "postalAddress":...,
    "preferredLanguage": "none",
    "subscriptions": {
      "href": "https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile/<PKEY>/subscriptions/"
    },
    ...
  }
```

对预订URL执行GET请求。

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile/<PKEY>/subscriptions \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

它会返回用户档案订阅的服务列表。

```
  {
    ...
    "PKey": "<PKEY>",
    "created": "2017-03-03 10:54:00.363Z",
    "service": {
      "PKey": "<PKEY>",
      "href": "https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/service/<PKEY>",
      "label": "Sport Newsletter",
      "name": "SVC1",
      "title": "Sport Newsletter (SVC1)"
    },
    ...
  }
```
