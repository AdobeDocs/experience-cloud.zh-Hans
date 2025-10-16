---
title: API疑难解答
description: 进一步了解与Campaign Standard API相关的常见问题
role: Developer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard迁移的用户"
source-git-commit: 11c49b273164b632bcffb7de01890c6f9d7ae9c2
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---

# API疑难解答 {#troubleshooting}

* **在转到Adobe.io控制台时，您会收到以下错误：“Adobe I/O控制台仅适用于企业帐户的选定成员。 如果您认为您应该拥有访问权限，请联系您的系统管理员。&quot;**

您只能为您所管理的组织创建API密钥。 如果显示此消息并且您希望创建API密钥，并且您希望询问组织的管理员之一。

* **向Adobe.io发出请求时，您收到{&quot;error_code&quot;：&quot;403023&quot;，&quot;message&quot;：&quot;Profile is not valid&quot;}**

这意味着您的特定Campaign产品的IMS配置存在问题：IMS团队需要修复该问题。

要获取更多详细信息，您可以使用令牌调用IMS API，以查看您的IMS配置文件是什么样的：您需要一个prodCtx，其中organization_id与您放置在Adobe.io URL中的相同，以便能够路由您的请求。
如果缺少IMS配置，则需要修复。

```
-X GET https://mc.adobe.io/{ORGANIZATION}/campaign/profileAndServices/profile \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

它会返回以下错误。

```
{"error_code":"403023","message":"Profile is not valid"}
```

使用此请求检查您的IMS配置文件。

```
-X GET https://ims-na1.adobelogin.com/ims/profile/v1 \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

在响应中，ORGANIZATION_ID值必须在您的第一个GET请求中相同。

```
{
  "countryCode": "FR",
  "mrktPermEmail": null,
  "projectedProductContext": [
    {
    "prodCtx": {
      "statusCode": "ACTIVE",
      "ident": "ZQ9FRQK7BF09YXAESFY9DDQP1G",
      "modDts": 1448307260000,
      "organization_id": "actest",
      "owningEntity": "6096892F54B5819E0A4C98A2@AdobeOrg",
      "serviceCode": "dma_tartan",
      "label": "Adobe Marketing Cloud",
      "serviceLevel": "standard",
      "createDts": 1421181343000,
      "deal_id": " "
      }
    }
  ]
}
```

* **向Adobe.io发出请求时，您会收到{&quot;code&quot;:500、&quot;message&quot;：&quot;Oops. 发生错误。 请检查您的URI并重试。&quot;}**

Adobe.io声明您的URI无效：您请求的URI很可能无效。 在Adobe.io上，当您选择Campaign服务时，您会获得一个选取器，其中包含可能的organization_id列表。 您需要检查您选择的就是您放入URL中的服务器。

* **向Adobe.io发出请求时，您收到{&quot;error_code&quot;：&quot;401013&quot;，&quot;message&quot;：&quot;Oauth令牌无效&quot;}**

您的令牌无效（用于生成令牌的IMS调用不正确）或您的令牌已过期。

* **创建后看不到我的个人资料**

根据实例配置，创建的配置文件需要关联到&#x200B;**orgUnit**。 若要了解如何在创建时添加此字段，请参阅[此章节](creating-profiles-api.md)。

<!-- * (error duplicate key : quand tu crées un profile qui existe déjà , il faut faire un patch pour updater le profile plutôt qu'un POST)

With Curl
List all profiles

Create a profile

Update the mobilePhone attribute of a profile

API Calls on Service

GET the list of services

-->

<!--

How to find and use a filter?
Error codes:

* PAtch sur Age = message d'erreur :
500
Cannot update the 'age' property that is read-only
'age' property is not valid for the 'profile' resource.
-->

<!--
How to filter a list of subscribed profiles with available profile filters ? by date (by les filtres dispo sur la ressource) ?

Pattern classique :

recupérer la liste des subscriptions filtrées d'un profile
1) get sur profile
2) recup PKey
3) get sur PKey
4) get sur href des subscriptions

Comment savoir quel filtre appliquer ?

1) get sur metadata de profile
2) retourne description de la collection subscription
3) get sur la valeur du champ resTarget
4) get sur le href dans filters
5) retourne les filtres applicables sur l'url des data.

-->
