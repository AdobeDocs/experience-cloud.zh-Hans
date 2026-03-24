---
audience: user
user-guide-title: Adobe体验转出
user-guide-description: 了解如何使用Adobe Experience转出管理应用程序中的功能标记、控制转出和定向发布。
source-git-commit: db719ba7b9db91aea818d8ef216a28fcedc6aa65
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 5%

---


# Adobe体验转出 {#experience-rollouts}

+ [概述](home.md)
+ 开始使用 {#get-started}
   + [体验转出简介](getting-started/introduction.md)
   + [为何使用体验转出](getting-started/why-use-experience-rollouts.md)
   + [体验转出模式](getting-started/experience-rollouts-modes.md)
+ 概念 {#concepts}
   + [什么是功能标记](concepts/what-is-a-feature-flag.md)
   + [用于启用和禁用功能的功能标记](concepts/feature-flags-to-enable-disable-features.md)
   + [用于控制多个特征的特征组](concepts/feature-groups-to-control-multiple-features.md)
   + [发布管理的概念](concepts/concept-of-release-management.md)
   + [体验转出中的版本管理](concepts/release-management.md)
   + [逐步转出](concepts/gradual-rollout.md)
+ 指南 {#guides}
   + 控制台入门 {#console}
      + [登录到“体验转出”控制台](guides/console/log-in-to-the-console.md)
      + [环境概述](guides/console/environments-overview.md)
      + [请求访问](guides/console/request-access.md)
      + [团队及其管理员](guides/console/teams-and-admins.md)
      + [创建新团队](guides/console/create-a-new-team.md)
   + 团队 {#teams}
      + [管理团队](guides/teams/manage-teams.md)
      + [用户角色](guides/teams/user-roles.md)
      + [将成员添加到团队](guides/teams/add-team-members.md)
      + [团队管理常见问题解答](guides/teams/team-management-faq.md)
   + 应用程序 {#applications}
      + [管理应用程序](guides/applications/manage-applications.md)
      + [载入您的应用程序](guides/applications/onboard-your-application.md)
   + 集成体验转出 {#integrate}
      + [在应用程序中集成体验转出](guides/integrate/integrating-in-your-app.md)
      + [启动指南](guides/integrate/startup-guide.md)
      + [桌面应用程序](guides/integrate/desktop-applications.md)
      + [移动设备应用程序](guides/integrate/mobile-applications.md)
      + [Web 应用程序](guides/integrate/web-applications.md)
      + [Web 服务](guides/integrate/web-services.md)
      + [SDK](guides/integrate/sdks.md)
      + [集成步骤](guides/integrate/integration-steps.md)
      + [订阅Adobe Developer Console中的API应用程序](guides/integrate/subscribe-to-api-application.md)
   + 功能标记和版本 {#feature-flags-releases}
      + [功能、功能组和版本](guides/feature-flags/features-feature-groups-releases.md)
      + [创建您的第一个功能标记](guides/feature-flags/create-your-first-feature-flag.md)
      + [设置功能以逐步推出](guides/feature-flags/set-feature-gradual-rollout.md)
      + [创建功能组](guides/feature-flags/create-a-feature-group.md)
      + [设置功能组以逐步推出](guides/feature-flags/set-feature-group-gradual-rollout.md)
      + [使用功能标记进行A/B测试](guides/feature-flags/a-b-testing.md)
      + [版本和跨团队功能组](guides/feature-flags/releases-and-cross-team-feature-groups.md)
      + [端到端发布工作流](guides/feature-flags/release-workflow-end-to-end.md)
      + [请求发布](guides/feature-flags/request-a-release.md)
      + [更新版本受众规则](guides/feature-flags/update-release-audience-rules.md)
      + [发行状态](guides/feature-flags/release-states.md)
      + [创建跨团队功能组](guides/feature-flags/create-cross-team-feature-group.md)
      + [版本管理常见问题解答](guides/feature-flags/release-management-faqs.md)
      + [Analytics](guides/feature-flags/analytics.md)
      + [计划](guides/feature-flags/schedule.md)
   + 受众条件 {#audience}
      + [功能标志和功能组中的受众](guides/audience/audience-in-feature-flags-and-feature-groups.md)
      + [在受众规则中使用上下文](guides/audience/using-context-in-audience-rules.md)
      + [复杂的受众规则](guides/audience/complex-rules.md)
      + [在受众规则中使用企业组织数据](guides/audience/using-enterprise-org-data.md)
      + [在受众条件中添加百分比规则](guides/audience/adding-percentage-rules.md)
      + [具有客户端IP上下文变量的受众规则](guides/audience/clientip-rule.md)
   + 跨环境工作流 {#cross-environment}
      + [跨环境概念](guides/cross-environment/cross-environment-concept.md)
      + [将环境与应用程序关联](guides/cross-environment/associate-environments.md)
      + [跨环境查看功能标记](guides/cross-environment/view-feature-flags-across-environments.md)
      + [导入功能标志](guides/cross-environment/import-feature-flags.md)
   + 支持 {#support}
      + [故障排除](guides/support/troubleshooting.md)
      + [获取支持](guides/support/get-support.md)
      + [联系支持人员](guides/support/contact-support.md)
   + SDK版本 {#sdk-releases}
      + Java SDK {#java-sdk}
         + [Java SDK集成指南](guides/sdk-releases/java/java-sdk-integration-guide.md)
         + [Java SDK发行说明](guides/sdk-releases/java/java-sdk-release-notes.md)
      + Node.js SDK {#nodejs-sdk}
         + [Node.js SDK集成指南](guides/sdk-releases/nodejs/nodejs-sdk-integration-guide.md)
         + [Node.js SDK发行说明](guides/sdk-releases/nodejs/nodejs-sdk-release-notes.md)
      + [SDK基准测试](guides/sdk-releases/java-sdk-benchmarking.md)
+ 功能API {#feature-api}
   + [GET功能API V3](feature-api/get-feature-api-v3.md)
   + [GET功能API V2](feature-api/get-feature-api-v2.md)
+ 管理API {#management-api}
   + [功能管理API概述](management-api/feature-management-apis-overview.md)
   + [功能标记管理API](management-api/feature-flags-management-api.md)
   + [功能组管理API](management-api/feature-group-management-api.md)
   + [发布管理API](management-api/release-management-apis.md)
   + [获取应用程序的客户端ID](management-api/get-client-id.md)
   + [获取所需的受众条件](management-api/get-audience-criteria.md)
   + [管理修补程序API](management-api/management-patch-api.md)
