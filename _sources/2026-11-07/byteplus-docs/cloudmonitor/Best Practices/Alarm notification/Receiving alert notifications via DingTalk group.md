---
title: "Receiving alert notifications via DingTalk group"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-DingTalk-groups"
---

You can set a DingTalk bot webhook as the alert callback in Cloud Monitor. Then, alerts will be sent to the specified DingTalk group when an alert policy is triggered.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations

DingTalk bots can only be added via the desktop client. Each bot can send a maximum of 20 messages per minute to a group. If this limit is exceeded, messages will be throttled for 10 minutes. For official instructions and considerations for DingTalk group bots, see [Custom bot integration](https://open.dingtalk.com/document/robots/custom-robot-access).

<span id=".5q2l6aqk5LiA77ya5Zyo6ZKJ6ZKJ576k5Lit5re75Yqg5py65Zmo5Lq6"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Zyo6ZKJ6ZKJ576k5Lit5re75Yqg5py65Zmo5Lq6"></span>
### Step 1: Add a bot to the DingTalk group


1. Open the DingTalk desktop client and enter the DingTalk group where you want to add the bot.

2. In the upper right corner of the DingTalk group, click the settings icon.

3. On the **Group settings** page, click **Smart group assistant.** 

4. In the **Bot management** dialog box, click the  **...**  icon on the right side of `Add bot`.

5. In the search bar of the **Bot management** dialog box, enter **Custom** to search, and then click the **Custom** bot.

6. Click **Add**, then configure the bot.

   1. Configure the bot name and security settings.

      In **Security settings**, select **Custom keywords** and manually set the keywords.  as the keyword

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">You can set up to 10 keywords. A message can be sent successfully only if it contains at least one of these keywords.      </div>
      

   2. Read and select **I have read and agree to the Custom Bot Service and Disclaimer**.

7. Click **Finish**, then copy the bot **Webhook** in the dialog box.

   Later, when configuring an alert policy in Cloud Monitor, you need to set this bot webhook as the alert callback URL.

8. Click **Finish**.


<span id="66b48b1c"></span>
### Step 2: Create a callback address


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation bar, click **Notification** \> **Callback**.

3. On the **Callback address list** page, click **Create callback address**.

4. On the **Create callback address** page, complete the following configuration, then click **Confirm**.

   
   |Parameter |Descriptions |Sample value |
   |---|---|---|
   |Callback address name |Configure the callback address name to identify this callback address. Duplicate names are not allowed. |dingtalk\-alarm\-demo |
   |Callback address type |Select the callback address type. Supported types include **Feishu**, **DingTalk**, **WeCom**, and **Generic callback address**. |DingTalk |
   |Callback address |Enter a publicly accessible URL, then click **Test ** to verify the callback address.<br><br><br>* If the callback URL returns the HTTP status code 200, it indicates that the connectivity test is successful, and the webhook can receive alerts and event notifications.<br><br>* The connectivity test enforces a one query per second (QPS) limit. |DingTalk bot webhook |
   


<span id=".5q2l6aqk5LqM77ya6YWN572u5ZGK6K2m5Zue6LCD"></span>
### Step 3: Create an alert policy


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).  console

2. In the left navigation bar, click **Alert center \> Alert policy**.

3. On the **Alert policy** page, click **Create alert policy**.

4. On the **Create alert policy page**, set up the basic info, alert object, and rules as needed. Then follow the example to configure the alert method and click **OK**.


<span id="d719acc3"></span>
## Verifying results

<span id="d719acc3"></span>
### View alert notification

Once an alert policy is triggered by a cloud product, the custom bot will send a notification to your DingTalk group.
