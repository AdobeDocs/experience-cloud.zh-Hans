---
title: 复杂的受众规则
description: 了解如何在Adobe体验转出中使用大型或复杂的受众规则集，包括批量值限制以及如何跨多个条件拆分规则。
source-git-commit: 3f3f7145b3c58dc721cbeb850e9e8571e3255bb1
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---


# 复杂的受众规则 {#complex-rules}

## 批量值限制 {#bulk-value-limits}

将大量值添加到单个受众规则（例如，电子邮件地址的较长列表）时，您可能会遇到错误，指示该规则已超出允许的最大大小。

每个受众规则具有每个属性的大小限制。 对于电子邮件地址，限制取决于条目的总字符长度，而不是固定计数。 作为一般准则，请为每个规则&#x200B;**使用大约** 100-115个电子邮件地址。

如果您需要定向的条目数超过此限制所允许的数量，请将列表拆分为较小的块，并使用嵌套逻辑将它们作为单独的OR连接条件应用。

## 对复杂规则使用嵌套逻辑 {#nested-logic}

通过嵌套逻辑，您可以将多个受众条件与精确的AND/OR控制结合使用。 要启用该功能，请执行以下操作：

1. 添加所需的受众条件。
2. 在受众规则部分中启用&#x200B;**嵌套逻辑**。
3. 每个条件都分配有一个编号。 输入引用这些数字的逻辑表达式，例如：
   * `1 and (2 or 3)`
   * `(1 and 2) or 3`
   * `(1 and 2) or (3 and 4)`

这是用于百分比规则与其他标准结合使用的相同机制。 有关已处理的示例，请参阅[在受众条件中添加百分比规则](adding-percentage-rules.md)。

## 另请参阅 {#see-also}

* [功能标志和功能组中的受众](audience-in-feature-flags-and-feature-groups.md)
* [在受众条件中添加百分比规则](adding-percentage-rules.md)
* [更新版本受众规则](../feature-flags/update-release-audience-rules.md)
