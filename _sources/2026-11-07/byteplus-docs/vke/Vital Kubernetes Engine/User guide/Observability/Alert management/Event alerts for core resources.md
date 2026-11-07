---
title: "Event alerts for core resources"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Event_alerts_for_core_resources"
---

VKE supports integrating exception events in VKE cluster core resources with Cloud Monitor. You can configure event alert rules based on these events to receive notifications immediately after an exception occurs in a cluster. This shortens troubleshooting and recovery time. This topic provides an example on how to configure Feishu event alerts to help you promptly detect and respond to cluster exception events.

<span id="HpeLwGPo"></span>
## Background

After a cluster is created, VKE automatically integrates exception events of core cluster resources (such as clusters, node pools, nodes, and add\-ons) with Cloud Monitor. As a result, cluster events can be continuously reported without additional configuration and you can query and handle them in the Event Center of the Cloud Monitor console. Based on these integrated events, you can also configure event alert rules to receive notifications immediately after an exception occurs in a cluster, proactively identifying key issues that affect cluster stability, security, and availability. This shortens troubleshooting and recovery time, ensuring high availability and continuity of your business. This is applicable to scenarios such as cluster O&M and monitoring, troubleshooting, and alert response. For supported exception types for core cluster resources, see [Event overview](https://docs.byteplus.com/en/docs/vke/Event-monitoring-overview?lang=en).

<span id="tulThUlw"></span>
## Prerequisites

A cluster has been created and is in the **Running** state. For details, see [Creating managed clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster?lang=en).

<span id="UUR8QSfE"></span>
## Procedure

Cloud Monitor supports various alert notification methods. This topic provides an example on how to configure Feishu alert notifications for VKE cluster events.

<span id="f2EEdg6Z"></span>
### Step 1: Configure a Feishu bot

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Feishu alert bots may vary based on different organizations. This topic uses a <strong>custom bot</strong> as an example. If you do not know the alert bot name in your organization, contact your Feishu administrator.</div>



1. Use your Feishu account to log in to Feishu and create or find the group that needs to receive alerts. Click `...` in the upper‑right corner of the group and click **Settings** from the drop‑down menu.

2. In the pop\-up panel, click **Bots** and click **Add bot**.

3. In the bot list, click **Custom Bot** and click **Add**.

4. Configure the information about the bot.

   * Specify the name and description of the bot.

   * View and configure the information about the bot.

      * Copy the **Webhook URL** of the bot. This address will be used in subsequent configuration.

      * Select **Set signature verification** and copy the **Key**. This key will be used in subsequent configuration.

5. Click **Finish** to add the bot.


<span id="ogtoZW3U"></span>
### Step 2: Create a callback URL


1. Log in to the [Cloud Monitor console](https://console.byteplus.com/observe/cloud-monitor/overview).

2. In the left navigation pane, click **Notification \> Notification Policy**.

3. Click the **Notification object** tab and select **Callback**. Click **Create Callback** and configure the callback URL that corresponds to the Feishu bot.

4. Click **connectivity testing** to verify whether the current callback URL is connected as expected. When the callback URL is connected, the Feishu bot will receive the corresponding notification.


<span id="OzfpJD5l"></span>
### Step 3: Create a notification policy


1. In the left navigation pane, click **Notification** \> ** Notification Policy**.

2. Click the **Notification policy** tab and click **Create notification policy** to configure the details about the policy.

   * For the **Notification method** parameter, select **Lark swarm robot**.

   * For the **Webhook** parameter, select the created callback URL.

3. Specify other parameters and then click **Confirm** to complete the configuration.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For more information about the parameters of notification policies, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Create_a_notification_policy?lang=en">Creating notification policies</a>.   </div>
   

<span id="7pHYa3m3"></span>
### Step 4: Create an event rule


1. In the left navigation pane, select **Event Center \> Event Rule**.

2. On the **Event rule** page, click **Create event rule**. Then, configure the rule details.

   * For the **Resource type** parameter, select VKE.

   * For the **Event name** parameter, select the event that requires an alert. In this example, **All** is selected.

   * For the **Severity level** parameter, select the level for the corresponding event.

   * For the **Notification policy** parameter, select the created notification policy.

3. Click **Confirm** to finish.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For more information about the parameters of the event rule, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule?lang=en">Creating event rules</a>.   </div>
   

<span id="iRcDLMuJ"></span>
## Validate results


1. After you have completed alert\-related configuration, when an alert that matches the defined rules is triggered, a notification will be sent to Feishu through the specified Feishu bot. You will receive the alert notification details in the group.

2. In the left navigation pane of the Cloud Monitor console, click **Alarm Center** \> **Alarm History** to view the generated log alerts.


<span id="Tb5r5yc9"></span>
## Related documentation

For more configuration methods for event alerts targeting different channels, see the following document. You only need to replace the **Create an alert policy** step in those topics with the **Create an event rule** step.


* [Receiving alert notifications through a Feishu group](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-Feishu-groups?lang=en)

* [Receiving alert notifications through a DingTalk group](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-DingTalk-groups?lang=en)

* [Receiving alert notifications through a WeCom group](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-WeChat-groups?lang=en)

* [Using event alert callback](https://vsop-online.bytedance.net/doc/manage/detail/6460/detail/?DocumentID=2650677&lang=zh)


&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
