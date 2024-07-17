---
title: 组件列表
description: 在此处查找中可用的每个组件的列表     动态报告及其定义。
level: Beginner
audience: end-user
badge: label="有限可用性" type="Informative" url="../campaign-standard-migration-home.md" tooltip="仅限于Campaign Standard已迁移的用户"
exl-id: 5c58db92-7878-4c70-b076-a393f1cda8b7
source-git-commit: 34c6f8a137a9085b26c0ea8f78930cff6192cfc9
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---

# 组件列表 {#list-of-components}

请注意，如果两个组件不兼容，单元格将显示值&#x200B;**无**。

## 维度 {#dimensions}

下表列出了报表中使用的维度及其定义。

<table> 
 <thead> 
  <tr> 
   <th> Dimension<br/> </th> 
   <th> 定义<br/> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> 浏览器<br/> </td> 
   <td> 打开或单击邮件的浏览器。<br/> </td> 
  </tr> 
  <tr> 
   <td> Campaign<br/> </td> 
   <td> 营销活动的标签和ID。<br/> </td> 
  </tr> 
  <tr> 
   <td> 投放<br/> </td> 
   <td> 投放的标签和ID。<br/> </td> 
  </tr> 
  <tr> 
   <td> 设备<br/> </td> 
   <td> 从中打开/查看/单击电子邮件/短信/推送通知的设备。<br/> </td> 
  </tr> 
  <tr> 
   <td> 失败原因<br/> </td> 
   <td> 导致每次投放退回的错误类型，例如用户未知、无效域或邮箱已满。<br/> </td> 
  </tr> 
  <tr> 
   <td> 移动设备应用程序名称<br/> </td> 
   <td> 移动应用程序的名称<br/> </td> 
  </tr>
  <tr> 
   <td> 平台<br/> </td> 
   <td> 从中打开/查看/单击消息的设备的平台。<br/> </td> 
  </tr> 
  <tr> 
   <td> 配置文件<br/> </td> 
   <td> 重组在配置文件资源扩展期间创建的现成配置文件字段和自定义配置文件字段。<br/> </td> 
  </tr> 
  <tr> 
   <td> 收件人域<br/> </td> 
   <td> 用于打开电子邮件的域。<br/> </td> 
  </tr> 
  <tr> 
   <td> 循环投放<br/> </td> 
   <td> 定期投放的标签和ID。<br/> </td> 
  </tr> 
  <tr> 
   <td> 发件人域<br/> </td> 
   <td> 用于发送电子邮件的域。<br/> </td> 
  </tr> 
  <tr> 
   <td> 发件人IP<br/> </td> 
   <td> 用于发送电子邮件的IP。<br/> </td> 
  </tr> 
  <tr> 
   <td> 跟踪URL<br/> </td> 
   <td> 用户从消息中单击的URL。<br/> </td> 
  </tr> 
  <tr> 
   <td> 跟踪URL类别<br/> </td> 
   <td> 分配给跟踪URL的类别。<br/> </td> 
  </tr> 
  <tr> 
   <td> 跟踪URL标签<br/> </td> 
   <td> 为URL指定的标签，如镜像页面、联系我们或打开。<br/> </td> 
  </tr> 
  <tr> 
   <td> 事务性投放<br/> </td> 
   <td> 事务性投放的标签和ID。<br/> </td> 
  </tr> 
  <tr> 
   <td> 变体<br/> </td> 
   <td> A/B测试时电子邮件的变体。<br/> </td> 
  </tr> 
 </tbody> 
</table>

## 量度 {#metrics}

下表列出了报表中使用的量度及其定义，具体取决于投放类型。

### 电子邮件量度 {#email-and-sms-metrics}

<table> 
 <thead> 
  <tr> 
   <th> 量度<br/> </th> 
   <th> 定义<br/> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> 在阻止列表<br/>上 </td> 
   <td> 将电子邮件声明为垃圾邮件或垃圾邮件的收件人数量。<br/> </td> 
  </tr> 
  <tr> 
   <td> 阻止列表率<br/> </td> 
   <td> 在阻止列表上标记的传递百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 退回+错误<br/> </td> 
   <td> 传递和自动返回处理期间累计的错误总数与已发送消息的总数之比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 退回+错误率<br/> </td> 
   <td> 与已发送的电子邮件相比退回的电子邮件百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 单击<br/> </td> 
   <td> 在投放中点击内容的次数。<br/> </td> 
  </tr> 
  <tr> 
   <td> 点进率<br/> </td> 
   <td> 投放中的点击百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 已投放<br/> </td> 
   <td> 成功发送的邮件数，与已发送的邮件总数相关。<br/> </td> 
  </tr> 
  <tr> 
   <td> 传递率<br/> </td> 
   <td> 成功发送的邮件百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 硬退回<br/> </td> 
   <td> 永久错误的总数，如错误的电子邮件地址。<br/> </td> 
  </tr> 
  <tr> 
   <td> 硬退回率<br/> </td> 
   <td> 因永久错误而失败的传递百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 镜像页面<br/> </td> 
   <td> 点击镜像页面链接的收件人数量。<br/> </td> 
  </tr> 
  <tr> 
   <td> 镜像页面速率<br/> </td> 
   <td> 与总投放消息相比镜像页面链接的点击次数百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 优惠点击次数<br/> </td> 
   <td> 在投放中点击优惠的次数。<br/> </td> 
  </tr> 
  <tr> 
   <td> 优惠点击率<br/> </td> 
   <td> 对优惠的点击百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 打开<br/> </td> 
   <td> 在投放中打开邮件的次数。<br/> </td> 
  </tr> 
  <tr> 
   <td> 打开率<br/> </td> 
   <td> 已打开邮件的百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 已处理/已发送<br/> </td> 
   <td> 投放的发送总数。<br/> </td> 
  </tr> 
  <tr> 
   <td> 隔离<br/> </td> 
   <td> 退回并导致地址隔离的邮件数。<br/> </td> 
  </tr> 
  <tr> 
   <td> 隔离率<br/> </td> 
   <td> 与已发送消息相比的隔离百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 已拒绝<br/> </td> 
   <td> SMTP服务器分类为垃圾邮件的邮件数。<br/> </td> 
  </tr> 
  <tr> 
   <td> 拒绝率<br/> </td> 
   <td> 标记为拒绝的邮件的百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 软退回<br/> </td> 
   <td> 临时错误总数，如收件箱已满。<br/> </td> 
  </tr> 
  <tr> 
   <td> 软退回率<br/> </td> 
   <td> 因临时原因而失败的投放百分比。<br/> </td> 
  </tr> 
  <tr> 
   <td> 独特点击<br/> </td> 
   <td> 点击投放中内容的收件人数量。<br/> </td> 
  </tr> 
  <tr> 
   <td> 唯一打开次数<br/> </td> 
   <td> 打开投放的收件人数量。<br/> </td> 
  </tr> 
  <tr> 
   <td> 独特取消订阅<br/> </td> 
   <td> 点击取消订阅链接的收件人数量。<br/> </td> 
  </tr> 
  <tr> 
   <td> 取消订阅率<br/> </td> 
   <td> 与传递的邮件相比的唯一取消订阅数。<br/> </td> 
  </tr> 
  <tr> 
   <td> 已取消订阅<br/> </td> 
   <td> 取消订阅链接的点击次数。<br/> </td> 
  </tr> 
 </tbody> 
</table>

<!--
### Push notification metrics {#push-notification-metrics}

<table> 
 <thead> 
  <tr> 
   <th> Metric<br/> </th> 
   <th> Definition<br/> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> Bounces + Errors<br/> </td> 
   <td> Total of errors cumulated during delivery in relation to the total number of sent messages, e.g. errors from MCPNS or provider.<br/> </td> 
  </tr> 
  <tr> 
   <td> Bounce + Error rate<br/> </td> 
   <td> Percentage of push notifications that bounced compared to push notifications sent.<br/> </td> 
  </tr> 
  <tr> 
   <td> Click<br/> </td> 
   <td> Number of times a push notification has been delivered to the device and clicked on by the user. The user either wanted to view the notification, which will then be moved to Push Open tracking, or dismiss it.<br/> </td> 
  </tr> 
  <tr> 
   <td> Click through rate<br/> </td> 
   <td> Percentage of users who interacted with the push notification.<br/> </td> 
  </tr> 
  <tr> 
   <td> Delivered<br/> </td> 
   <td> Number of push notifications successfully sent, in relation to the total number of sent push notifications.<br/> </td> 
  </tr> 
  <tr> 
   <td> Delivered rate<br/> </td> 
   <td> Percentage of push notifications successfully sent.<br/> </td> 
  </tr> 
  <tr> 
   <td> Impressions<br/> </td> 
   <td> Number of times a push notification has been delivered to the device and left untouched in the notification center. In most cases, impressions number should be similar to the delivered number. This ensures that the device got the message and relayed that information back to the server.<br/> </td> 
  </tr> 
  <tr> 
   <td> Processed/sent<br/> </td> 
   <td> Total number of push notifications sent.<br/> </td> 
  </tr> 
  <tr> 
   <td> Open<br/> </td> 
   <td> Total number of push notifications delivered to the device and clicked on by users thus opening the app. This is similar to the Push Click except a Push Open will not be triggered if the notification was dismissed.<br/> </td> 
  </tr> 
  <tr> 
   <td> Open rate<br/> </td> 
   <td> Percentage of opened push notifications.<br/> </td> 
  </tr> 
  <tr> 
   <td> Unique clicks<br/> </td> 
   <td> Number of times a unique user interacts with the push notification, e.g. clicks on the notification or button.<br/> </td> 
  </tr> 
  <tr> 
   <td> Unique impressions<br/> </td> 
   <td> Number of impressions by recipient.<br/> </td> 
  </tr> 
  <tr> 
   <td> Unique Opens<br/> </td> 
   <td> Number of recipients who opened the delivery.<br/> </td> 
  </tr> 
 </tbody> 
</table>

### In-App metrics {#in-app-metrics}

<table> 
 <thead> 
  <tr> 
   <th> Metric<br/> </th> 
   <th> Definition<br/> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> Delivered<br/> </td> 
   <td> Total number of In-App messages delivered to the device by the service provider.<br/> </td> 
  </tr> 
  <tr> 
   <td> Impressions<br/> </td> 
   <td> Total of In-App messages seen by recipients depending on whether trigger criterion was met.<br/> </td> 
  </tr> 
  <tr> 
   <td> In-App clicks <br/> </td> 
   <td> Total number of recipients who clicked on Button 1 or Button 2.<br/> </td> 
  </tr> 
  <tr> 
   <td> In-App click through rate<br/> </td> 
   <td> Percentage of users who clicked on Button 1 or Button 2 compared to users who saw the message.<br/> </td> 
  </tr> 
  <tr> 
   <td> In-App dismissal<br/> </td> 
   <td> Total number of messages that recipients dismissed either by clicking the close button or auto-dismiss.<br/> </td> 
  </tr> 
  <tr> 
   <td> In-App dismissal rate<br/> </td> 
   <td> Percentage of In-App messages that recipients dismissed.<br/> </td> 
  </tr> 
  <tr> 
   <td> Processed/sent<br/> </td> 
   <td> Total number of In-App messages sent from Adobe Campaign as part of the delivery sent process.<br/> </td> 
  </tr> 
  <tr> 
   <td> Unique impressions<br/> </td> 
   <td> Number of impressions by a unique recipient.<br/> </td> 
  </tr> 
  <tr> 
   <td> Unique In-App clicks<br/> </td> 
   <td> Number of times recipients clicked on Button 1 or Button 2.<br/> </td> 
  </tr> 
  <tr> 
   <td> Unique In-App dismissals<br/> </td> 
   <td> Number of time recipients dismissed an In-App message.<br/> </td> 
  </tr> 
 </tbody> 
</table>
-->

## 区段 {#segments}

下表列出了报表中使用的区段及其定义。

<table> 
 <thead> 
  <tr> 
   <th> 区段<br/> </th> 
   <th> 定义<br/> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> 年龄：婴儿潮一代1<br/> </td> 
   <td> 1946年至1954年出生的收件人。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年龄：婴儿潮一代2<br/> </td> 
   <td> 1955年至1965年出生的收件人。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年龄：从18到25<br/> </td> 
   <td> 18到25岁的收件人。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年龄：从26到30<br/> </td> 
   <td> 26到30岁的收件人。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年龄：从31到40<br/> </td> 
   <td> 31到40岁的收件人。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年龄：从41到50<br/> </td> 
   <td> 41到50岁的收件人。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年龄：层代X<br/> </td> 
   <td> 1966年至1976年出生的收件人。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年龄：第Y代（千禧一代）<br/> </td> 
   <td> 1977年至1994年出生的收件人。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年龄：层代Z<br/> </td> 
   <td> 1995年至今天出生的收件人。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年龄：大于50<br/> </td> 
   <td> 年龄大于50岁的收件人。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年龄：小于25<br/> </td> 
   <td> 年龄小于25岁的收件人。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年龄：小于30<br/> </td> 
   <td> 年龄小于30岁的收件人。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年龄：小于40<br/> </td> 
   <td> 年龄小于40岁的收件人。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年龄：小于50<br/> </td> 
   <td> 年龄小于50岁的收件人。<br/> </td> 
  </tr> 
  <tr> 
   <td> 年龄：静默生成<br/> </td> 
   <td> 1945年或之前出生的收件人。<br/> </td> 
  </tr> 
  <tr> 
   <td> 所有访问<br/> </td> 
   <td> 每个收件人<br/> </td> 
  </tr>
 </tbody> 
</table>
