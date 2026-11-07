---
title: "Webhook Subscription Push Method Configuration"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Webhook_Subscription_Push_Method_Configuration"
---

This article describes how to configure Webhook subscription push notifications through **WeCom group chats, DingTalk regular groups, Larkxternal groups, and system API** channels.

<span id="bd4bceed"></span>
# Feature overview

Users can subscribe to dashboards to receive scheduled dashboard updates pushed by the system, enabling close tracking of the latest data. At the same time, the product provides a subscription management feature to help users manage their subscription records and supports modifying subscriptions for dashboards where they have management permissions.

A Webhook is a mechanism by which one application sends an automated notification (usually an HTTP request) to another application when a specific event occurs.

To push dashboard subscription messages to **WeCom group chats, DingTalk regular groups, Larkxternal groups, or system API**, you can select the **Webhook push method** to **receive messages in the enterprise IM group**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb81a14b784e4006a38ccae3bd52dacb~tplv-goo7wpa0wc-image.image) </span>

<span id="6541631d"></span>
# Prerequisites

The Webhook configuration feature is only available to project administrator accounts. Please obtain project management permissions first. For details about permissions, refer to [Permission Overview](https://docs.byteplus.com/docs/DataWind/Permission_Overview).

<span id="41720041"></span>
# Quick start


1. Preliminary steps: Depending on the interface type, complete operations such as creating a new group bot as needed to obtain the Webhook address or API information.

2. Create a new Webhook configuration. Go to "Project Center" – "Webhook Configuration" page, click the New Configuration button, enter the relevant parameters, and complete the configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/470ca25336424aa7b34af66e58f7d069~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Name |Supports user\-defined Webhook names; it is recommended not to exceed 30 characters. |
   |URL |This is the URL corresponding to the Webhook, that is, the actual destination for Webhook message delivery.<br><br><br>* For group bots, this URL is provided by the group bot information from the corresponding platform (such as DingTalk, 飞书, or WeCom).<br><br>* For self\-developed systems, this is your server's API address for receiving messages. |
   |Secret |The key used for **signature encryption or request source verification**. Not all platforms require this. For example, if a key is needed for the generic IM interface, enter it here; if the API requires authentication, you can also enter the Token or other information here. |
   |Remarks |Optional. Supplementary description for this Webhook configuration, such as its purpose, responsible personnel, and more. |
   |Interface type |Select the platform or protocol type that this Webhook configuration connects to. The system will adapt the message format according to your selection.<br><br><br>* API interface: Suitable for connecting to Lark bots or third\-party self\-built systems.<br><br>* Generic IM bot: Suitable for internal company or third\-party customized IM platforms.<br><br>* DingTalk group bot: Dedicated for connecting to DingTalk group custom bots.<br><br>* WeCom group bot: Dedicated for connecting to WeCom group bots. |
   |Subscription events |* Subscription: Scheduled dashboard push tasks triggered at specified times. For example, automatically push the sales daily report to the group chat at 9:00 a.m. every day. For details, see [Data Subscription](https://docs.byteplus.com/docs/DataWind/Data_Subscription).<br><br>* Monitoring alert: When your configured data monitoring rules are triggered (such as metric anomalies or threshold breaches), the system will immediately send an alert message. For details, see [Monitoring and Alerting](https://docs.byteplus.com/docs/DataWind/Monitoring_and_Alerting).<br><br>* Insight report: The system automatically analyzes data based on attribution decision features (such as attribution analysis and anomaly detection), and the generated insight reports are pushed through this event. For details, see [Attribution Subscription](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f62844).<br><br>* Dataset synchronization monitoring: Sends notifications when dataset synchronization tasks succeed, fail, or experience abnormal duration. For details, refer to [Synchronization Settings](https://docs.byteplus.com/docs/DataWind/Synchronization_Setting).<br><br>* Add chart comments: Monitors and pushes notifications for chart comment operations within this project. The push content includes the comment content, commenter, related personnel, and the comment target (chart name), and other information.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The "Insight Report" feature is only supported in private deployment V2.64.0 and later versions.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The "Add Chart Comment" feature is only supported in V2.87.0 and later versions.   </div><br>    |
   |Scope of availability |Optional: Available only to the creator or to all members under the project.<br><br><br>* Available only to the creator: Only the configuration creator can see and select it when subscribing.<br><br>* Available to all members under the project: All users within the project who have permission to create subscriptions can select this configuration. |
   

3. Create a subscription. In the dashboard's new subscription section, complete the subscription configuration. For detailed steps, refer to the specific push scenario and [Data Subscription](https://docs.byteplus.com/docs/DataWind/Data_Subscription).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f7796a120004532a544b7e454918781~tplv-goo7wpa0wc-image.image) </span>


<span id="5f2e6bda"></span>
# Push scenarios

<span id="017e7946"></span>
## WeCom group chat push

<span id="2258b77b"></span>
### Step 1: Create a group bot

Before configuring subscription push, complete the creation and configuration of a group bot in WeCom. With your custom group bot, you can obtain the Webhook URL and then configure it in this product's subscription push method. For details, see [How to set up a group bot in WeCom](https://open.work.weixin.qq.com/help2/pc/14931#%E4%BA%94%E3%80%81%E7%BE%A4%E6%9C%BA%E5%99%A8%E4%BA%BAWebhook%E5%9C%B0%E5%9D%80).


1. Enter the WeCom group chat, click the "···" icon in the upper right corner, select "Add Group Bot," and create a group bot.

2. The creator of the group robot can view the robot information to obtain the group robot's Webhook address. You will use this address in subsequent steps.


<span id="d2066da9"></span>
### Step 2: Create a WeCom group Webhook


1. Create a new configuration in "Project Center" – "Webhook Configuration".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3612c14b04e4fbabbe720e610fb2186~tplv-goo7wpa0wc-image.image) </span>

2. In "Create Webhook Configuration", enter a custom name and URL (the **Webhook address** corresponding to the robot), select your interface type as WeCom group robot, then select the subscription events you need and set the applicable scope.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa8575f0816543f1b48c519adba69317~tplv-goo7wpa0wc-image.image) </span>


<span id="aff1e0a9"></span>
### Step 3: Create a subscription


1. You can click the upper right corner of the dashboard to create a subscription.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c058ad01c9524ac4ad04095d993401f4~tplv-goo7wpa0wc-image.image) </span>

2. In "Create Subscription – Subscription Notification", select the push method as "WeCom group", and select the recipient as the Webhook name you created.

3. After configuration is complete, you can click "Send Test" to verify whether the subscription message appears in the group. If the test is successful, click "Confirm".


<span id="53ec2594"></span>
## DingTalk standard group push

<span id="bb2f4d3d"></span>
### Step 1: Create a group robot

Before configuring subscription push, complete the creation and configuration of the group robot in DingTalk. Through your custom group robot, you can obtain the Webhook URL, which can then be configured in the subscription push method of this product. For details, see [How to set up a group robot in DingTalk](https://open.dingtalk.com/document/orgapp/custom-robot-access).


1. Enter the DingTalk group chat, click "Group Settings" \> "Smart Group Assistant" to create a group robot, select "Custom Robot" on the robot management page, enter the robot name, and select the group to send messages to.

2. Obtain the group robot's Webhook address. You will use this address in subsequent steps.


<span id="61e73094"></span>
### Step 2: Create a DingTalk standard group Webhook


1. Create a new configuration in "Project Center" – "Webhook Configuration".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08815bdcd182468aa0b2e99b113654d8~tplv-goo7wpa0wc-image.image) </span>

2. In "Create Webhook Configuration", enter a custom name and URL (the **Webhook address** corresponding to the robot), select your interface type as DingTalk group robot, then select the subscription events you need and set the applicable scope.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a0261ed5521461cb661013cfe021878~tplv-goo7wpa0wc-image.image) </span>


<span id="a44778f4"></span>
### Step 3: Create a subscription


1. You can click the upper right corner of the dashboard to create a subscription.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55fa1230eb424f42ada96e3da6b3b735~tplv-goo7wpa0wc-image.image) </span>

2. In the New Subscription \- Subscription Notification section, select the push method as "DingTalk regular group" and select the recipient as the Webhook name you created.

3. After configuration is complete, you can click "Send Test" to verify whether the subscription message appears in the group. If the test is successful, you can click "OK".


<span id="8053a1ec"></span>
## Lark external group push

<span id="7873809f"></span>
### Step 1: Create a group bot

Before configuring subscription push, complete the creation and configuration of a group bot in Lark. By using your custom group bot, you can obtain the Webhook URL, which can then be configured as the subscription push method in this product. For detailed steps, see [How to set up a group bot in Lark](https://open.feishu.cn/document/client-docs/bot-v3/add-custom-bot).


1. Enter the Lark external group, click the "···" in the upper right corner, select Settings \> Group Bots \> Add Bot \> Add Custom Bot.

2. Obtain the Webhook address of the group bot. You will use this address in subsequent steps.


<span id="82155e86"></span>
### Step 2: Create a Lark external group Webhook


1. Create a new configuration in "Project Center" \- "Webhook Configuration".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08815bdcd182468aa0b2e99b113654d8~tplv-goo7wpa0wc-image.image) </span>

2. In "Create Webhook Configuration", enter a custom name and URL (the bot's corresponding **Webhook address**), select API as the interface type, then select the subscription events you need and set the available scope.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f2e9946269e4a638928c2d52b4235e4~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="079a57c0"></span>
### Step 3: Create a subscription


1. Click Create Subscription in the upper right corner of the dashboard.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de73019ad71a453fa6ab8b00981d1f18~tplv-goo7wpa0wc-image.image) </span>

2. In the New Subscription \- Subscription Notification section, select the push method as "Webhook".

3. After configuration is complete, you can click "Send Test" to verify whether the subscription message appears in the group. If the test is successful, you can click "OK".


<span id="213fa75b"></span>
## API push

<span id="8b9bde1f"></span>
### Step 1: Obtain the API

Prepare the API address for your users to receive subscription messages.

<span id="d6c45905"></span>
### Step 2: Confirm the subscription push structure

The following provides the output script specification for your reference.

```JSON
{
   "context":{
       "screenshots":[//Screenshot information
           {
             "img_key": "img_v3_0290_e3cbb4e4-9ad2-4e94-88330-05f6da41d3bg",//Screenshot key
             "title":"页面1",
             "url": "https://el68-2-8abi.datarangers-onpremise.volces.com/minio.datawind/82f366da-0bf1-4i7c0-a9a2-
522174a39824.jpeg",//Image download URL
              "height":770,//height
              "width":1160,//width
              "time":"2024-03-15 12:32:07 UTC+08:00",//screenshot time
              "sheetUrl": "https://e168-2-8abi.datarangers-
              onpremise.volces.com/"//sheet access URL
                 }
             ],
             "subscription":{//subscription information
             "dashboard_link_visible": true,
             "language": "zh_CN",
              "title":"【Datawind订阅】test",
              "manage_url": "https://el68-2-8abi.datarangers- 
onpremise.volces.com/bi#/dashboard/subscripticon/35905?appId=1"
              "push_type": "webhook",
               "dashboard_id":35905,//dashboard ID
               "owner": "admin",
               "dashboard_content_visible": true,
               "id": 40
              }
          },
                "card":{},//card is a Lark protocol structure, ignored here
                "msg_type": "interactive"
     }
```


<span id="d111179c"></span>
### Step 3: Select Webhook as the subscription push method


1. Click Create Subscription in the upper right corner of the dashboard.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f876d90f10e24d34b7b4f95dd85deee2~tplv-goo7wpa0wc-image.image) </span>

2. In the New Subscription \- Subscription Notification section, select the push method as "Webhook"; for the recipient, select "1) Quickly create webhook".

3. In "Create Webhook configuration," enter a custom name and URL (the bot's corresponding **Webhook address**), select API interface as the interface type, then choose the events you want to subscribe to and set the available scope.

4. Select the recipient as the Webhook name you just created. After configuration is complete, you can click "Send test" to verify whether the subscription message appears in the group. If the test is successful, click "Confirm."


<span id="c3aeae4f"></span>
## General IM

For integration scenarios involving company\-developed IM collaboration tools, OA systems, or other third\-party applications, such as subscription, monitoring, and dataset task monitoring notifications, "General IM" capability support is provided. Essentially, this uses WebHook functionality to transmit information, and by mapping users in advance with third\-party systems, information can be delivered to specific users.

The General IM capability operates at the project level, meaning each project can independently configure one or more General IMs.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dad71fe4cbdd42aba3532ca288643da5~tplv-goo7wpa0wc-image.image) </span>

<span id="3eb5ee8f"></span>
### Step 1: Create IM\-WebHook configuration


1. The administrator enters the project center, clicks WebHook configuration, and creates a new WebHook configuration on the right.

2. After obtaining the API address and key in IM for users to receive subscription messages, select General IM bot as the interface type, then choose the events to subscribe to and set the available scope.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1618a3b5c0834d44a202c4e49794265a~tplv-goo7wpa0wc-image.image) </span>

<span id="88aa745d"></span>
### Step 2: Create subscription


1. Click "Create subscription" in the upper right corner of the dashboard.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/445937fc75d04e22b3bd980e3a3ffc22~tplv-goo7wpa0wc-image.image) </span>

2. Select **General IM,**  as the push method, and choose the IM bot you just configured as the recipient. After configuration is complete, you can click "Send test" to verify whether the subscription message appears in the group. If the test is successful, click "Confirm."

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd95ad52b5a74e4c895dae92edb9868d~tplv-goo7wpa0wc-image.image) </span>
