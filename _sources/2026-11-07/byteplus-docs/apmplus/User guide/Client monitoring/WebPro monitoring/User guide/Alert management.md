---
title: "Alert management"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/alert_management_webpro"
---

Alert tasks support configuring alert strategies across multiple dimensions, including user analysis, performance metrics, JavaScript error metrics, static resource metrics, request metrics, and composite metrics. Flexible and complex custom configuration rules are also supported to meet your monitoring requirements for each metric.

<span id=".5paw5bu65oql6K2m5Lu75Yqh"></span>
## **Create an alert task**

<span id="9813940d"></span>
### Glossary


|Glossary |DescriptionS |
|---|---|
|SLA |Service level agreement (SLA). |
|SLO |Service level objectives (Service Level Objectives). In alert tasks, SLO refers to the threshold configured for alert metrics. |
|SLI |Service level indicators In alert tasks, SLI refers to the actual statistical value of the alert metric. |
|Budgets |* Budget calculation method for numerical metrics:<br><br>   For example, if the error count for alerts in a 10\-minute period exceeds 10, the budget for one day is 10.*6*24。<br><br>* Budget calculation methods for rate\-type metrics:<br><br>   For example, if the alert is triggered when the error rate exceeds 1% within a 10\-minute period, the daily budget will be calculated based on an average error rate of 1% for the entire day. |
|Budget consumption percentage |* Method for calculating the budget consumption ratio of numerical metrics:<br><br>   For example, if the number of alert errors in 10 minutes exceeds 10, then if the error count is 50 in 30 minutes, the proportion of budget consumed is 50/(10).*6*24)。<br><br>* Calculation method for the budget consumption ratio of rate\-type metrics<br><br>   For example, if the error rate for an alert exceeds 1% over a 10\-minute period, then if the error rate reaches 2% over a 30\-minute period, the proportion of budget consumed is 30*2/(24*60\*1). |
|Spike |Alert generated due to SLI fluctuations caused by some incidental factors. |


<span id="ee1777e2"></span>
### Operation Procedure


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. Click **Webpro Monitoring** under the target application.

3. In the upper left corner of the console, select **All features \> alert management**.

4. On the alert task page, click **Create alert task**.

   Parameter description:

   
   |**Configuration area** |**Parameter** |**DescriptionS** |
   |---|---|---|
   |Alert information |Alert task name |Custom name used to identify alert tasks. |
   ||alert level |Supports two levels: Warning and Fatal.<br><br><br>* **Warning**: Warning<br><br>* **Fatal**: Severe |
   ||Alert description |Describe the purpose of the alert task and the handling procedures or other information after an alert occurs. |
   |Create an alert policy |Alert types |Different alert types correspond to different alert metrics.<br><br>Supported alert types: **user analysis**, **performance metric**, **JavaScript error metric**, **static resource metric**, **static resource error metric**, **blank screen metric**, **request metric**, **request error metric**, **event metric**, **composite metric**, **custom log**. |
   ||Task execution intervals |The task execution interval refers to how frequently the backend polling service runs. For example, if a five\-minute interval is configured, the service will check every five minutes whether the metric values within the most recent period meet the alert threshold.<br><br>Supports**5 minutes**, **10 minutes**, **30 minutes**, and **60 minutes**. |
   ||Multiple policy relationships |When configuring multiple policy relationships, you can configure the relationships between policies.<br><br><br>* **The following rules must be satisfied simultaneously**: In the default configuration, an alert is triggered only when multiple policies are satisfied at the same time.<br><br>* **Meet any of the following rules**: If multiple policies meet any one of the rules, an alert is triggered. |
   ||Alert metrics |* Metric: Different alert types have different metrics. If you select 'composite metric' for the alert type, the metric here will require a complex configuration, and the calculation rules for the composite metric must be configured separately.<br><br>* Filter conditions:<br><br>   * **Threshold**: An alert is triggered when the number of exceptions within a single time window reaches a certain amount.<br><br>   * **Comparison**: Refers to whether, within a single time window, the magnitude of increase or decrease, compared to the value in the same time window n time units earlier, exceeds the set value.<br><br>* **Sample size threshold**: An alert is triggered only when the reported sample size reaches a certain threshold, to prevent alerts from being unrepresentative due to an insufficient number of samples.<br><br>* **User count threshold**: An alert is triggered only when the reported number of users reaches a specified threshold, preventing alerts from being triggered when the user count is too low and not representative.<br><br>* **Grouping**: Currently, only single\-dimension grouping is supported. If any item within a dimension meets the alert condition, an alert is triggered. For example, if you select regions as a group and the regions include China, Singapore, and the United States, an alert will be reported as long as any one of these regions meets the alert condition.<br><br>* **Attribution dimension**: Provides a default attribution dimension for intelligent attribution of alerts. After configuration, when the dimension and filter items are the same, you can view the top 3 results for that dimension in the alert history with one click. |
   ||Alert activation time |The effective time is set to all day by default, from 00:00 to 23:59. If the selected metric fluctuates significantly within a day and alert thresholds vary across different time ranges, you can avoid excessive interference by setting the alert effective time. |
   ||Alert optimization |* Spike filtering: Reduce false alarms and improve the accuracy of alerts.<br><br>   Spikes are alerts triggered by fluctuations in the service level metric (SLI) due to random factors. Over a long period, these alerts do not affect the SLI and do not warrant any action.<br><br>   Which alerts are considered spikes?<br><br>   * Scenario A: The **budget consumption ratio** for 30 minutes exceeds 1% of the total 14\-day budget<br><br>   * Scenario B1: 5\-hour SLI exceeds SLO<br><br>   * Scenario B2: The SLI for the last 10 minutes exceeds the SLO<br><br>      The scenario where a spike alert eventually occurs: A<br><br>* PCT alert: An alert is triggered only when the number of alert sub\-windows reaches the threshold.<br><br>   For example, if the error count within X minutes exceeds threshold Y, an alert is triggered.<br><br>   After turning on the PCT alert, each minute is considered a sub\-window. The error count for each minute is checked, and if the error count in more than Y/X minutes exceeds Y/X, an alert is triggered.<br><br><br>For more information about concepts, refer to [glossary](https://docs.byteplus.com/en/docs/apmplus/alert_management_webpro#9813940d). |
   |Configure the notification audience |alert method |Supports alerts via **Lark**, **email**, **WeCom**, **DingTalk**, and **alert callback**. |
   ||Lark webhook |Enter the Lark webhook. When the alert method is set to **Lark**, this field is required.<br><br>For details on webhook configuration, see [How to configure a webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   ||People to mention in Lark |Lark users for whom alert notifications are configured based on User ID or Open ID. When **Lark** is selected as the alert method, this field is optional.<br><br>For methods to obtain User ID and Open ID, refer to [How to obtain User ID, Open ID, and Union ID](https://open.feishu.cn/document/home/user-identity-introduction/open-id).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The individual to receive the notification must be in the same group as the group bot.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Please ensure that the User ID and Open ID are correct; otherwise, the notification cannot be pushed to the user.</div><br> |
   ||Email notification group |Configure email notification recipient groups. When you select **Email** as the alert method, this field is required. |
   ||WeCom webhook |Enter the WeCom webhook. When the alert method **WeCom** is selected, this field is required.<br><br>For details on webhook configuration, see [How to configure webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   ||People to @\-mention in WeCom |WeCom users who are configured to receive alert notifications according to their mobile phone number or User ID. When the alert method **WeCom** is selected, this field is optional.<br><br>For the method to obtain the User ID, refer to [User ID](https://developer.work.weixin.qq.com/document/path/98728#.5piO5paHdXNlcmlk).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The individual to receive the notification must be in the same group as the group bot.</div><br> |
   ||DingTalk webhook |Enter a DingTalk webhook. When the alert method **DingTalk** is selected, this field is required.<br><br>For details on webhook configuration, see [How to configure a webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   ||People to @\-mention in DingTalk |DingTalk users whose alert notifications are configured based on mobile phone number or User ID. When you select **DingTalk** as the alert method, this field is optional.<br><br>For the method to obtain the User ID, refer to [User ID](https://open.dingtalk.com/document/orgapp/basic-concepts#title-o8w-yj2-t8x).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Individuals to be notified must be in the same group as the group bot.</div><br> |
   ||Alert callback webhook |Enter alert callback webhook. When the alert method **alert callback** is selected, this field is required. |
   


<span id="f65bba0e"></span>
### Result validation.

After the alert task has been created, view alert information on each notification platform. The following is an example of alert information from the Lark webhook.


|alert strategy |Alert information |
|---|---|
|Single policy, no grouping, no attribution |Links are included in the result description, pointing to all errors that caused the alert. |
|Single policy, with grouping, no attribution |Each group has a corresponding link, which points to that group. |
|Single policy, no grouping, with attribution |Each attribution result is accompanied by a corresponding link, which points to the respective attribution result. |
|Multiple policies, with grouping and attribution |For each group and each attribution result in a policy that triggers an alert, a corresponding link is provided. |


<span id="1a82c866"></span>
### Back to alerts

<span id="03a79b46"></span>
#### **request body field**

The request body contains callback information in JSON format. The specific fields are as follows:


|**Field** |**Type** |**Sample value** |**DescriptionS** |
|---|---|---|---|
|title |string |APMPlus alerts |The name of the alert task. |
|content |object |\- |The content of the callback after the alert task is triggered.<br><br><br>* 1. No returned content.<br><br>* There is returned content. For details, refer to **content data structure**. |


<span id="04c1bf7f"></span>
#### **Content data structure**


|**Field** |**Type** |**Sample value** |**DescriptionS** |
|---|---|---|---|
|alarm_param |object |\- |Parameters configured in the alert task. For details, refer to **alarm_param data structure**. |
|alarm_result |object |\- |Alert response result For details, refer to **alarm_result data structure**. |


<span id="5b93d538"></span>
#### **The alarm_param data structure**


|**Field** |**Type** |**Sample value** |**DescriptionS** |
|---|---|---|---|
|aid |string |`123456` |Application ID. |
|alarm_level |string |`warning` |Alert level.<br><br><br>* warning<br><br>* fatal: Severe |
|alarm_period |array |\- |The effective time of the alert. Alerts outside this time range do not trigger notification. |
|category |string |\- |Alert categories. |
|category_label |string |\- |Alert category tags. |
|desc |string |\- |Alert descriptions |
|id |int |`766` |Alert Task ID. |
|interval_seconds |string |`300` |Alert task execution interval.<br><br><br>* 300 in 5 minutes<br><br>* 600: 10 minutes<br><br>* 1800: 30 minutes<br><br>* 3600: 60 minutes |
|is_avoid_spike |boolean |`false` |Alert optimization: Whether to filter spike alerts. |
|is_close |int |`0` |Turn off the alert?<br><br><br>* 0: Turn on<br><br>* 1. Turn off |
|name |string |`Webpro alert callback` |The name of the alert task. |
|notify_config |array |\- |Notification configuration for alert tasks. |
|os |string |`webpro` |Types of services. |
|site_type |string |\- |Types of web sites. |
|strategy_list |array |\- |Alert strategies list |
|strategy_op |string |`and` |Relationships between alerts and policies.<br><br><br>* and: All policies must be satisfied at the same time<br><br>* or: Satisfy any policy |


<span id="0ae8f710"></span>
#### **The alarm_result data structure**


|**Field** |**Type** |**Sample value** |**DescriptionS** |
|---|---|---|---|
|group_result_list |array |\- |List of returned alerts.<br><br>For details, refer to **the group_result_list data structure**. |
|is_alarm |boolean |`true` |Whether the alert was triggered by an alert task. |
|is_attributable |boolean |`false` |Attribution status. |
|title |string |`Page view threshold alert` |Alert return title. |


<span id="d92f3142"></span>
#### group_result_list**data structure**


|**Field** |**Type** |**Sample value** |**DescriptionS** |
|---|---|---|---|
|alarm_tag_list |array |`[{`<br><br>`"format_value":"4290",`<br><br>`"label":"Current value",`<br><br>`"value":4290`<br><br>`}]` |Alert value acquisition. |
|alarm_value |object |\- |Alert metrics and possible values Different alert types have different alert values, such as threshold, current value, sample size, number of users, time window, and so on. |
|attribution_results |object |\- |Attribution results. |
|group_value |string |\- |Grouping results. |
|is_alarm |boolean |`true` |Whether to trigger an alert. |
|is_spike |boolean |`false` |Suppress spikes? The default is false. The value is true when alert optimization or spike filtering is turned on and a spike occurs. |


<span id=".5oql6K2m5Lu75Yqh5YiX6KGo"></span>
## **The alert task list**

The alert task list displays added alert tasks, including the task name, creator, alert level, alert method, alert rule abstract, metric type, most recent update time, alert count in the past month, and monitoring status.


* You can quickly view detailed information about the alert task by clicking the task name in the task details.

* In the **Actions** column, click **Edit** to reconfigure this alert task.

* In the **Actions** column, click **alert detail** to view the alert detail for this alert.


<span id=".5oql6K2m6K-m5oOF"></span>
## **alert detail**

The alert detail page displays the alert overview and the alert list.


* The alert detail page supports setting alert ACK, and the effective time of ACK depends on the alert ACK setting in the project setting.

* **Alert overview** displays a trend chart of alert situations within the selected time range.

* **Alert list** displays alert content, alert time, alert details, alert method, and creator. Click **alert detail** to navigate to **data explore**, where you can view detailed data for **Requests**.
