---
title: 删除订阅
description: 了解如何使用API删除订阅
role: Data Engineer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
source-git-commit: 84b72258789ba61016deb813e93bdca0ea142712
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# 删除具有API的订阅 {#mdeleting-subscriptions-api}

<!--NOTE TO WRITER: There are two duplicate headings that seem to have the same content. Delete one? Rename if different?-->

## 删除特定配置文件的服务订阅 {#deleting-service-subscription}

此过程分为三个步骤。

1. 检索所需配置文件的订阅URL。
1. 对预订URL执行GET请求。
1. 对所需的服务URL执行DELETE请求。

如果删除请求成功，则响应状态为204 No Content。

<br/>

***示例请求***

以下负载示例显示了如何取消订阅服务的配置文件。 首先执行GET请求以检索配置文件。

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

它会返回所选配置文件的订阅列表，以及每个订阅服务的URL。

```
...
"service": {
  "PKey": "<PKEY>",
  "href": "https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/service/<PKEY>",
  "label": "Sport Newsletter",
  "name": "SVC1",
  "title": "Sport Newsletter (SVC1)"
},
...
```

对所需的服务URL执行DELETE请求。

```
-X DELETE https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/service/<PKEY> \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

<!-- + réponse -->

## 删除特定配置文件的服务订阅

此过程分为三个步骤。

1. 检索所需的服务及其订阅URL。
1. 对订阅URL执行GET请求以检索所有配置文件订阅。
1. 对所需的配置文件订阅URL执行DELETE请求。

如果删除请求成功，则响应状态为204 No Content。

<br/>

***示例请求***

检索服务记录。

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
  "mode": "newsletter",
  "name": "SVC3",
  "subScenarioEventType": "subscriptionEvent",
  "subscriptions": {
    "href": "https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/service/<PKEY>/subscriptions/"
  },
  "targetResource": "profile",
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

它会返回所选服务的订阅列表，并为每个用户档案订阅返回一个URL (href)。

```
{
  "PKey": "<PKEY>",
  "created": "2019-03-26 08:58:04.764Z",
  "email": "",
  "expirationDate": "",
  "href": "https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/service/<PKEY>/subscriptions/<PKEY>",
  "metadata": "subscriptionRcp",
  "service": ...,
  "serviceName": "SVC3",
  "subscriber": ...,
  ...
}
```

对所需的配置文件订阅URL执行DELETE请求。

```
-X DELETE https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/service/<PKEY>/subscriptions/<PKEY> \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

<!-- + réponse -->
