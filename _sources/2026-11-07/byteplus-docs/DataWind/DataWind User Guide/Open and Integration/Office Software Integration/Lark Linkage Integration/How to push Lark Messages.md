---
title: "How to push Lark Messages"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/How_to_push_Lark_Messages"
---

<span id="_1-概述"></span>
# Overview

After the administrator completes the basic Lark integration (connecting the Lark application) and the basic configuration (including permission settings), subscriptions and alert rules can be set in Intelligent Data Insights to enable charts, dashboards, and data anomalies to be pushed to Lark and Lark groups.

<span id="_2-前置操作"></span>
# Prerequisite operations


1. Complete all basic configurations for connecting the Lark application.

2. Complete all configuration operations for account binding when connecting the Lark application;

3. Complete the corresponding Lark permission configuration:

   On the permission management page of the Lark Open Platform, ensure the following permissions are enabled. "View, comment, edit, and manage multi\-dimensional tables" and "View, comment, and export multi\-dimensional tables" are permissions for multi\-dimensional tables. "View, comment, edit, and manage spreadsheets" and "View, comment, and export spreadsheets" are permissions for spreadsheets. It is recommended to select all permissions related to cloud documents. The permission configuration interface of the Lark Open Platform may be updated periodically. Please note that you should refer to the latest permission configuration interface, and it is also recommended to select all permissions related to cloud documents.


For more specific operations, see [Basic Configuration for Lark Integration](https://docs.byteplus.com/docs/DataWind/Basic_Configuration_for_Lark_Integration) and [Data Subscription](https://docs.byteplus.com/docs/DataWind/Data_Subscription), and more.

<span id="_3-推送配置"></span>
# Push configuration

<span id="_3-1-应用权限配置"></span>
## Application permission configuration

<span id="_3-1-1-应用可见范围设置“全部成员”"></span>
### Set application visibility to "All members"

Contact the **Lark enterprise organization administrator** in the [Lark management console](http://feishu.cn/admin/index) to confirm that the application's address book visibility is set to all members. Entry: Workbench \-\> Application list \-\> Find the application \-\> Application availability scope

<span id="_3-1-2-配置发送消息的权限"></span>
### Configure permission to send messages

**Lark application administrator goes to** [Lark Open Platform](https://open.feishu.cn/) to add, configure, and authorize permission to send messages, and asks the **enterprise organization administrator** to approve the permission.


1. **Obtain and send direct and group messages:**  After enabling this permission, the bot can send direct messages to users or send group messages to groups where the bot is present. By adding the "Receive messages" event (go to the "Event Subscription" panel \> Add Event \> Messages and Groups), the bot can then receive direct messages sent by users.

2. **Obtain messages where the bot is mentioned in a group:**  After enabling this permission and adding the "Receive messages" event (go to the "Event Subscription" panel \> Add Event \> Messages and Groups), the bot can receive messages in which users mention it in a group chat.


<span id="_3-1-3-添加机器人"></span>
### Add a bot

**Lark application administrators should go to** [Lark Open Platform](https://open.feishu.cn/app) and, under "Add Application Capabilities," click to add "Bot." The "Bot" option will then appear in the left sidebar. Next, enter the configuration interface for "Bot," where custom menus and other settings can be configured.

<span id="_3-2-如何发送到个人"></span>
## How to send to an individual


* After completing the binding configuration, go to the dashboard and click "Create Subscription."

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c377489228a34657b5077eb280dc9cd3~tplv-goo7wpa0wc-image.image) </span>

* Select the test account as shown below and click "Send Test."

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51d87c1c64d34ae39090c3dac05f3c46~tplv-goo7wpa0wc-image.image) </span>

* You will then receive the push test message in your personal Lark account. If it is not successful, please check whether the above configuration is correct.


<span id="_3-3-如何发送到飞书群"></span>
## How to send to a Lark group

**To properly receive messages, the Lark group must add the bot corresponding to the application information you configured in Enterprise Management/Enterprise Domain Management \- Office Platform Integration.** 

Steps to add a bot to a Lark group:


1. Open Lark, enter the group chat to be subscribed to, and go to Conversation Settings \> Group Bots \> Add Bot.

2. Click Add Bot, search for the name of the bot you use to push messages, find and click the bot, and it will be added successfully.

3. After completing the addition, perform the verification test steps for sending to an individual, but change the message recipient to the Lark group and select the created test group.


Note: You need to set a recent time here to test message push. If you choose to send a test, only the sender will receive the push message, which is the same as pushing to an individual.


4. After pushing a group message at the specified time, you will receive a subscription creation notification, and at the specified time, you will receive a subscription message. This indicates that the configuration is successful. If it is not successful, please check whether the configuration is correct according to the instructions above.
