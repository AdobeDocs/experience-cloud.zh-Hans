---
title: 必读
description: 在使用API之前必须先读取。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Developer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard迁移的用户"
exl-id: 9e2d1b59-55a5-4715-adfb-35191a9df536
source-git-commit: 11c49b273164b632bcffb7de01890c6f9d7ae9c2
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# 必读 {#must-read}

## 技术要求

* Adobe Campaign API必须仅用于“服务器到服务器”。
* 如果您要实施的用例与Adobe API允许的规模一致，请始终与您的Adobe Campaign技术联系人核实。
* 设置AdobeIO访问需要特定权限，如果遇到任何问题，请与Adobe支持部门联系。

## 权限和访问

* 默认情况下，Adobe Campaign API使用管理员上下文，因此组织单位和角色不适用。
* Adobe Campaign API将从角色上下文中排除。
* 如果要使用一个或多个组织单位配置API，请先与您的Adobe技术联系人联系。

## 资源表示

所有API资源都可在&#x200B;**JSON**&#x200B;中使用，扩展名为URL，或位于HTTP接受标头内：

`GET /profileAndServices/<resourceName>.json`

>[!NOTE]
>
>在URL中没有扩展名，**json格式是内容类型的默认格式**。

<br/>

***请求样本***

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile.json \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

## 主键和URL

* 不要尝试自己构建URL。 所有URL均由API返回。 但是，可以根据顶级资源名称构建URL。

* 说明示例的自动主键(PKey)值不适用于其他特定部署。 它们由Adobe Campaign API生成。

* 绝不能将Adobe Campaign生成的自动主键值存储到外部数据库或网站中。 您必须在数据库定义中生成特定的键字段，并在开发过程中使用它。

## 自定义密匙 {#custom-keys}

如果用户档案资源已通过自定义键字段扩展，则可以使用此字段作为键，而不是Adobe Campaign生成的自动主键：

`GET /.../profileAndServicesExt/profile/<customKey>`

如果键值不同于原始键，或者您将自己的业务键用作URI，而不是Adobe提供的业务键，则无法使用PATCH操作修改自定义键。

仅对&#x200B;**顶层配置文件资源**&#x200B;使用自定义键。 URL由API返回，绝不应该自行构建。

<br/>

***示例请求***

要使用自定义键检索用户档案的订阅，请对自定义键执行GET操作。

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServicesExt/profile/<customKey> \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

对返回的订阅URL执行GET请求。

```
-X GET <SUBSCRIPTION_URL> \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

它会返回用户档案的订阅列表。

```
"service": {
"PKey": "<PKEY>",
"href": "https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/service/<PKEY>",
"label": "Sport Newsletter",
"name": "SVC1",
"title": "Sport Newsletter (SVC1)"
}
```
