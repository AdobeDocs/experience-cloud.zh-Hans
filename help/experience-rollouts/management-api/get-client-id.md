---
title: 获取应用程序的客户端ID
description: 了解如何在Experience Rollout控制台中找到应用程序的数字客户端ID，这是调用管理API时必需的。
source-git-commit: 6ecedbfc6c7de392f214f3f8f2e71aa18e1bacb9
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 1%

---


# 获取应用程序的客户端ID {#get-client-id}

功能标志和功能组管理API需要数字`clientId`来标识该功能所属的应用程序。 这与用于API身份验证的基于字符串的IMS客户端ID不同。

按照以下步骤查找应用程序的数字客户端ID。

## 步骤 {#steps}

要查找应用程序的数字客户端ID，请执行以下步骤：

1. 登录到“体验转出”控制台。
2. 导航到&#x200B;**功能和版本**。
3. 选择&#x200B;**功能标志**&#x200B;选项卡。
4. 打开&#x200B;**应用程序**&#x200B;下拉列表，然后选择需要其客户端ID的应用程序。
5. 查看浏览器地址栏中的URL。 在`feature-flags/`之后，显示的数字是该应用程序的数字客户端ID。

例如，如果URL以`.../feature-flags/1191/...`结尾，则客户端ID为`1191`。

## 在API调用中使用客户端ID {#use-in-api}

将此值作为管理API请求中的`clientId`参数传递。 例如，在创建功能标记时：

```json
{
  "name": "my-feature-flag",
  "clientId": 1191,
  "state": "disabled"
}
```

## 另请参阅 {#see-also}

* [功能标记管理API](feature-flags-management-api.md)
* [功能组管理API](feature-group-management-api.md)
* [获取所需的受众条件](get-audience-criteria.md)
