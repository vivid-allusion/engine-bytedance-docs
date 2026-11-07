---
title: "Alert management"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/alert_management"
---

Alert tasks are divided into crash alert, error alert, lag alert, page monitoring alert, and more. The configuration method for each type of alert task is similar, but the metrics differ.

<span id=".5bSp5rqD5oql6K2m"></span>
## Create an alert task

<span id="879db72e"></span>
### Operation Procedure

Using crash alert as an example, this introduces how to create an alert task.


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. Click **App Monitoring** under the target application.

3. In the upper left corner of the console, select**All features \> Crash alert**.

4. On the **crash alert task** page, click **create alert task**.

5. On the **Create alert task** page, complete the following configuration, and then click **Save**.

   Configuration description:

   
   |**Configuration area** |**Parameter** |**DescriptionS** |
   |---|---|---|
   |Basic information for alerts |Alert task name |Custom name, used to identify alert tasks. |
   ||Alert description |Provide a description of the purpose of this alert task, as well as the response plan or other relevant information in the event of an alert. |
   ||alert level |Supports the Warning and Fatal levels.<br><br><br>* **Warning**: Warning<br><br>* **Fatal**: Severe |
   |Establish an alert policy |Filter dimensions |Support filtering metrics by dimension.<br><br>Supported filter criteria: **Operating System name**, **Operating System version**, **APP version**, **Device ID**, **SDK version**, **issue status**, **crash type**, **device model**, **APP minor version**, **download channel**, **APP page**, **issue new status**, **crash details**, **Host APP ID**.<br><br>Specifically, the newly added dependency version number in the issue is related to the version in which it first appeared.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The dimensions of each type of alert task may vary; the interface shall prevail for specifics.</div><br> |
   ||alert rule |When configuring multiple policy relationships, you can configure the relationships between policies.<br><br><br>* **Simultaneously meet all of the following rules**: An alert is triggered only when multiple alert strategies simultaneously reach their thresholds.<br><br>* **Satisfy any of the following rules**: An alert is triggered if any of the multiple alert strategies reach their threshold. |
   ||Task execution intervals |The task execution interval refers to how frequently the backend polling service runs. For example, if a 5\-minute interval is configured, the service checks every 5 minutes to see if the metric values from the most recent period meet the alert threshold.<br><br>Supports **5 minutes**, **10 minutes**, **30 minutes**, and **60 minutes**. |
   ||Alert metrics |You can add multiple metric policies.<br><br><br>* Recent N minutes: The size of the time window for checking data.<br><br>* Metric: Different alert types have different metrics. If the alert type is set to the composite metric, the metric here will require a complex configuration, and the calculation rules for the composite metric must be configured separately.<br><br>* Filter criteria:<br><br>   * **Threshold**: An alert is triggered when the exception count within a single time window reaches a certain amount.<br><br>   * **Comparison**: Refers to whether, within a single time window, the percentage increase or decrease in value compared to the value in the same time window n time units earlier exceeds the specified setting. |
   ||Alert activation time |The effective time defaults to 00:00–23:59 (all day). If the selected metric fluctuates significantly within a day and alert thresholds vary across different time periods, you can avoid too many alerts by setting the time period during which the alert is active. |
   ||Alert groups |After you turn on grouped alert, an alert is triggered if any group meets the alert condition. |
   ||Alert callback |After setting the alert callback address, when an alert is triggered, an HTTP POST request will be sent to the URL you specified to receive the callback. For detailed callback information, refer to [request body field](https://docs.byteplus.com/en/docs/apmplus/alert_management#1eb1116a). |
   |Configure notification audiences |alert method |Support alerting via **Lark**, **email**, **WeCom**, and **DingTalk**. |
   ||Lark webhook |Enter Lark webhook. When the alert method is set to **Lark**, this field is required.<br><br>For details on webhook configuration, see [How do I configure a webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   ||People to @\-mention in Lark |Lark users whose alert notifications are configured according to User ID or Open ID. When you select **Lark** as the alert method, this is optional.<br><br>To obtain User ID and Open ID, refer to [How to obtain User ID, Open ID, and Union ID](https://open.feishu.cn/document/home/user-identity-introduction/open-id).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The notification recipient must be in the same group as the group robot.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Please ensure that the User ID and Open ID are correct; otherwise, the notification cannot be pushed to the user.</div><br> |
   ||Email notification group |Configure the recipient group for email notifications When the alert method is selected as **email**, this field is required. |
   ||WeCom webhook |Enter a WeCom webhook. When the alert method is set to **WeCom**, this field is required.<br><br>For details about webhook configuration, see [How do I configure a webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   ||People who need to be @\-mentioned in WeCom |WeCom users for whom alert notification configuration is based on mobile phone number or User ID. When the alert method is set to **WeCom**, this field is optional.<br><br>For information on how to obtain a User ID, refer to [User ID](https://developer.work.weixin.qq.com/document/path/98728#.5piO5paHdXNlcmlk).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The individual to receive the notification must be in the same group as the group bot.</div><br> |
   ||DingTalk webhook |Enter a DingTalk webhook. When the alert method **DingTalk** is selected, this field is required.<br><br>For details on webhook configuration, see [How to configure a webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   ||People to mention in DingTalk |DingTalk users for whom alert notification configuration is based on mobile phone number or User ID. When the alert method is set to **DingTalk**, this field is optional.<br><br>To obtain the User ID, refer to [User ID](https://open.dingtalk.com/document/orgapp/basic-concepts#title-o8w-yj2-t8x).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The notification recipient must be in the same group as the group bot.</div><br> |
   ||Alert event name |Custom name used to identify the alert event. |
   ||Alert content |Custom alert content. |
   


<span id="6ef1b507"></span>
### Back to alert

<span id="1eb1116a"></span>
#### **request body field**

The request body contains callback information in JSON format, with the following fields:


|**Field** |**Type** |**Sample value** |**DescriptionS** |
|---|---|---|---|
|rule |object |\- |The original alert rule. For details, refer to **rule data structure**. |
|context |object |\- |Content of the callback after the alert is triggered. For details, refer to **context data structure**. |


<span id="95ecc4fd"></span>
#### **Context data structures**


|**Field** |**Type** |**Sample value** |**DescriptionS** |
|---|---|---|---|
|top_issue_infos |array[TopIssueInfo] |\- |Speculate on the top issue related to alerts. Up to 5. For details, refer to **TopIssueInfo data structure**. |
|detail_url |string |`https://console.byteplus.com/observe/apmplus-client/app/crash/alarm_record?aid=123456` |Alert detail page. |
|message |string |`APM alert`<br><br>`Application name [Test app]`<br><br>`Alert module: crash/exception - test crash alert by issue`<br><br>`Alert time: 2022-05-07 18:01:43`<br><br>`Trigger condition (and):`<br><br>`Crash count in the last 180 minutes is greater than or equal to 1`<br><br>`Group 1: crash type: Native crash`<br><br>`Operating system name: Android issue details` |Alert information. |


<span id="853ab0e2"></span>
#### **The TopIssueInfo data structure**


|**Field** |**Type** |**Sample value** |**DescriptionS** |
|---|---|---|---|
|title |string |`com.ixigua.feature.video.player.layer.playtips.PlayTipLayer` |The issue title. |
|link |string |\- |issue link. |
|info |string |`Exception count = 1; Year-over-Year increase: 100%; Assignee: none` |issue metric value, metric fluctuation range, and assignee information. |


<span id="8cbcb08b"></span>
#### **Rule data structures**


|**Field** |**Type** |**Sample value** |**DescriptionS** |
|---|---|---|---|
|alarm_level |int |`0` |Alert level.<br><br><br>* **0**：warning<br><br>* **1**：fatal |
|check_cycle |int |`5` |Monitoring interval, measured in minutes; instantaneous alert is 0. |
|rule_status |int |`1` |The alert status.<br><br><br>* **1**Enable:<br><br>* **2**: Disable<br><br>* **0**: Delete |
|id |uint64 |`737` |Alert ID. |
|aid |int64 |`123456` |Application ID |
|day_active_start |int64 |`1654858020` |The effective start time for daily tasks. |
|day_active_end |int64 |`1654858020` |The effective end time for daily tasks. |
|create_at |string |`2022-04-20T20:56:30+08:00` |Task create time, Y\-M\-HTh:m:s+08:00. |
|update_at |string |`2022-04-20T20:56:30+08:00` |The latest task update time, Y\-M\-HTh:m:s+08:00. |
|name |string |`Test crash alert per issue` |The alert rule name. |
|description |string |`Test alert` |Alert rule description. |
|monitor_type |string |`crash` |Alert rule types.<br><br><br>* **crash**: crash<br><br>* **crash_defend**: crash protection<br><br>* **lag**: lag<br><br>* **app_page_js_err**: Page monitoring/JS error<br><br>* **app_page_ajax_err**: Page monitoring/request error<br><br>* **app_page_perf**: Page monitoring/performance<br><br>* **app_event**: event alert<br><br>* **net_err**: network error<br><br>* **custom_exception**: custom error<br><br>* **traffic_exception**: traffic<br><br>* **disk_exception**: disk<br><br>* **battery_trace**: battery<br><br>* **cpu_exception**：CPU |
|owner |string |`cc` |Rule creation. |
|day_active |string |`[`<br><br>`{`<br><br>`"activation_start":"00:00",`<br><br>`"activation_end":"23:59",`<br><br>`"activation_start_stamp":1541174400,`<br><br>`"activation_end_stamp":1541260740`<br><br>`}`<br><br>`]` |Effective start time for daily tasks. |
|callback_url |string |`https://console.byteplus.com/` |Alert callback address. |


<span id=".5oql6K2m5YiX6KGo"></span>
## Alert list

The alert list is used to display and manage created alert tasks. In the list, you can view the key fields and information for each alert task, and you can turn on or turn off one or more alert tasks.


* Task name: Click to enter the alert detail, and view the alert history and statistics page for this alert task.

* Edit: Click to modify parameters such as alert description, metric type, filter dimension, and alert rule. The alert task name and alert level cannot be modified.

* Alert detail: Click to enter alert detail, then view the alert overview and alert list.


<span id=".5oql6K2m6K-m5oOF"></span>
## alert detail

<span id="b192145b"></span>
### Filter items


* Filter criteria: time range, time granularity, and alert task.

* ACK: Click ACK to suppress alert notifications. Alert events will still be generated normally, and the rule will remain active.

   * By default, only the assignee specified by the rule and group members can ACK.

   * The initial status is **ACK**. The default blocking duration for a single ACK is 24 hours. You can modify the ACK duration on the **platform setting** page. For details, refer to [platform setting](https://docs.byteplus.com/en/docs/apmplus/Platform_setting).

   * After clicking **ACK**, set the due time. At the same time, the button status is **Reset ACK**. Within the 24\-hour period of ACK, users with permission can reset ACK at any time, and the countdown will be refreshed. After 24 hours, the button status returns to **ACK**.


<span id="230af8d4"></span>
### Alert status overview

The alert trend chart displays the alert count for each alert task, allowing you to observe fluctuations in the alert count for each task and identify the time periods when alerts occur more frequently, as well as other related information.

<span id=".5oql6K2m57uf6K6h"></span>
### The alert list

Each feature module, such as crash analytics, error analytics, and others, has a corresponding alert statistics module.

For example, in crash analytics, there is a **crash alert** feature, which is used to display and statistically analyze the alert history for crash types. You can also filter alert tasks to query the historical data of tasks you are interested in.
