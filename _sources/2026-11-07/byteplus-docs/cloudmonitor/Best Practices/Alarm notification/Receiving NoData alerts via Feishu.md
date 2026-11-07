---
title: "Receiving NoData alerts via Feishu"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Receive-NoData-alarm-notifications-through-Lark"
---

In user\-side data collection, cloud products may hang, causing resource metrics not to be reported to Cloud Monitor. This topic uses Feishu Webhook as an example to describe how to configure NoData alerts for cloud products. When an alert policy is triggered, alert notifications are pushed to designated Feishu groups. This helps you promptly monitor metrics that have no data.

<span id="6975285e"></span>
## Considerations


* Feishu group bots fall into two types: app bots and custom bots. This topic is about adding a custom bot. For instructions on using Feishu group bots, see [How to use bots in groups](https://www.feishu.cn/hc/zh-CN/articles/360024984973).

* Custom bots are supported only on the Feishu desktop application. Each Feishu group can contain up to 99 bots.


<span id="7cf9993e"></span>
## Procedure:

<span id="7cf9993e"></span>
### Step 1: Add a bot to a Feishu group


1. Launch the Feishu desktop app and go to the group where you wish to add a custom bot.

2. In the upper\-right corner of the group chat, select  **`···`**  \> **Settings**.

3. On the **Settings** page, click **Group bot**.

4. In the upper\-right corner of **Group bot** page, click **Add bot**.

5. In the **Add bot** dialog box, find and click **Custom bot**.

6. In the pop\-up window, set the bot avatar, name, and description, then click **Add**.

   Once the bot is successfully added, you will be able to see its Webhook URL.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To ensure the group bot receives alert notifications, we recommend disabling all the options under <strong>Security Settings</strong>.   </div>
   

7. Click **Copy** next to the **Webhook URL** to copy the bot Webhook, then click **Finish**.

   Later, when configuring an alert policy in Cloud Monitor, you need to set this bot webhook as the alert callback URL.


<span id="f35b3996"></span>
### Step 2: Create a callback address


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).  console

2. In the left navigation bar, click **Notification** \> **Callback**.

3. On the **Callback address list** page, click **Create callback address**.

4. On the **Create callback address** page, complete the following configuration, then click **Confirm**.

   
   |Parameter |Descriptions |Example |
   |---|---|---|
   |Callback address name |Configure a callback address name to identify the callback address. Duplicate names are not allowed. |Feishu NoData alert URL |
   |Callback address type |Select callback address type. Supported types include Feishu, DingTalk, WeCom, and Generic Webhook. |Feishu |
   |Callback address |Enter a publicly accessible URL, then click **Test **  to verify the callback address.<br><br><br>* If the callback URL returns the HTTP status code 200, it indicates that the connectivity test is successful, and the webhook can receive alerts and event notifications.<br><br>* The connectivity test enforces a one query per second (QPS) limit. |https://open.feishu.cn/open\-apis/bot/v2/hook/\*\*\* |
   


<span id="edaccb3b"></span>
### Step 3: Create an alert policy


1. In the left navigation bar, click **Alert center \> Alert policy**.

2. On the **Alert policy** page, click **Create Alert policy**.

3. On the **Create alert policy** page, complete the configuration according to your business needs, then click **Confirm**.

   Parameter description:

   
   |Section |Parameter |Descriptions |Example |
   |---|---|---|---|
   |Basic information |Name |Specify a custom name for the alert policy to identify the alert policy. |NoData alert callback test |
   ||Description |Specify a custom description for the alert policy. |None |
   |Alert object |resource type |Specify the type of cloud products under monitoring. |Elastic Compute Service (ECS) |
   ||Region |The region of the resources under monitoring. |China (Beijing) |
   ||Subnamespace |Specify the resource dimension of the cloud product under monitoring. |Instance |
   ||Resource |Set the resource scope for the alert policy, meaning monitoring will only be performed within this scope. Available options are as follows:<br><br><br>* All: Applies the alert policy to all resources under the current account that match the specified resource type, region, and dimensions.<br><br>   After selection, the created resources that meet the conditions will automatically match the alert policy.<br><br>* Part: You need to manually select one or more resources.<br><br>   After selection, the alert policy will be effective only for the selected resources.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">NoData alert notifications will not be sent if the corresponding resource is deleted.</div><br><br><br><div data-tips="true" data-tips-type="warning">For example, when the resource scope of an alert rule is set to "All", deleting a resource (e.g., Resource A) will not trigger a NoData alert, even if the data reports are missing for N consecutive cycles afterward.</div><br> |All |
   |Alert rules |Metric type |Select the metric type. Available options: **Single\-metric** and **Multi\-metrics**. If you need to monitor multiple metrics of a resource, you can select Multiple\-metrics.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If a rule triggers both a threshold alert and a NoData alert simultaneously, two separate notifications will be sent.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Not all cloud service metrics support NoData alerts. At present, NoData alerts can only be configured for cloud product metrics that have an alert rule dimension of "Instance" and involve resources at a single level. Please refer to the console for the actual configuration.</div><br> |Multiple\-metrics |
   ||Trigger condition |Configure the metrics, duration, statistic type, comparison operator, and threshold for the alert. If the monitored resource metric meets the trigger condition, the system will send an alert notification.<br><br><br>* If the **Metric type** is set to **Single\-metric**, only one trigger condition can be configured.<br><br>* If the **Metric type **  is set to **Multi\-metrics**, one or more trigger conditions can be configured. |If any metric condition is met for one cycle, an alert is triggered.<br><br><br>* Average CPU usage \> 1%<br><br>* Maximum disk \> 10 MiB<br><br>* Average memory usage \> 20% |
   ||Alert level |Specify the severity level of the alert. Valid values: **Critical**, **Warning**, **Notice**. |Critical |
   ||Effective time |Configure the effective time of the alert policy. The alert policy monitors resource data against trigger conditions only during its effective time. |00:00~23:59 |
   ||Mute For |After an alert policy is triggered, if the monitored resource continuously triggers alerts, the system will periodically send alerts to prevent excessive notifications.<br><br><br>* Available options include **5 minutes**, **10 minutes**, **15 minutes**, **30 minutes**, **60 minutes**, **3 hours**, **6 hours**, **12 hours**, **24 hours**.<br><br>* The default value is 5 minutes. |5 minutes |
   ||Alert recovery notification |Send a recovery notification to the user when the alert is resolved. This is enabled by default.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">An alert recovery notification is sent when the alert policy status returns to <strong>normal</strong>. This indicates that Cloud Monitor has determined the alert has been resolved.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">In a NoData alert scenario, a recovery notification is sent when the resource resumes data reporting for 5 consecutive minutes.</div><br> |Enable |
   ||NoData alert |Specify the number of consecutive cycles. A NoData alert will be triggered if no data is reported from the resources of cloud products during those cycles.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can configure 3 to 20 cycles. The default value is 10 cycles.</div><br> |Enable<br><br>If a resource reports no data for 3 consecutive cycles, a NoData alert will be triggered. |
   |Alert way |Alert channel |Select one or more channels. Valid values: **Email**, **Phone**, **SMS**, and **Alert callback**. |Alert callback |
   ||Alert callback |* You must specify a public URL as the webhook URL. Later, when a resource triggers the alert policy, the alert details will be sent to this URL via POST for further data analysis.<br><br>   * You can select created webhook URLs. Up to eight webhook URLs can be selected.<br><br>   * You can enter only one webhook URL.<br><br>* We recommend that you prepare an HTTP server accessible via the Internet, and then set the URL of the server as the callback URL.<br><br>* For more information about alert callback, see [Alert callback usage](https://docs.byteplus.com/en/docs/cloudmonitor/Webhook-instructions). |Feishu NoData alert URL |
   


<span id="ecce005c"></span>
## Verifying results

<span id="ecce005c"></span>
### View alert notification

Once an alert policy is triggered by a cloud product, the custom bot will send a notification to your Feishu group.
