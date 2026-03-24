---
title: 设置功能组以逐步推出
description: 了解如何在Adobe体验转出中为功能组配置基于百分比的逐步转出。
source-git-commit: 9bfe0e55e89c1d7fbd77cde63831a6a186820e24
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 3%

---


# 设置功能组以逐步推出 {#gradual-rollout-feature-group}

已在&#x200B;**基本详细信息**&#x200B;选项卡中配置功能组的百分比转出。 您可以随时在转出过程中向上或向下调整此值。

## 工作原理 {#how-it-works}

当您设置百分比转出（例如，60%）时，定义受众的该百分比对功能组可见。 剩余40%被放置在&#x200B;**控制组**&#x200B;中，该控制组接收默认行为。

如果已配置多个变体（用于A/B测试），则暴露百分比平均分配给各个变体。 例如，三种变体的60%暴露会导致每种变体的20%，对照组为40%。

您可以随时增加或减少百分比以展开、减少或暂停转出。

## 另请参阅 {#see-also}

* [创建功能组](create-a-feature-group.md)
* [使用功能标记进行A/B测试](a-b-testing.md)
* [逐步转出](../../concepts/gradual-rollout.md)
