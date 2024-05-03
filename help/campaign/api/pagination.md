---
title: 分页
description: 了解如何执行分页操作。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
source-git-commit: 84b72258789ba61016deb813e93bdca0ea142712
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---

# 分页

默认情况下，一个列表中加载25个资源。

此 **_lineCount** 参数允许您限制响应中列出的资源数。  然后，您可以使用 **下一个** 节点，显示下一个结果。

>[!NOTE]
>
>始终使用返回的URL值 **下一个** 节点，以执行分页请求。
>
>此 **_lineStart** 计算请求后，必须始终在 **下一个** 节点。

<br/>

***示例请求***

用于显示配置文件资源1条记录的示例GET请求。

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile?_lineCount=1 \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

对请求的响应，使用 **下一个** 节点以执行分页。

```
{
    "content": [
        {
            "PKey": "<PKEY>",
            "firstName": "John",
            "lastName":"Doe",
            "birthDate": "1980-10-24",
            ...
        }
    ],
    "next": {
        "href": "https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile/email?_lineCount=10&_
        lineStart=@Qy2MRJCS67PFf8soTf4BzF7BXsq1Gbkp_e5lLj1TbE7HJKqc"
    }
    ...
}
```

默认情况下， **下一个** 在与具有大量数据的表交互时，节点不可用。 为了能够执行分页，您必须添加 **_forcePagination=true** 参数到调用URL。

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile?_forcePagination=true \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

>[!NOTE]
>
>在Campaign Standard中定义了一个表，超过该表被视为大型的记录数 **XtkBigTableThreshold** 选项。 默认值为100,000条记录。
