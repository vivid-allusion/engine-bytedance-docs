---
title: "Receiving alert notifications via Slack"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Receiving_Alarm_Notifications_in_Slack_channels"
---

The alert callback feature of Cloud Monitor can be configured as a Webhook for Slack. Once configured, alert notifications can be sent to a designated Slack channel automatically whenever a cloud resource triggers an alert policy.

<span id="2xv1HD9j"></span>
## Background

Slack is an enterprise collaboration platform launched in 2013 and currently owned by Salesforce. Slack enhances team efficiency through its channel\-based chat interface, supporting real\-time sharing of text messages, voice communication, and files. It also integrates with over 2,000 third\-party applications, including Google Drive and Zoom. Its core features include creating topic\-based conversation channels, retrieving historical messages, assigning tasks, and automating workflows, effectively reducing email exchanges. It is especially well\-suited for remote teams and project collaboration, offering enterprise\-grade features such as cross\-device synchronization, permission management, and data encryption. Used by over 750,000 businesses worldwide, it has become an essential tool for digital workplaces. For more details, see [the official website of Slack](https://slack.com/intl/zh-cn/).

<span id="xaqwShXD"></span>
## Prerequisites


* You have signed up for Slack and created a workspace. For details, see [the official Slack documentation](https://slack.com/intl/zh-cn/help/articles/360059928654-%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8-Slack%EF%BC%9A%E4%BD%A0%E7%9A%84%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8%E6%8C%87%E5%8D%97?utm_source=hppromo&utm_medium=promo).

* You have created a channel in your workspace.


<span id="lA6XEEK2"></span>
## Procedure

<span id="xaqwShXD"></span>
### Step 1: Create a Slack application


1. Log in to [the Slack API website](https://api.slack.com/messaging/webhooks).

2. Click the **Create your Slack app** button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0904e51db251f8d73c78c7790728003b.png) </span>

3. Go to Your Apps and click the **Create New App** button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a27667f2b64c09c4521f46fa75bd1df6.png) </span>

4. In the pop\-up window, select **From a manifest**. You can also choose **From scratch** to start creating.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5d4c2fbaa1afd239f2579e31827993b7.png) </span>

5. Select the workspace where you want to install your app, then click **Next**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_10202b346d640ab75f2f9a043489543f.png) </span>

6. Configure basic information, then click **Next**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_71bce439308c2b5bfe8c2734523ebb1c.png) </span>

7. Click **Create** to complete creation.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6d5800055fa501c85d7c011acc4e8a84.png) </span>


<span id="MCIdYYvj"></span>
### Step 2: Obtain the Incoming Webhook for the Slack application


1. In the left navigation bar of the Basic Information page, select **Incoming Webhooks**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9b662e9e8b19529e28865b8ca04d2936.png) </span>

2. Click the **Activate Incoming Webhooks ** toggle to enable the Webhook feature.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1bdfa9f87b48dffefd93aeffb68973d.png) </span>

3. Click the **Add New Webhook to Workspace** button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_00618518e3a18b3e7d3f511e2412732f.png) </span>

4. Select the channel to receive messages and click **Allow**.

5. Click **Copy** to copy the generated Webhook URL.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7a348a684bf0d21d03c1fb0331395d91.png) </span>


<span id="SZgaAnf0"></span>
### Step 3: Create a callback address


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Notification** \> **Callback**.

3. On the **Callback address list** page, click **Create callback address**.

4. On the **Create callback address** page, complete the following configuration.

5. (Optional) Click **Test** to perform a connectivity test.

   You can also receive connectivity test information in the Slack channel.

6. Click **Create** to complete the configuration.


<span id="iyRpiNwg"></span>
### Step 4: Create an alert policy


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).  console

2. In the left navigation bar, click **Alert Center \> Alert policy**.

3. On the **Alert policy** page, click **Create alert policy**.

4. On the **Create alert policy ** page, configure the basic information, alert object, and alert rules based on your business needs, and set up the alert method as shown in the example below. For more configuration details, see [Creating alert policies](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).

5. Click **Create** to complete the configuration.


<span id="EtduIrud"></span>
## Verifying results

<span id="EtduIrud"></span>
### View alert notification

When a cloud product triggers the corresponding alert policy, you can receive alert notifications in your Slack channel. 

&nbsp;
