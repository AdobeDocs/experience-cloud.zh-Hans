---
title: 使用API创建用户档案
description: 了解有关如何使用API创建用户档案的更多信息。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Developer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard迁移的用户"
exl-id: 69e8d034-6bdd-4b82-bcd7-1ef4be0a59b3
source-git-commit: 11c49b273164b632bcffb7de01890c6f9d7ae9c2
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# 使用API创建用户档案 {#creating-profiles-api}

创建配置文件是通过配置文件资源上的&#x200B;**POST**&#x200B;请求执行的。

>[!CAUTION]
>
>如果要将<b>orgUnit</b>关联到已创建的配置文件，则需要使用此字段扩展配置文件资源，并且在发布扩展后，对<b>ProfileAndServicesExt</b>端点执行POST请求。
>
>有关用户档案资源扩展的更多信息，请参阅<a href="https://helpx.adobe.com/cn/campaign/standard/administration/using/organizational-units.html#partitioning-profiles">Campaign文档</a>。

<br/>

***示例请求***

使用电子邮件“john.doe@mail.com”创建用户档案的示例POST请求。

```
-X POST https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServices/profile \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>' \
-i
-d '{"email":"john.doe@mail.com"}'
```

它会返回新创建的配置文件，并带有“john.doe@mail.com”电子邮件地址。

```
{
    "PKey": "<PKEY>",
    "firstName": "John",
    "lastName":"Doe",
    "birthDate": "1980-10-24",
    "email": "john.doe@mail.com",
    ...
}
```
