---
title: 触发信号活动
description: 了解如何使用API触发信号活动。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
exl-id: 9f94e98f-fe04-4369-8946-1380e02cdece
source-git-commit: 14d8cf78192bcad7b89cc70827f5672bd6e07f4a
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 2%

---

# 触发信号活动 {#triggering-a-signal-activity}

在Adobe Campaign Standard工作流中，可以有一个或多个&#x200B;**外部信号**&#x200B;活动。 这些活动是等待触发的“侦听器”。

Campaign StandardAPI允许您触发&#x200B;**外部信号**&#x200B;活动以调用工作流。 API调用可以包含将被摄取到工作流的事件变量中的参数（要定位的受众名称、要导入的文件名、消息内容的一部分等）。 这样，您就可以轻松地将Campaign自动化与外部系统集成。

>[!NOTE]
>
>外部信号活动的触发频度不能超过每10分钟一次，并且目标工作流必须已在运行。

要触发工作流，请执行以下步骤：

1. 对工作流执行&#x200B;**GET**&#x200B;请求以检索外部信号活动触发器URL。

   `GET https://mc.adobe.io/<ORGANIZATION>/campaign/workflow/execution/<workflowID>`

1. 对返回的URL执行&#x200B;**POST**&#x200B;请求以触发信号活动，有效负载中包含&#x200B;**&quot;source&quot;**&#x200B;参数。 此属性是必需的，它允许您指定触发请求源。

如果要使用参数调用工作流，请将其添加到具有&#x200B;**&quot;parameters&quot;**&#x200B;属性的有效负载中。 语法由参数名称及其值组成（支持以下类型：**字符串**、**数字**、**布尔值**&#x200B;和&#x200B;**日期/时间**）。

```
  -X POST <TRIGGER_URL>
  -H 'Authorization: Bearer <ACCESS_TOKEN>' \
  -H 'Cache-Control: no-cache' \
  -H 'X-Api-Key: <API_KEY>' \
  -H 'Content-Type: application/json;charset=utf-8' \
  -H 'Content-Length:79' \
  -i
  -d {
  -d    "source":"<SOURCE>",
  -d    "parameters":{
  -d      "<PARAMETER_NAME":"<PARAMETER_VALUE>",
  -d      "<PARAMETER_NAME":"<PARAMETER_VALUE>",
  -d      "<PARAMETER_NAME":"<PARAMETER_VALUE>",  
  -d      "<PARAMETER_NAME":"<PARAMETER_VALUE>"
  -d    }
  -d }
```

>[!NOTE]
>
>向有效负载添加参数时，请确保其&#x200B;**name**&#x200B;和&#x200B;**type**&#x200B;值与External signal活动中声明的信息一致。 此外，有效负载大小不应超过64Ko。

<br/>

***示例请求***

对工作流执行GET请求。

```
-X GET https://mc.adobe.io/<ORGANIZATION>/campaign/workflow/execution/<workflowID> \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>'
```

它会返回工作流信号活动和关联的触发器URL。

```
{
"PKey": "<PKEY>",
"activities": {
  "activity": {
    "signal1": {
      ...
      "trigger": {
        "href": "https://mc.adobe.io/<ORGANIZATION>/campaign/workflow/execution/<PKEY>/activities/activity/<PKEY>/trigger/"
        },
        ...
      }
    }
  }
}
```

要触发信号活动，请使用“source”对触发器url执行POST请求。 如果要使用参数调用工作流，请添加“参数”属性。

```
-X POST https://mc.adobe.io/<ORGANIZATION>/campaign/workflow/execution/<PKEY>/activities/activity/<PKEY>/trigger \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer <ACCESS_TOKEN>' \
-H 'Cache-Control: no-cache' \
-H 'X-Api-Key: <API_KEY>' \
-i
-d '{
-d "source":"API",
-d "parameters":{
-d    "audience":"audience",
-d    "email":"anna.varney@mail.com",
-d    "template":"05",
-d    "contentURL":"http://www.adobe.com",
-d    "test":"true",
-d    "segmentCode":"my segment",
-d    "attribute":"2019-04-03 08:17:19.100Z"}
-d  }'
```

<!-- + réponse -->

如果未在外部信号活动中声明其中一个参数，则POST请求会返回以下错误，指示缺少哪个参数。

```
RST-360011 An error has occurred - please contact your administrator.
'contentURL' parameter isn't defined in signal activity.
XTK-170006 Unable to parse expression 'HandleTrigger(@name, $(source), $({parameters}))'.
RST-360000 Error while assessing 'HandleTrigger(@name, $(source), $({parameters}))' expression ('xtk:workflow:execution/activities/signal/trigger' resource)
```
