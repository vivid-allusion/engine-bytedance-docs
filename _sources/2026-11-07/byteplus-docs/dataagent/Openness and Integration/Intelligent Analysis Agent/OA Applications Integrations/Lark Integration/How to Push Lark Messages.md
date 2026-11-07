---
title: "How to Push Lark Messages"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/How_to_Push_Lark_Messages"
---

<span id="86f57514"></span>
# Overview

After the administrator completes the basic Lark integration (connecting the Lark application) and its basic configuration (including permission configuration), subscriptions and alert\-related rules can be set in Intelligent Data Insight, enabling charts, dashboards, and data anomalies to be pushed to Lark and Lark groups.

<span id="e174e279"></span>
# Prerequisite operations


* **Complete all basic configurations for connecting the Lark application.** 

* **Complete all configuration operations for account binding when connecting the Lark application.** 

* **Complete the corresponding Lark permission configuration:** 


On the permission management page of the Lark Open Platform, ensure the following permissions are enabled. "View, comment, edit, and manage multi\-dimensional tables" and "View, comment, and export multi\-dimensional tables" are permission settings for multi\-dimensional tables. "View, comment, edit, and manage spreadsheets" and "View, comment, and export spreadsheets" are permission settings for spreadsheets. It is recommended to select all permissions related to cloud documents. The permission configuration interface of the Lark Open Platform may be updated periodically. Please note that you should refer to the latest permission configuration interface, and it is also recommended to select all permissions related to cloud documents.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b7346b691ee046c7b2d5b2c945d8eafb~tplv-goo7wpa0wc-image.image) </span>

For more specific operations, see "[Connecting the Lark application](https://www.volcengine.com/docs/4726/67236)", "[Data subscription](https://www.volcengine.com/docs/4726/66646)", and so on.

<span id="59e0e05f"></span>
# Push configuration

<span id="e4772817"></span>
## Application permission configuration

<span id="52663014"></span>
### Set application visibility to "All members"

Contact the **Lark enterprise organization administrator** in the [Lark management console](http://feishu.cn/admin/index) to confirm that the application's address book visibility is set for all members. Entry: Workbench \-\> Application list \-\> Find the application \-\> Application availability scope

<span id="401f8a51"></span>
### Configure permission to send messages

The **Lark application administrator** needs to go to the [Lark Open Platform](https://open.feishu.cn/) to add and configure authorization to enable permission to send messages, and request the **enterprise organization administrator** to approve the permission.


1. **Obtaining and sending private and group messages** After enabling this permission, the bot can send private messages to users or group messages to groups where the bot is present. Once the “Receive messages” event is added (go to the “Event subscription” panel \> Add event \> Messages and groups), the bot can receive private messages sent by users.

2. **Obtaining messages where users @ the bot in groups** After enabling this permission and adding the “Receive messages” event (go to the “Event subscription” panel \> Add event \> Messages and groups), the bot can receive messages where users @ the bot in group chats.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a05201b5e1840809ca22d57bee409b1~tplv-goo7wpa0wc-image.image) </span>

<span id="826af237"></span>
### Adding a bot

**The Lark application administrator goes to** [Lark Open Platform](https://open.feishu.cn/app) In “Add application capabilities”, click to add “Bot”, and then “Bot” will appear in the left sidebar. Next, enter the bot configuration interface, where you can set custom menus and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6de1622d03684f6eb7060690bacdc944~tplv-goo7wpa0wc-image.image) </span>

<span id="a7747d05"></span>
## Sending to an individual


* After completing the binding configuration, go to the dashboard and click Create new subscription.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d36c60d2734743cb9fa332d05d337528~tplv-goo7wpa0wc-image.image) </span>


* Select the test account as shown below and click Send test.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1920bd8675964185938aedbcbfca6d5c~tplv-goo7wpa0wc-image.image) </span>


* You will receive the push test message in your personal Lark account. If it is not successful, please check whether the above configuration is correct.


<span id="fb40615c"></span>
## Sending to a Lark group

**To receive messages in the Lark group, add the bot associated with your application configuration in Enterprise Management/Enterprise Domain Management – Office Platform Integration.** 

Steps for adding a bot to a Lark group


1. Open Lark, enter the group chat you want to subscribe to, go to Conversation settings – Group bots – Add bot


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee171409571a44759d4d238b5f7fa7d5~tplv-goo7wpa0wc-image.image" width="403px" /></div>



2. Click Add bot, search for the bot name you use to push messages, find and click the bot, and it will be added successfully.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55c5694128904b69b1699def33c8cf73~tplv-goo7wpa0wc-image.image) </span>


3. After adding, follow the verification test steps for sending to an individual, change the message sending target to the Lark group, and select the created test group.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/365d9c2639f3444ab2587f0080d4900c~tplv-goo7wpa0wc-image.image) </span>

Note: You need to set a recent time here to test message push. If you choose to send a test, the push message will only be sent to the sender, which is the same as pushing to an individual.


4. After pushing a group message at the specified time, you will receive a subscription creation notification, and at the specified time, you will receive a subscription message. This indicates that the configuration is successful. If not, please check whether the configuration is correct according to the instructions above.


<span id="531ecb15"></span>
## 3.4 Multi\-subnet push

This feature supports displaying push links by subnet. You can set up the PC or mobile client for the required subnet. (Caution: This feature is an exclusive value\-added feature for private deployments.)

You can follow these steps:

**Step 1**: Click System Management in the upper right corner of the Intelligent Data Insight page.

**Step 2**: Click System Settings

**Step 3**: Click Network Zone Access Control

**Step 4**: After enabling multiple network zones, add a network zone.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c058731ce914866b1a539983e11fd25~tplv-goo7wpa0wc-image.image) </span>

**Step 5**: In the area shown below, select the corresponding method for Lark push for different subnets.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d347ea3a37e494eaea4e4e2c708b658~tplv-goo7wpa0wc-image.image) </span>
