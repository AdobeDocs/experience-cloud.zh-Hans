---
title: 与自定义资源交互
description: 了解有关使用API进行自定义资源管理的更多信息/
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
exl-id: 19bfeecb-da60-479c-a929-0cfb72ef59e3
source-git-commit: 3f4400f24b75e8e435610afbe49e9d9444dbf563
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 与自定义资源交互 {#interacting-with-custom-resources}

此 **/customResources** 端点允许您在REST中公开Campaign自定义资源。 基于此API，可在自定义实体和外部端点之间实现集成。

/customResources端点的行为与/profileAndServices端点完全相同。

此API中公开的自定义资源包括：

* 所有未在/profileAndServicesExt下公开的实体
* 所有与个人资料无关的实体，对于这些实体，还包括其子代和孙代。
* 默认情况下，所有未链接到任何内容的实体及其子项和孙项。

>[!NOTE]
>/profileAndServicesExt下可用的自定义资源不会在/customResources API中公开。


以下是从自定义资源检索元数据的示例：

```
GET /customResources/resourceType/<customResourceName>
```

要执行创建、更新或删除，请使用GET、POST、PATCH、DELETE。

```
POST /customResources/<customResourceName>
```
