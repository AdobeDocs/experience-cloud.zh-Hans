---
title: 自定义资源
description: 了解有关使用API进行自定义资源管理的更多信息/
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Developer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard迁移的用户"
exl-id: d7b2231d-46ff-4966-9ea7-27a775e5236b
source-git-commit: 11c49b273164b632bcffb7de01890c6f9d7ae9c2
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 2%

---

# 自定义资源 {#custom-resources}

Adobe Campaign附带预定义数据模型，其中数据通过不同资源进行定义。 您可以通过扩展资源以添加自己的自定义字段或自定义表（如采购表或产品表）来扩充提供的数据模型。

可使用&#x200B;**/profileAndServicesExt**&#x200B;端点和自定义资源名称通过API访问自定义资源。

`https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServicesExt/<resourceName>/`

>[!NOTE]
>
>对于非现成可用的资源，请始终在资源名称前使用<b>&quot;cus&quot;</b>前缀。

您可以使用自定义资源执行任何操作，只要这些资源链接到用户档案表即可。 例如，我们来看看下面的表结构：

![替换文本](assets/cusresources.png)

在这种情况下，只要来自&#x200B;**Transaction**、**TransactionDetails**&#x200B;和&#x200B;**Product**&#x200B;表的所有资源链接到&#x200B;**Profile**&#x200B;表，这些资源即可使用。

<br/>

***示例请求***

访问扩展的profileAndServicesExt资源的GET请求示例。

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServicesExt/\
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>' \
```

它会返回所有链接的自定义资源的列表。 然后，您可以使用资源URL来执行本文档中描述的任何API任务。

```
{
"apiName": "resourceType",
"cusProduct": {
        "content": ...,
        "data": "/profileAndServicesExt/cusProduct/",
        "help": "Product",
        "href": "https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServicesExt/cusProduct/metadata",
        "name": "cusProduct",
        "type": "collection"
    },
"cusTransaction": {
        "content": ...,
        "data": "/profileAndServicesExt/cusTransaction/",
        "help": "Product",
        "href": "https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServicesExt/cusTransaction/metadata",
        "name": "cusProduct",
        "type": "collection"
    },
    ...
}
```
