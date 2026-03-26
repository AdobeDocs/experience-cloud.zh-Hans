---
title: 在受众规则中使用企业组织数据
description: 了解如何在Adobe Experience推广中使用企业组织ID作为受众标准来定位特定的客户组织。
exl-id: 74f97ec7-a809-41bf-a41d-bb57f033040f
source-git-commit: 4a3133f014a9bb9d6ed26eb9d9f763db79ce63b3
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# 在受众规则中使用企业组织数据 {#enterprise-org-data}

体验转出支持根据用户的企业组织(org) ID来定位用户。 这允许您在将功能广泛提供之前将其部署到特定客户组织。

## 在受众规则中添加组织 {#adding-org-rule}

企业组织定位在&#x200B;**受众规则>配置文件>企业**&#x200B;下的&#x200B;**受众**&#x200B;选项卡中可用。

支持两种组织类型：

### DME组织 {#dme-orgs}

DME组织由其组织ID标识。 创建规则时，请仅输入组织ID — 不包括身份验证源。

### DMA组织 {#dma-orgs}

DMA组织使用`XXXXXXXXXXXXXXXXXXXXXXXX@ADOBEORG`格式的组织ID。 输入DMA组织ID时：

* 使用包含`@ADOBEORG`后缀的完整组织ID。
* 全大写输入`ADOBEORG`。

**示例：** `57F22B5D5A5F83AE0A495E6E@ADOBEORG`

## 重要说明 {#important-notes}

* 将针对与用户的已验证会话关联的组织评估基于组织的定位。 测试时，确保用户登录到正确的组织。
* 如果受众标准中未显示您预期找到的组织，或者特定组织的功能未按预期返回，请联系体验转出支持。
* 暂存环境和生产环境可能因可用的组织而异。 在升级到生产环境之前，请在暂存环境中测试受众规则。

## 另请参阅 {#see-also}

* [功能标志和功能组中的受众](audience-in-feature-flags-and-feature-groups.md)
* [复杂的受众规则](complex-rules.md)
