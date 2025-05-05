---
title: 控制工作流
description: 了解如何使用API控制工作流。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
exl-id: 79eacc31-d5a2-4e13-aa0b-744d7ab7004f
source-git-commit: 14d8cf78192bcad7b89cc70827f5672bd6e07f4a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 10%

---

# 控制工作流 {#controlling-a-workflow}

您可以通过包含工作流ID和所需执行命令的POST请求，直接从REST API控制工作流：

`POST https://mc.adobe.io/<ORGANIZATION>/campaign/workflow/execution/<workflowID>/commands`

>[!CAUTION]
>
>如果在Adobe Campaign中更改了工作流ID，则API请求将不再有效。

有四个执行命令可用于控制工作流：

* 开始
* 暂停
* 继续
* 停止

有关执行命令的详细信息，请参阅[Campaign文档](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/executing-a-workflow/about-workflow-execution.html?lang=zh-Hans)。

<br/>

***示例请求***

* 启动工作流。

  ```
  -X POST https://mc.adobe.io/<ORGANIZATION>/campaign/workflow/execution/<workflowID>/commands \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <ACCESS_TOKEN>' \
  -H 'Cache-Control: no-cache' \
  -H 'X-Api-Key: <API_KEY>' \
  -i
  -d '{"method":"start"}'
  ```

  <!-- + réponse -->

* 停止工作流。

  ```
  -X POST https://mc.adobe.io/<ORGANIZATION>/campaign/workflow/execution/<workflowID>/commands \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <ACCESS_TOKEN>' \
  -H 'Cache-Control: no-cache' \
  -H 'X-Api-Key: <API_KEY>' \
  -i
  -d '{"method":"stop"}'
  ```

  <!-- + réponse -->
