---
title: 使用API创建用户档案
description: 了解有关如何使用API创建用户档案的更多信息。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
source-git-commit: 84b72258789ba61016deb813e93bdca0ea142712
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# 使用API创建用户档案 {#creating-profiles-api}

创建用户档案是通过执行 **POST** 请求。

>[!CAUTION]
>
>如果要关联 <b>orgUnit</b> POST对于已创建的配置文件，您需要使用此字段扩展配置文件资源，并在发布扩展后，对 <b>配置文件和服务扩展</b> 端点。
>
>有关用户档案资源扩展的更多信息，请参阅 <a href="https://helpx.adobe.com/campaign/standard/administration/using/organizational-units.html#partitioning-profiles">Campaign文档</a>.

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
