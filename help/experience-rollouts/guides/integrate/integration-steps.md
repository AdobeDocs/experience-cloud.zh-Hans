---
title: 集成步骤
description: 按照与您的应用程序类型相关的集成步骤，将Adobe Experience转出连接到您的Web服务、Web或移动应用程序或桌面应用程序。
source-git-commit: b82520eebe0070b5f76e0f7daeb2bb79a4bccca0
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 3%

---


# 集成步骤 {#integration-steps}

选择与您的应用程序类型匹配的集成路径。

## Web 服务 {#web-services}

后端服务使用服务器端SDK进行集成。 为您的技术栈栈选择SDK 。

**Java**

有关设置、依赖项配置和初始化，请按照[Java SDK集成指南](../sdk-releases/java/java-sdk-integration-guide.md)操作。

**Node.js**

请按照[Node.js SDK集成指南](../sdk-releases/nodejs/nodejs-sdk-integration-guide.md)中的说明进行设置和初始化。

**其他语言**

如果您的栈栈未在上面列出，请直接与&#x200B;**功能API V3**&#x200B;集成（请参阅本指南的功能API部分）。 如果您需要指导，请联系体验转出支持。

## Web和移动应用程序 {#web-mobile}

Web和移动应用程序调用&#x200B;**功能API V3**&#x200B;以检索当前用户的功能标记并在应用程序中应用条件逻辑。

有关完整API参考，请参阅本指南的功能API部分中的&#x200B;**GET功能API V3**。

## 桌面应用程序 {#desktop}

桌面应用程序调用&#x200B;**功能API V2**&#x200B;以检索功能标志。

有关完整API参考，请参阅本指南的功能API部分中的&#x200B;**GET功能API V2**。

>[!IMPORTANT]
>
>桌面客户端必须遵守API响应中的TTL值，并针对API不可用实施正常错误处理。 有关要求，请参阅[桌面应用程序](desktop-applications.md)。

## 另请参阅 {#see-also}

* [启动指南](startup-guide.md)
* [SDK](sdks.md)
* [Web 服务](web-services.md)
* [桌面应用程序](desktop-applications.md)
