---
title: 品牌化
description: 了解可用于管理品牌策略的所有工具
audience: administration
context-tags: branding,overview;branding,main
role: Admin
level: Experienced
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
source-git-commit: 51abadc86b97097d13824651d8c50d4ddd014a51
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 18%

---

# 品牌策略入门 {#branding-gs}

>[!IMPORTANT]
>
>最终用户不能创建或修改品牌：必须由 Adobe Campaign 技术管理员执行这些操作。如有任何需求，请与 Adobe 客户关怀部门联系。

每家公司都有定义视觉元素和技术细节的品牌准则。 Adobe Campaign可帮助您集中管理这些准则，以使您可在所执行的所有操作（从电子邮件中的徽标到营销活动中使用的URL和域）中为客户提供一致的品牌形象。

技术管理员可以在Adobe Campaign中创建和管理多个品牌。 这允许您定义构成品牌标识的所有元素，包括徽标甚至电子邮件跟踪设置。 创建后，这些品牌可以轻松链接到您的投放。

您可以在Campaign中添加组织的新实体，或创建必须在其他子域下发送的新类型电子邮件。 为此，请执行以下步骤：

1. **配置新子域**  — 对于Adobe要使用的任何新子域，第一步是对其进行配置。 您可以通过以下方式执行此操作 [营销活动控制面板](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/subdomains-branding.html?lang=zh-Hans) 或联系您的Adobe技术联系人。 了解有关子域配置的更多信息 [本页内容](https://experienceleague.adobe.com/en/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/campaign/ac-domain-name-setup).

   >[!NOTE]
   >
   >所有管理员用户都可访问控制面板。[此页面](https://experienceleague.adobe.com/docs/control-panel/using/discover-control-panel/managing-permissions.html?lang=zh-Hans#discover-control-panel)详细介绍了授予用户管理员访问权限的步骤。

1. **创建投放模板**  — 新品牌可用后，最佳做法是创建至少一个引用此新品牌的新空白投放模板。 [了解详情](branding-assign.md)。

1. **查看可投放性准则**  — 在开始使用新域之前，应与Adobe可交付性团队讨论该策略。 例如，如果应该创建新的关联以便在域之间拆分IP，和/或是否应定义提升计划，则这些规则将有助于定义最佳实践。

