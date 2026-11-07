---
title: "Receiving alert notifications via Feishu group"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-Feishu-groups"
---

You can set a Feishu bot webhook as the alert callback in Cloud Monitor. Then, alerts will be sent to the specified Feishu group when an alert policy is triggered.

<span id="7ZUJjqsL"></span>
## Considerations


* Feishu group bots fall into two types: app bots and custom bots. This topic is about adding a custom bot. For instructions on using Feishu group bots, see [How to use bots in groups](https://www.feishu.cn/hc/zh-CN/articles/360024984973).

* Custom bots are supported only on the Feishu desktop application. Each Feishu group can contain up to 99 bots.


<span id=".5q2l6aqk5LiA77ya5Zyo6aOe5Lmm576k5Lit5re75Yqg5py65Zmo5Lq6"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Zyo6aOe5Lmm576k5Lit5re75Yqg5py65Zmo5Lq6"></span>
### Step 1: Add a bot to a Feishu group


1. Launch the Feishu desktop app and go to the group where you wish to add a custom bot.

2. In the upper right corner of the group chat, select  **`···`**  \> **Settings**.

3. On the **Settings** page, click **Group bots**.

4. Click **Add bot**, find and click **Custom bot**.

6. In the pop\-up window, set the **bot avatar**, **Name**, and **Description**, then click **Add**.

   Once the bot is successfully added, you will be able to see its Webhook URL.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To ensure the group bot receives alert notifications, we recommend disabling all the options under <strong>Security Settings</strong>.   </div>
   

7. Click **Copy** next to the **Webhook URL** to copy the bot Webhook, then click **Finish**.

   Later, when configuring an alert policy in Cloud Monitor, you need to set this bot Webhook as the alert callback URL.


<span id="30545f84"></span>
### Step 2: Create a callback address


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation bar, select **Notification** \> **Callback**, click **Create callback address**, and configure a Feishu\-type callback address.

3. Click **Confirm** to complete the configuration.


<span id="b5b77794"></span>
### Step 3: Create an alert policy


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, select **Alert Center \> Alert Policy**, and click **Create alert policy**.

3. On the **Create alert policy** page, configure the basic information, alert object, and alert rules based on your business needs, and set up the alert method as shown in the example below.


<span id=".5q2l6aqk5LqM77ya6YWN572u5ZGK6K2m5Zue6LCD"></span>
## Verifying results

<span id=".5q2l6aqk5LqM77ya6YWN572u5ZGK6K2m5Zue6LCD"></span>
### View alert notification

Once an alert policy is triggered by a cloud product, the custom bot will send a notification to your Feishu group. 

&nbsp;
