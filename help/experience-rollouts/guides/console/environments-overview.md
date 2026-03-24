---
title: 环境概述
description: 了解Adobe Experience转出中的暂存环境和生产环境以及何时使用它们。
source-git-commit: 9bfe0e55e89c1d7fbd77cde63831a6a186820e24
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 4%

---


# 环境概述 {#environments}

体验转出提供了单独的环境，以便您可以在将更改提升到实时用户之前验证功能标记。

## 可用环境 {#available-environments}

| 环境 | 用途 |
|---|---|
| **阶段** | 测试和验证。 在生产环境中启用功能标记之前，请使用此环境配置和测试功能标记。 |
| **生产** | 实时转出。 此处配置的功能标志将根据您的实际用户群进行评估。 |

>[!IMPORTANT]
>
>在阶段中所做的更改不会自动转移到生产环境。 功能标记和受众规则必须在每个环境中单独配置。

## 选择环境 {#selecting}

登录到“体验转出”控制台后，从界面顶部的环境切换器中选择环境。 在创建或修改功能标记之前，请确保您在正确的环境中工作。

## 最佳实践 {#best-practices}

请按照以下建议操作，以避免配置错误和保护生产受众：

* 始终首先在&#x200B;**阶段**&#x200B;中创建并测试功能标记。
* 在生产中复制之前，验证暂存中的受众规则、百分比转出和定位逻辑。
* 使用[跨环境工作流](../cross-environment/cross-environment-concept.md)查看和管理跨环境的标记状态。

## 另请参阅 {#see-also}

* [登录到控制台](log-in-to-the-console.md)
* [将环境与应用程序关联](../cross-environment/associate-environments.md)
* [跨环境查看功能标记](../cross-environment/view-feature-flags-across-environments.md)
