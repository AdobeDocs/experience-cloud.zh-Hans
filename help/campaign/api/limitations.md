---
title: Recommendations和限制
description: 迁移到Campaign v8 REST API时Recommendations和限制。
audience: developing
content-type: reference
topic-tags: campaign-standard-apis
role: Data Engineer
level: Experienced
mini-toc-levels: 1
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
exl-id: 45acebb1-9325-4e26-8fe9-cc73f745d801
source-git-commit: 34c6f8a137a9085b26c0ea8f78930cff6192cfc9
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 1%

---

# Recommendations和限制 {#limitations}

## 权限和安全性 {#permissions}

### 产品配置文件映射

在Campaign Standard中，无论您分配了什么产品配置文件，都向您授予了更高的API管理员角色访问权限。 Campaign v8引入了一组不同的产品配置文件，需要从Campaign Standard映射到Campaign v8产品配置文件。

通过迁移，可将两个产品配置文件添加到您现有或预先创建的技术帐户：管理员和消息中心（用于访问事务型API）。 如果您不希望将管理员产品配置文件映射到您的技术帐户，请查看产品配置文件映射，并分配所需的产品配置文件。

### 租户ID

迁移后，对于任何未来的集成，建议在REST URL中使用您的&#x200B;**Campaign v8租户ID**，替换您以前的Campaign Standard租户ID。

### 密钥用法

PKey值的管理在Campaign Standard和Campaign v8之间有所不同。 如果您使用Campaign Standard存储PKeys，请确保您的实施使用从以前的API调用中获取的PKeys或href动态形成后续API调用。

## 可用API {#deprecated}

目前，下面列出的REST API可供使用：

* **用户档案**
* **服务和订阅**
* **自定义资源**
* **工作流**

>[!AVAILABILITY]
>
>目前，**事务性消息** REST API不可用。
>
>下面列出的REST API已弃用，无法使用：
>* 营销历史记录
>* 组织实体
>* 隐私管理

## 筛选

* 要在REST API负载中使用筛选器，您需要在Campaign v8中编辑这些筛选器，并提供要在负载中使用的名称。 为此，请从&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡访问筛选器的其他参数，并在REST API的&#x200B;**[!UICONTROL 筛选器名称]**&#x200B;字段中提供所需的名称。

  ![](assets/api-filtering.png)


* 不再需要使用自定义筛选器所需的“by”前缀。 过滤器名称应按照原样在请求中使用。

  示例：

  `GET https://mc.adobe.io/<ORGANIZATION>/campaign/profileAndServicesExt/<resourceName>/<customFilterName>?<customFilterparam>=<customFilterValue>`

## 删除的数据库字段

迁移期间将删除数据库中的某些字段。 使用放置的字段时，REST API将返回空白值。 将来，弃用和删除所有已删除的字段。

## 包含链接资源的POST

使用以下请求正文格式时，“vehicleOwner”表示指向“nms：recipient”的链接：

```
{
    "vehicleNumber": "20009",
    "vehicleName": "Model E",
    "vehicleOwner":{
        "firstName":"tester 11",
        "lastName":"Smith 11"
    }
}
```

链接信息将被忽略。 因此，在“cusVehicle”下生成了一个仅包含“vehicleNumber”和“vehicleName”值的新记录。 但是，链接仍然为空，导致“vehicleOwner”被设置为null。

在Campaign v8中，当使用相同的请求正文结构并且“vehicle”链接到用户档案时，会发生错误。 出现此错误是因为“firstName”属性未被识别为“cusVehicle”有效。 但是，请求正文仅包含属性而没有链接功能，没有任何问题。

## PATCH操作

* Campaign v8不支持请求正文为空的PATCH：它返回204无内容状态。
* 虽然Campaign Standard支持对架构中的元素/属性进行PATCH，但请注意，Campaign v8不支持对位置进行PATCH操作。 尝试对位置进行PATCH将导致500内部服务器错误，并显示一条错误消息，指示“zipCode”属性对于“profile”资源无效。

## REST响应

以下部分列出了Campaign Standard与v8 REST响应之间的细微差异。

* 对于单个GET记录，响应中包含href。
* 在使用属性进行查询时，Campaign v8在响应中提供计数和分页。
* POST操作后，响应中将返回来自链接资源的值。

## 错误代码和消息

以下部分列出了Campaign Standard与Campaign v8错误代码和消息之间的差异。

| 方案 | Campaign Standard | Campaign v8 |
|  ---  |  ---  |  ---  |
| 在请求正文中使用无效的PKey | 500 — “O5iRp40EGA”属性未知(请参阅“Profiles (nms：recipient)”架构的定义)。 XTK-170036无法解析表达式“@id = @O5iRp40EGA”。 | 404 — 无法解密PKey。 (PKey=@jksad) |
| 在URI中使用无效的PKey | 500 — “O5iRp40EGA”属性未知(请参阅“Profiles (nms：recipient)”架构的定义)。 XTK-170036无法解析表达式“@id = @O5iRp40EGA”。 | 404 — 无法解密PKey。 (PKey=@jksad)不支持的端点。 (endpoint=rest/profileAndServices/profile/@jksad) |
| 在URI和请求正文中使用两个不同的原始Pkey | 500 - RST-360011发生错误 — 请联系您的管理员。 RST-360012对资源“服务”的操作不一致 — 无法将键“SVC3”更新为“SVC4”。 | 500 — 发生错误 — 请联系您的管理员。 |
| 在URI中使用PKey，并在请求正文中使用其他原始PKey | 500 — 具有相同键“SVC4”的“服务”已存在。 PGS-220000 PostgreSQL错误：错误：重复的键值将违反唯一约束“nmsservice_name”。详细信息：键(sname)=(SVC4)已存在。 | 500 — 发生错误 — 请联系您的管理员。 |
| 在URI中使用不存在的原始ID | 404 - RST-360011发生错误 — 请联系您的管理员。 无法从键“adobe_nl：0”（模式为“service”且名称为“adobe_nl”的文档）找到路径为“Service”的文档 | 404 — 无法从键“adobe_nl”（模式为“service”且名称为“adobe_nl”的文档）找到路径为“Service”的文档 |
| 在请求正文中使用不存在的原始ID | 404 - RST-360011发生错误 — 请联系您的管理员。 无法从键“adobe_nl”中找到路径为“Service”的文档（架构为“service”且名称为“adobe_nl”的文档） | 404 — 无法从键“adobe_nl”（模式为“service”且名称为“adobe_nl”的文档）找到路径为“Service”的文档 |
| - | 500 - RST-360011发生错误 — 请联系您的管理员。 | 500 — 发生错误 — 请联系您的管理员。 |
| 插入具有无效性别（或任何）枚举值的配置文件/服务 | 500 - RST-360011发生错误 — 请联系您的管理员。 值“invalid”对于“@gender”字段的“nms:recipient:gender”枚举无效 | 500 — 发生错误 — 请联系您的管理员。 |

## 个人资料 — 时区

对于Campaign Standard，时区显示为&#x200B;**profileAndServices/profile** REST API调用的JSON响应的一部分。

使用Campaign v8时，时区仅作为&#x200B;**profileAndServicesExt/profile** REST API调用的一部分显示给用户。 它不是&#x200B;**profileAndServices/profile** REST API调用的一部分，因为它被添加到扩展架构中。

## 工作流 — 外部信号触发

Campaign Standard工作流GETAPI返回参数名称，例如工作流实例变量及其数据类型（布尔值、字符串等）。 当通过POSTAPI调用触发信号时，可用于创建格式适当的JSON请求正文。

Campaign v8不支持广告工作流实例变量，但希望开发人员了解这些变量。 因此，在迁移后，需要构建POST请求正文中的参数信息，而没有GETAPI响应中的参数信息。

## 事务性消息

* 使用Campaign Standard时，POST请求将为请求正文中的元素和属性返回空字段。 使用Campaign v8时，响应会返回与请求正文中的值匹配的值。

* 发布事件配置时，API预览面板在请求正文语法旁边显示REST URL。

  由于Campaign v8不支持事件配置字段定义（事件创建只是向eventType枚举添加值），因此在添加事件类型时没有API预览面板。 发布事件事务型消息后，事务型消息用户界面中会显示REST URL。
