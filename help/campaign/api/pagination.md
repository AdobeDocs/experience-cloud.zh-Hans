---
title: 分页
description: 了解如何执行分页操作。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Developer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard迁移的用户"
exl-id: d6ebce3c-1e84-4b3b-a68d-90df4680af64
source-git-commit: 11c49b273164b632bcffb7de01890c6f9d7ae9c2
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---

# 分页

默认情况下，一个列表中加载25个资源。

**_lineCount**&#x200B;参数允许您限制响应中列出的资源数。  然后，可以使用&#x200B;**next**&#x200B;节点显示下一个结果。

>[!NOTE]
>
>始终使用&#x200B;**next**&#x200B;节点中返回的URL值执行分页请求。
>
>已计算&#x200B;**_lineStart**&#x200B;请求，必须始终在&#x200B;**next**&#x200B;节点中返回的URL中使用。

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

响应请求，使用&#x200B;**next**&#x200B;节点执行分页。

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

默认情况下，在与具有大量数据的表交互时，**next**&#x200B;节点不可用。 若要执行分页，必须将&#x200B;**_forcePagination=true**&#x200B;参数添加到调用URL中。

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile?_forcePagination=true \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

>[!NOTE]
>
>在Campaign Standard **XtkBigTableThreshold**&#x200B;选项中定义了表大于此值的记录数。 默认值为100,000条记录。
