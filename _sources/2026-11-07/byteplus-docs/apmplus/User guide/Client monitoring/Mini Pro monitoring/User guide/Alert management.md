---
title: "Alert management"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/alert_management_minipro"
---

Alert tasks configure alert strategies across multiple dimensions, including user analysis, performance metrics, JavaScript error metrics, request metrics, composite metrics, and more. Flexible and complex custom configuration rules are also supported, helping you monitor the health status of your application.

<span id=".5paw5bu65oql6K2m5Lu75Yqh"></span>
## Create an alert task

<span id="8a03b499"></span>
### Glossary


|Glossary |DescriptionS |
|---|---|
|SLA |Service Level Agreement (SLA). |
|SLO |Service Level Objectives (Service Level Objectives). In alert tasks, SLO refers to the threshold set in alert metric configuration. |
|SLI |Service level indicators (Service Level Indicators). In alert tasks, SLI refers to the actual statistical value of the alert metric. |
|Budgets |* Budget calculation method for numerical metrics:<br><br>   For example, if the error count in alerts over a 10\-minute period exceeds 10, the daily budget is set to 10.*6*24。<br><br>* Budget calculation method for rate\-type metrics:<br><br>   For example, if the alert error rate exceeds 1% over a 10\-minute period, the daily budget is set based on the average error rate for one day, which is 1%. |
|Budget consumption ratio |* Calculation method for the budget consumption ratio of numeric metrics:<br><br>   For example, if the alert error count exceeds 10 in 10 minutes, and the error count is 50 in 30 minutes, the proportion of budget consumed is 50/(10*6*24)。<br><br>* Method for calculating the budget consumption ratio of rate\-type metrics:<br><br>   For example, if the error rate exceeds 1% for 10 minutes and reaches 2% for 30 minutes, the proportion of budget consumed is 30*2/(24*60\*1). |
|Spike |Alerts triggered by SLI fluctuations caused by certain accidental factors. |


<span id="9c0894d1"></span>
### Operation Procedure


1. Log in to [the Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. Click **Mini Program Pro Monitoring** under the target application.

3. In the upper left corner of the console, select **All features \> alert management**.

4. On the alert task page, click **Create alert task**.

   Parameter description

   
   |**Configuration area** |**Parameter** |**DescriptionS** |
   |---|---|---|
   |Alert basic information |Alert task name |Custom name, used to identify alert tasks. |
   ||alert level |Supports the Warning and Fatal levels.<br><br><br>* **Warning**: Warning<br><br>* **Fatal**: Serious |
   ||Mini Program type |Select a mini program type<br><br><br>* **TikTok Mini Program**<br><br>* **WeChat Mini Program**<br><br>* **Alipay Mini Program**<br><br>* **Baidu Mini Program**<br><br>* **Lark mini program** |
   ||Alert description |Description of the purpose of the alert task, as well as the handling plan or other relevant information after an alert occurs. |
   |Create an alert strategy |Alert type |Different alert types correspond to different alert metrics.<br><br>Supported alert types: **user analysis**, **performance metric**, **JavaScript error metric**, **request metric**, **event metric**, **composite metric**, **custom log**. |
   ||Task execution interval |The task execution interval refers to the frequency at which the backend polling service operates. For example, if the interval is set to 5 minutes in the configuration, the service will check every 5 minutes whether the metric values within a recent period meet the alert threshold.<br><br>Supports **5 minutes**, **10 minutes**, **30 minutes**, and **60 minutes**. |
   ||Multiple policy relationships |When configuring multiple policy relationships, you can configure the relationships between policies.<br><br><br>* **All of the following rules must be met simultaneously**: An alert is triggered only when multiple alert strategies reach their thresholds at the same time.<br><br>* **Meet any of the following rules**: An alert is triggered if any alert strategy reaches its threshold. |
   ||Alert metrics |* Metrics: Different alert types have different metrics. If you select composite metrics as the alert type, the metrics here will require a complex configuration, and the calculation rules for composite metrics must be configured separately.<br><br>* Filter criteria:<br><br>   * **Threshold**: When the number of exceptions within a single time window reaches a specified amount, an alert is triggered.<br><br>   * **Ratio**: Refers to whether the magnitude of increase or decrease in value within a single time window, compared to the value in the same time window n time units earlier, exceeds the specified setting.<br><br>* **Sample size threshold**: An alert is triggered only when the reported sample size reaches a specified quantity, to prevent alerts from being generated when the sample size is too small and therefore not representative.<br><br>* **User count threshold**: An alert is triggered only when the reported number of users reaches a specified threshold, preventing alerts from being triggered when the user count is too low and not representative.<br><br>* **Grouping**: Currently, only single\-dimension grouping is supported. If any item within a dimension meets the alert condition, an alert is triggered. For example, when selecting regions by group, including China, Singapore, and the United States, an alert will be reported as long as any one of China, Singapore, or the United States meets the alert condition.<br><br>* **Attribution dimensions**: Provides default attribution dimensions and intelligently attributes alerts. When the dimension and filter items are the same, after configuration, you can view the top 3 records for that dimension with one click in the alert history. |
   ||Alert activation time |The effective time defaults to the entire day, from 00:00 to 23:59. If the selected metric fluctuates significantly within a day and alert thresholds vary across different time ranges, you can avoid excessive interference by setting the alert effective time. |
   ||Alert optimization |* Spike filtering: Reduce false alarms and improve alert accuracy.<br><br>   Spikes are alerts triggered by occasional fluctuations in the service level indicator (SLI) metric. Over a long period, these do not affect the SLI and are not worth handling.<br><br>   Which alerts are considered spikes?<br><br>   * Scenario A: The **budget consumption ratio** for 30 minutes exceeds 1% of the total 14\-day budget.<br><br>   * Scenario B1: The SLI for the past 5 hours exceeds the SLO<br><br>   * Scenario B2: The SLI for the last 10 minutes exceeds the SLO<br><br>      Scenario in which a spike alert eventually occurs: A<br><br>* PCT alert: An alert is triggered only when the number of alert sub\-windows reaches the threshold.<br><br>   For example, if the error count within X minutes exceeds threshold Y, an alert is triggered.<br><br>   After turning on the PCT alert, each minute is treated as a sub\-window. The error count is checked for each minute, and if the number of minutes with an error count exceeding Y/X surpasses a threshold, an alert is triggered.<br><br><br>For more information about concepts, refer to [glossary](https://docs.byteplus.com/en/docs/apmplus/alert_management_minipro#8a03b499). |
   |Configure notification audience |alert method |Supports alerting via **Lark**, **email**, **WeCom**, **DingTalk**, and **alert callback**. |
   ||Lark webhook |Enter a Lark webhook. When the alert method is set to **Lark**, this field is required.<br><br>For details on webhook configuration, see [How to configure webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   ||People who need to be @\-mentioned in Lark |Lark users for whom alert notification configuration is based on User ID or Open ID. When the alert method **Lark** is selected, this field is optional.<br><br>To obtain User ID and Open ID, refer to [How to obtain User ID, Open ID, and Union ID](https://open.feishu.cn/document/home/user-identity-introduction/open-id).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The notification recipient must be in the same group as the group bot.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Please ensure that the User ID and Open ID are correct; otherwise, the notification cannot be pushed to the user.</div><br> |
   ||Notification group |Configure email notification recipient groups. When the alert method is set to **Email**, this field is required. |
   ||WeCom webhook |Enter a WeCom webhook. When the alert method is set to **WeCom**, this field is required.<br><br>For detailed webhook configuration, see [How to configure a webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   ||People to @\-mention in WeCom |WeCom users for whom alert notification configuration is based on mobile phone number or User ID. This field is optional when the alert method **WeCom** is selected.<br><br>For information on obtaining the User ID, refer to [User ID](https://developer.work.weixin.qq.com/document/path/98728#.5piO5paHdXNlcmlk).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The individual to receive the notification and the group bot must be in the same group.</div><br> |
   ||DingTalk webhook |Enter DingTalk webhook. When the alert method is set to **DingTalk**, this field is required.<br><br>For details on webhook configuration, see [How to configure a webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   ||People to @\-mention in DingTalk |DingTalk users for whom alert notification configuration is based on phone number or User ID. When the alert method is set to **DingTalk**, this field is optional.<br><br>For information on how to obtain the User ID, refer to [User ID](https://open.dingtalk.com/document/orgapp/basic-concepts#title-o8w-yj2-t8x).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The individual to receive the notification must be in the same group as the group bot.</div><br> |
   ||Alert callback webhook |Enter alert callback webhook. When the alert method is set to **alert callback**, this field is required. |
   


<span id="27a4e139"></span>
### Back to alert

<span id="30563a61"></span>
#### **request body field**

The request body contains callback information in JSON format. The specific fields are:


|**Field** |**Type** |**Sample value** |**DescriptionS** |
|---|---|---|---|
|title |string |APMPlus alert |The name of the alert task. |
|content |object |\- |Content of the callback after the alert task is triggered.<br><br><br>* 1. No returned content.<br><br>* There is returned content. For details, refer to **content data structure**. |


<span id="2415f726"></span>
#### **The content data structure**


|**Field** |**Type** |**Sample value** |**DescriptionS** |
|---|---|---|---|
|alarm_param |object |\- |Parameters configured in the alert task. For details, refer to **alarm_param data structure**. |
|alarm_result |object |\- |Alert response results. For details, refer to **alarm_result data structure**. |


<span id="42995f5d"></span>
#### **The alarm_param data structure**


|**Field** |**Type** |**Sample value** |**DescriptionS** |
|---|---|---|---|
|aid |string |`123456` |Application ID. |
|alarm_level |string |`warning` |Alert level.<br><br><br>* warning<br><br>* fatal: Severe |
|alarm_period |array |\- |Effective time of the alert Alerts outside this time range will not be notified. |
|category |string |\- |Alert categories. |
|category_label |string |\- |Alert category tags. |
|desc |string |\- |Alert description. |
|id |int |`766` |Alert task ID. |
|interval_seconds |string |`300` |The alert task execution interval.<br><br><br>* 300: 5 minutes<br><br>* 600: 10 minutes<br><br>* 1800: 30 minutes<br><br>* 3600: 60 minutes |
|is_avoid_spike |boolean |`false` |Alert optimization, should spike alerts be filtered? |
|is_close |int |`0` |Turn off the alert.<br><br><br>* 0: Turn on<br><br>* Step 1: Turn off |
|name |string |`Alert callback` |The name of the alert task. |
|notify_config |array |\- |Alert task notification configuration. |
|os |string |`minipro` |Types of services. |
|site_type |string |\- |Type of web site. |
|strategy_list |array |\- |Alert strategy list. |
|strategy_op |string |`and` |Relationships among multiple alert policies.<br><br><br>* and: Satisfy all policies simultaneously<br><br>* or: Meet any one policy |


<span id="b1b8ad88"></span>
#### **The alarm_result data structure**


|**Field** |**Type** |**Sample value** |**DescriptionS** |
|---|---|---|---|
|group_result_list |array |\- |Alert return list<br><br>For details, refer to **group_result_list data structure**. |
|is_alarm |boolean |`true` |Whether the alert was triggered by an alert task. |
|is_attributable |boolean |`false` |Attribution status. |
|title |string |`Pv threshold alert` |Alert back title. |


<span id="3e7d2aa6"></span>
#### group_result_list**data structure**


|**Field** |**Type** |**Sample value** |**DescriptionS** |
|---|---|---|---|
|alarm_tag_list |array |`[{`<br><br>`"format_value":"4290",`<br><br>`"label": "Current value",`<br><br>`"value":4290`<br><br>`}]` |Alert values. |
|alarm_value |object |\- |Alert metrics and values Different alert types have different alert values, including threshold, current value, sample size, number of users, time window, and many others. |
|attribution_results |object |\- |The attribution results. |
|group_value |string |\- |Grouping results. |
|is_alarm |boolean |`true` |Whether to trigger an alert. |
|is_spike |boolean |`false` |Filter spikes. The default value is false. The value is true when alert optimization or spike filtering is turned on and a spike occurs. |


<span id=".5oql6K2m5Lu75Yqh5YiX6KGo"></span>
## Alert task lists

The alert task list displays all added alert tasks, including task name, creator, alert level, alert method, mini program type, metric type, recent update time, alert count in the past month, and monitoring status.


* Click the task name to quickly view detailed information about the alert task in the task details.

* In the **Actions** column, click **edit** to reconfigure the alert task.

* In the **Actions** column, click **alert detail** to view the alert detail for this alert.


<span id=".5oql6K2m6K-m5oOF"></span>
## alert detail

The alert detail page displays an overview of alerts and an alert list.


* The alert detail page supports configuring alert ACK, and the ACK effective time depends on the alert ACK setting in the project setting.

* **Alert overview** displays the trend chart of alert conditions within the selected time range.

* **Alert list** displays alert content, alert time, alert details, alert method, and creator. Click **alert detail** to navigate to **data explore**, where you can view detailed data for **Requests**.
