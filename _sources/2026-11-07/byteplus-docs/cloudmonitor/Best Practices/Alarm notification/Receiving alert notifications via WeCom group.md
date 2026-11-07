---
title: "Receiving alert notifications via WeCom group"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-WeChat-groups"
---

Cloud Monitor alert callback feature supports WeCom group bot webhooks. When an alert policy is triggered, notifications are automatically pushed to the specified WeCom group.

<span id="519b83e5"></span>
## Considerations


* There is no upper limit on the number of bots that can be added to a WeCom group. However, each bot cannot send more than 20 messages per minute.

* This topic uses the WeCom mobile app as an example to show how to add a group bot. You can also add a group bot and obtain its webhook by referring to the WeCom official documentation. For details, see [How to Set Up a Group bot](https://open.work.weixin.qq.com/help2/pc/14931).


<span id="9cc45f7e"></span>
## Procedure

<span id="9cc45f7e"></span>
### Step 1: Add a bot to a WeCom group


1. Log in to the WeCom mobile app and navigate to the WeCom group where you want to add the bot.

2. In the upper\-right corner of the group chat, click the `...` icon.

3. Find and click **Group bot**.

4. In the upper\-right corner of the page, click **Add**, then enter a name for the bot to complete the addition.

5. After successfully adding the bot, you can view its corresponding webhook information. Click **Copy** to copy the Webhook information, then click **Done** in the upper\-right corner of the page.


<span id="4e3ac8d7"></span>
### Step 2: Create a callback address


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation bar, click **Notification** \> **Callback**.

3. On the **Callback address list** page, click **Create callback address**.

4. On the **Create callback address** page, complete the following configuration, then click **Confirm**.

   
   |Parameter |Descriptions |Sample value |
   |---|---|---|
   |Callback address name |Configure a callback address name to identify the callback address. Duplicate names are not allowed. |Doc |
   |Callback address type |Select a callback address type. Supported types include **Feishu**, **DingTalk**, **WeCom**, and **Generic callback address**. |WeCom |
   |Callback address |Enter a publicly accessible URL, and then click **Test** to verify the callback address.<br><br><br>* If the callback URL returns an HTTP status code 200, it indicates that the connectivity test is successful, and the webhook can receive alerts and event notifications.<br><br>* The connectivity test enforces a one query per second (QPS) limit. |Paste the bot Webhook |
   


<span id="42025f6c"></span>
### Step 3: Create an alert policy


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation bar, click **Alert Center \> Alert policy**.

3. On the **Alert policy** page, click **Create Alert policy**.

4. On the **Create alert policy** page, configure the basic information, alert object, and alert rule according to your business, set the alert method as shown below, then click **Confirm**.


<span id="3c9238e5"></span>
## Verifying results

<span id="3c9238e5"></span>
### View alert notification

When a cloud product triggers a corresponding alert policy, you can receive message notifications sent by a custom bot in the WeCom group.
