---
title: 自定义资源
description: 了解有关使用API进行自定义资源管理的更多信息/
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
source-git-commit: 84b72258789ba61016deb813e93bdca0ea142712
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 2%

---

# 自定义资源 {#custom-resources}

Adobe Campaign附带预定义数据模型，其中数据通过不同资源进行定义。 您可以通过扩展资源以添加自己的自定义字段或自定义表（如采购表或产品表）来扩充提供的数据模型。

可通过API使用访问自定义资源 **/profileAndServicesExt** 端点和自定义资源名称。

`https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServicesExt/<resourceName>/`

>[!NOTE]
>
>对于非开箱即用的资源，请始终使用 <b>&quot;cus&quot;</b> 在资源名称之前添加前缀。

您可以使用自定义资源执行任何操作，只要这些资源链接到用户档案表即可。 例如，我们来看看下面的表结构：

![替换文本](assets/cusresources.png)

在这种情况下，来自 **交易**， **交易详细信息** 和 **产品** 只要表链接到 **个人资料** 表格。

<br/>

***示例请求***

访问扩展的profileAndServicesExt资源的示例GET请求。

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
