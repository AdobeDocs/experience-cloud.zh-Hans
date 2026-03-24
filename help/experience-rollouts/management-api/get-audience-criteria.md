---
title: 获取所需的受众条件
description: 了解如何使用控制台和GET功能API生成在Experience Rollout管理API中使用的正确受众标准JSON结构。
source-git-commit: 6ecedbfc6c7de392f214f3f8f2e71aa18e1bacb9
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 1%

---


# 获取所需的受众条件 {#get-audience-criteria}

管理API中的受众标准字段使用结构化JSON格式，这种格式手工编写可能会比较复杂。 推荐的方法是使用控制台构建所需的受众，然后通过API检索其JSON表示形式。

## 步骤 {#steps}

要获取所需受众标准的JSON，请执行以下步骤：

1. 在“体验转出”控制台中，根据要在API调用中使用的受众条件创建一个临时功能标记。
2. 保存后，请注意浏览器URL中的功能标志ID。 ID显示在URL中的客户端ID之后。 例如，在`.../feature-flags/1191/22080`中，功能ID为`22080`。
3. 使用该功能ID调用[按ID获取功能](feature-flags-management-api.md#get-feature-by-id)终结点。
4. 在响应JSON中，找到`audience`字段。 这包含所需的确切受众标准结构。
5. 复制`audience`值，从每个规则对象中删除`id`属性。 在创建或更新功能API调用中使用此项。

## 示例 {#example}

调用GET `/m/api/v1/mgmt/feature/22080`后，响应包括：

```json
{
  "audience": [
    {
      "id": 10034665,
      "criteria": {
        "and": [
          {
            "operator": "EQ",
            "attr": "LOCALE",
            "val": "EN",
            "ruleId": 1,
            "category": "default"
          }
        ]
      }
    }
  ]
}
```

要在“创建”功能调用中使用它，请从受众对象中删除`id`字段：

```json
{
  "audience": [
    {
      "criteria": {
        "and": [
          {
            "operator": "EQ",
            "attr": "LOCALE",
            "val": "EN",
            "ruleId": 1,
            "category": "default"
          }
        ]
      }
    }
  ]
}
```

## 另请参阅 {#see-also}

* [功能标记管理API](feature-flags-management-api.md)
* [获取应用程序的客户端ID](get-client-id.md)
* [管理修补程序API](management-patch-api.md)
