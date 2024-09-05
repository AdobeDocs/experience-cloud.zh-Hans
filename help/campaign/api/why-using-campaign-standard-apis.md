---
title: 为何使用Campaign StandardAPI？
description: 了解有关Campaign StandardAPI以及为何使用它们的更多信息。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
exl-id: ef045e5d-cd02-44a0-9a1e-d468483a38d9
source-git-commit: 6e4e214731b9772014d01dde89b3f80e4c4e93a6
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 1%

---

# 为何使用Campaign StandardAPI {#why-using-campaign-standard-apis}

Adobe Campaign Standard提供了API，允许现有系统与Campaign平台集成，实时解决现实世界中的问题。

注册或选择退出页面等公共网站需要连接到后端系统以存储配置文件信息。 像Adobe Campaign这样的后端系统灵活而强大，能够将配置文件数据摄取到其中并对其执行自定义操作。

以下是一些示例：

* 潜在客户在线注册。
* 现有的客户个人资料和营销通信偏好管理。
  <!--* Event based transactional communication triggering – order confirmation, booking Itinerary, password reset, etc.-->
* 甚至放弃电子邮件通信。

注册登陆页面为客户或潜在客户提供了一种注册其姓名和电子邮件地址的方法。 一旦Campaign Standard捕获了用户档案信息和偏好设置，它就可以根据用户的兴趣发送个性化消息。

构建这些规则时使用了以下元素：

1. 带有Campaign API侦听器的注册表单。

   ![替换文本](assets/apis_uc1.png)

1. 要根据复选框执行的自定义操作。 与普通注册流程相比，选择“电子邮件特别优惠”的客户将收到一封包含礼品券的自定义邮件。

   ![替换文本](assets/apis_uc2.png)

1. 用户档案在单击电子邮件中的“Update Details”链接后可能会更改其详细信息。 这将配置文件转到“更新您的配置文件和偏好设置详细信息”页面。 为了执行该操作，会将配置文件详细信息(Pkey)传递到Campaign服务器，并检索和表示配置文件。 一旦用户档案单击“更新”按钮，信息就会更新到系统中(通过PATCH命令)。

   ![替换文本](assets/apis_uc3.png)

提供了一组请求，以帮助您熟悉Campaign StandardAPI请求。 此收藏集采用JSON格式，提供了代表常见用例的预设计API请求。

以下步骤描述了分步使用案例，用于导入和使用收藏集在Campaign Standard数据库中创建用户档案。

>[!NOTE]
>
>我们的示例使用Postman。 但是，请随意使用您最喜爱的REST客户端。

1. 单击[此处](https://helpx.adobe.com/content/dam/help/en/campaign/kb/working-with-acs-api/_jcr_content/main-pars/download_section/download-1/KB_postman_collection.json.zip)下载JSON收藏集。

1. 打开Postman，然后选择&#x200B;**文件** / **导入**&#x200B;菜单。

1. 将下载的文件拖放到窗口中。 预先设计的API请求显示，可供使用。

   ![替换文本](assets/postman_collection.png)

1. 选择&#x200B;**创建配置文件**&#x200B;请求，然后使用您自己的信息(&lt;ORGANIZATION>、&lt;API_KEY>、&lt;ACCESS_TOKEN>)更新POST请求和&#x200B;**标头**&#x200B;选项卡。 有关详细信息，请参阅[此部分](setting-up-api-access.md)。

   ![替换文本](assets/postman_uc1.png)

1. 在&#x200B;**正文**&#x200B;选项卡中填写要添加到新配置文件中的信息，然后单击&#x200B;**发送**&#x200B;按钮以执行请求。

   ![替换文本](assets/postman_uc2.png)

1. 创建对象后，主键(PKey)将与其关联。 它可以在请求响应中以及其他属性中可见。

   ![替换文本](assets/postman_uc3.png)

1. 打开您的Campaign Standard实例，然后检查是否创建了配置文件，其中包含有效负载中的所有信息。

   ![替换文本](assets/postman_uc4.png)
