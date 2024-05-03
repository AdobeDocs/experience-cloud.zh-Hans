---
title: 端点
description: 了解有关API端点的更多信息。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
source-git-commit: 84b72258789ba61016deb813e93bdca0ea142712
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 9%

---

# 端点 {#endpoints}

Adobe Campaign REST API的可用端点：

* **/profileAndServices**：与开箱即用的字段交互。 不能使用此端点访问扩展字段。
* **/profileAndServicesExt**：与Profile或Services自定义资源扩展期间添加的自定义字段交互。 有关自定义资源的更多信息，请参阅 [本节](custom-resources.md).
* **/&lt;transactionalapi>**：与事务型消息API交互（事务型消息API端点的名称取决于您的实例配置）。 有关详细信息，请参阅[此部分](managing-transactional-messages.md)。
* **/workflow/execution**：与工作流交互。 有关详细信息，请参阅[此部分](controlling-a-workflow.md)。

默认情况下，主要资源可用于 **配置文件与服务** 和 **profileAndServiceExt** API包括：

* **/profile**：与Campaign数据库中的用户档案交互。 要将配置文件添加到服务，请使用 **/service** 端点。 有关Campaign用户档案的更多信息，请参阅 [Campaign文档](https://helpx.adobe.com/campaign/standard/audiences/using/about-profiles.html).
* **/service**：管理订阅服务。 有关Campaign中服务的更多信息，请参阅 [Campaign文档](https://helpx.adobe.com/campaign/standard/audiences/using/creating-a-service.html).

>[!NOTE]
>
>已扩展或创建的所有其他资源均可通过以下网站获取： **配置文件和服务扩展** 仅限API。 它们必须链接到 **个人资料** 资源。
