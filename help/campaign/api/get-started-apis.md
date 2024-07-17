---
title: Campaign REST API入门
description: 通过将 Campaign 与一组技术建立联系，创建集成并构建您自己的生态系统。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
exl-id: c6968252-a012-4029-bbb8-66f4f693e99b
source-git-commit: 14d8cf78192bcad7b89cc70827f5672bd6e07f4a
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 48%

---

# Campaign REST API入门 {#get-started-apis}

>[!CAUTION]
>
>本文档适用于迁移到Campaign v8的Adobe Campaign Standard客户。
>
>在执行 API 调用之前，请检查与您的许可协议对应的比例限制。有关详细信息，请参见[此页面](https://helpx.adobe.com/legal/product-descriptions/campaign-standard.html#ITInfrastructureResourcesbyActiveProfilesTiers)。

Campaign REST API旨在通过将Adobe Campaign与您使用的技术面板连接，让您&#x200B;**为Adobe Campaign创建集成**，并&#x200B;**构建您自己的生态系统**。

通过Adobe Campaign REST API，您可以访问以下功能：

<table><tr>
 <td valign="top"><a href="retrieving-profiles.md"><img width="60px" alt="条件" src="assets/icon_profile.svg"/></a><p><a href="retrieving-profiles.md">配置文件</a></p></td>
<td valign="top"><a href="creating-a-service.md"><img width="60px" alt="条件" src="assets/icon_services.svg"/></a><p><a href="creating-a-service.md">服务和订阅</a></p></td>
<td valign="top"><a href="interacting-with-custom-resources.md"><img width="60px" alt="条件" src="assets/icon_customresources.svg"/></a><p><a href="interacting-with-custom-resources.md">自定义资源</a></p></td>
<td valign="top"><a href="controlling-a-workflow.md"><img width="60px" alt="条件" src="assets/icon_workflows.svg"/></a><p><a href="controlling-a-workflow.md">工作流</a></p></td>
</tr></table>

要使用Campaign REST API，您需要Adobe I/O帐户。 这是前进和发现 API 功能的必备第一步。
有关详细信息，请参阅[此部分](setting-up-api-access.md)。

我们提供的 API 使用 REST 接口的&#x200B;**标准概念**&#x200B;以及 JSON 负载。

本文档中对所有端点进行了详尽的描述，其中包含您应当了解的关于操作API、完整API引用、代码示例和快速入门指南的一般概念。 所有示例都适用于 Postman，但可随意使用您最喜爱的 REST 客户端。

如果有任何内容缺失或错误，请咨询[社区](https://experienceleaguecommunities.adobe.com/t5/adobe-campaign-standard/ct-p/adobe-campaign-standard-community)。
