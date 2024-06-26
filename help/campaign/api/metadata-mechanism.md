---
title: 元数据机制
description: 了解有关元数据机制的更多信息。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
source-git-commit: 84b72258789ba61016deb813e93bdca0ea142712
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 1%

---

# 元数据机制 {#metadata-mechanism}

您可以使用检索资源元数据 **resourceType** 在GET请求中：

`GET /profileAndServices/resourceType/<resourceName>`

响应会从资源返回主元数据（所有其他字段均为描述性或内部字段）：

* 此 **内容** 节点返回资源的字段。 对于 **内容** 节点，可以找到以下字段：

   * “apiName”： API中使用的属性的名称。
   * &quot;type&quot;：这是高级类型定义（字符串、数字、链接、收藏集、枚举……）。
   * “dataPolicy”：字段的值必须遵循给定的策略规则。 例如，如果dataPolicy规则设置为“email”，则该值必须是有效的电子邮件。 在PATCH或POST期间，dataPolicy可以检查值或修改值以进行转换（例如smartCase）。
   * &quot;category&quot;：在查询编辑器中提供字段的类别。
   * &quot;resType&quot;：这是技术类型。

     如果“type”以值“link”或“collection”结束，则resTarget值是链接所定向资源的名称。
如果“type”以“enumeration”值完成，则会添加“values”字段，并且每个枚举值在中都会详细说明 **值** 节点。

* 此 **过滤器** 节点会返回用于检索关联过滤器的URL。 有关筛选器的更多信息，请参阅 [本节](filtering.md) 部分。

<!-- créer une section au même niveau sur les liens -->
<!-- dans l'exemple: birthdate, email +  mettre 2 liens : un de type 1-1 , 1-N
si on prend l'exemple de l'org unit, on aura un bon exemple lien -->
<!-- plus reparler du node Data -->

<br/>

***示例请求***

对资源执行GET请求。

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/resourceType/profile \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

它会返回用户档案资源的完整描述。

```
{
...
"content": {
  "email": {...},
    ...
    },
"data": "/profileAndServices/profile/",
"filters": {
        "href": "https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/resourceType/<PKEY>"
    },
"help": "Identified profiles",
"href": "https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile/metadata",
"label": "Profiles",
"mandatory": false,
"name": "profile",
"pkgStatus": "never",
"readOnly": false,
"schema": "nms:recipient",
"type": "item"
}
```
