---
title: 具有客户端IP上下文变量的受众规则
description: 了解如何在Adobe Experience转出的受众规则中使用客户端IP上下文变量，包括支持IP地址、CIDR块和网络范围。
source-git-commit: 3f3f7145b3c58dc721cbeb850e9e8571e3255bb1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---


# 具有客户端IP上下文变量的受众规则 {#clientip-rule}

`clientip`上下文变量允许您根据用户的客户端IP地址定位用户。 这对于根据用户访问您的应用程序的所在网络来限制或启用功能非常有用，例如，限制对公司网络上的用户的早期访问。

## 支持的输入类型 {#input-types}

`clientip`上下文变量支持三种类型的输入值：

| 输入类型 | 描述 | 支持的运算符 |
|---|---|---|
| **IP地址** | 单个IPv4或IPv6地址 | 是，不等于，在 |
| **CIDR块** | CIDR表示法的IP地址范围（例如，`192.168.1.0/24`） | 等于，在中，不等于 |
| **网络范围** | 由平台维护的预定义命名网络范围 | 属于 |

## 添加客户端IP规则 {#adding-rule}

1. 在控制台中打开功能标记、功能组或跨团队功能组。
2. 转到&#x200B;**受众**&#x200B;选项卡。
3. 在&#x200B;**上下文**&#x200B;下，使用&#x200B;**clientip**&#x200B;变量添加条件。
4. 选择运算符并输入值（IP地址、CIDR块或选择预定义的网络范围）。

## 另请参阅 {#see-also}

* [在受众规则中使用上下文](using-context-in-audience-rules.md)
* [功能标志和功能组中的受众](audience-in-feature-flags-and-feature-groups.md)
* [复杂的受众规则](complex-rules.md)
