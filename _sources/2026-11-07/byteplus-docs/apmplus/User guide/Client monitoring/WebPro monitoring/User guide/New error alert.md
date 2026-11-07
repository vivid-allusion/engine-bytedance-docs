---
title: "New error alert"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/new_error_alert"
---

This page is used to monitor newly added errors and alert, helping you pay attention to and view newly added errors in different versions.

<span id=".5paw5bu65oql6K2m5Lu75Yqh"></span>
## Create an alert task

<span id="d2b6df5d"></span>
### Operation Procedure


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. Click **Webpro client monitoring** under the target application.

3. In the upper left corner of the console, select **All features \> New error alert**.

4. On the error alert creation page, click **create alert task**.

   Parameter description:

   
   |**Configuration area** |**Parameters** |**DescriptionS** |
   |---|---|---|
   |Basic alert information |Alert task name |Custom name used to identify alert tasks. |
   ||alert level |Supports the Warning and Fatal levels.<br><br><br>* **Warning**: Warning<br><br>* **Fatal**: Severe |
   ||Alert description |Description of the purpose of this alert task, as well as the handling plan or other information after an alert occurs. |
   |Create alert strategies |Alert type |The supported alert types are: **JavaScript error**, **static resource error**, and **request error**. |
   ||alert strategy |* The version where the alert strategy takes effect.<br><br>   * **Latest version**: When the latest version is selected, if an error occurs for the first time, an alert is triggered.<br><br>      Example scenario: The historical version is 1.0, and the latest version is 2.0. There is a known error in historical version 1.0.<br><br>      If the policy configuration is set to the latest version, this known error will not trigger an alert.<br><br>   * **Specified version**: Select the specified version. If an error occurs for the first time in the specified version, trigger an alert.<br><br>      Example scenario: The historical version is 1.0, and the latest version is 2.0. There is a known error in historical version 1.0.<br><br>      If the specified version includes 2.0 and does not include 1.0, this known error will trigger an alert.<br><br>   * **All versions**: When you select All versions, you need to configure the system to trigger an alert if an error first appears within a specified number of days.<br><br>      Example scenario: The previous version is 1.0, and the latest version is 2.0. There is a known error in historical version 1.0.<br><br>      If the policy configuration is set to trigger an alert only when an error appears for the first time within seven days across all versions, then this known error will not trigger an alert.<br><br>* Filter criteria: Add filter criteria.<br><br>* **Sample size threshold**: An alert is triggered only when the reported sample size reaches a certain threshold, to avoid alerts that are not representative due to insufficient samples.<br><br>* **User threshold**: An alert is triggered only when the reported number of users reaches a specified threshold, preventing alerts from being triggered when the user count is too low and not representative. |
   |Configure the notification audience |alert method |Alerting is supported via **Lark**, **email**, **WeCom**, **DingTalk**, and **alert callback**. |
   ||Lark webhook |Enter Lark webhook. When **Lark** is selected as the alert method, this field is required.<br><br>For details on webhook configuration, see [How to configure a webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   ||The people to @ in Lark |Lark users configured to receive alert notifications based on User ID or Open ID. When you select **Lark** as the alert method, this field is optional.<br><br>For methods to obtain User ID and Open ID, refer to [How to obtain User ID, Open ID, and Union ID](https://open.feishu.cn/document/home/user-identity-introduction/open-id).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The individual to receive the notification must be in the same group as the group bot.</div><br><br><br><div data-tips="true" data-tips-type="warning">Please ensure that the User ID and Open ID are correct; otherwise, the notification cannot be pushed to the user.</div><br> |
   ||Email notification groups |Configure the recipient group for email notification. When the alert method **email** is selected, this field is required. |
   ||WeCom webhook |Enter WeCom webhook. When the alert method is set to **WeCom**, this field is required.<br><br>For details on webhook configuration, see [How to configure a webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   ||People to @\-mention in WeCom |WeCom users whose alert notifications are configured by mobile phone number or User ID. When the alert method is set to **WeCom**, this field is optional.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The individual to receive the notification must be in the same group as the group bot.</div><br> |
   ||DingTalk webhook |Enter DingTalk webhook. When you select **DingTalk** as the alert method, this field is required.<br><br>For details on webhook configuration, see [How to configure a webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
   ||People to @\-mention in DingTalk |DingTalk users for whom alert notification configuration is based on phone number or User ID. When the alert method is selected as **DingTalk**, this field is optional.<br><br>For information on how to obtain the User ID, refer to [User ID](https://open.dingtalk.com/document/orgapp/basic-concepts#title-o8w-yj2-t8x).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The notification recipient must be in the same group as the group bot.</div><br> |
   ||Alert callback webhook |Enter the alert callback webhook. When the alert method **alert callback** is selected, this field is required. |
   


<span id="03256e7b"></span>
### Result validation.

After the alert task is created, view alert information on each notification platform. The following is an example alert from the Lark webhook.

<span id="30ddafb9"></span>
### Alert back

<span id="443aed95"></span>
#### **request body field**

The request body contains callback information in JSON format. The specific fields are:


|**Field** |**Type** |**Sample value** |**DescriptionS** |
|---|---|---|---|
|title |string |APMPlus alert |The name of the new error alert task. |
|content |object |\- |The content of the callback after the new error alert task is triggered.<br><br><br>* No content is returned.<br><br>* Returned content is available. For details, refer to **the content data structure**. |


<span id="7591fef8"></span>
#### **The content data structure**


|**Field** |**Type** |**Sample value** |**DescriptionS** |
|---|---|---|---|
|alert_param |object |\- |Parameters configured in the new error alert task. For details, refer to **alert_param data structure**. |
|alert_result |object |\- |The response result of adding a new error alert. For details, refer to **alert_result data structure**. |
|aid |int |`123456` |App ID。 |


<span id="f3c1b247"></span>
#### **The alert_param data structure**


|**Field** |**Type** |**Sample value** |**DescriptionS** |
|---|---|---|---|
|alert_language |string |`zh` |The language for the new error alert. |
|alarm_level |string |`warning` |The level of new error alert.<br><br><br>* warning<br><br>* fatal: indicates a severe error |
|alert_strategy |object |\- |The policy for new error alerts. |
|callback_urls |array |\- |Alert callback for the configuration of the alert task for newly added errors. |
|dingding_at_conf |object |\- |DingTalk account information for the new error alert task configuration. |
|dingding_webhooks |array |\- |DingTalk webhook address for configuring new error alert tasks. |
|feedback_duty_name |string |\- |Back to task name. |
|id |int |`766` |New error alert ID. |
|is_close |boolean |`false` |Do you want to turn off the alert?<br><br><br>* true: turn on<br><br>* false: turn off |
|lark_at_conf |object |\- |Lark account information for the configuration of newly added error alert tasks. |
|lark_webhooks |array |\- |Lark webhook address for the configuration of the new error alert task. |
|mail_groups |array |\- |Email notification group for configuring a new error alert task. |
|methods |array |\- |Notification methods for new error alerts.<br><br><br>* callback_url: alert callback<br><br>* we_chat_webhook: WeCom<br><br>* dingding_webhook: DingTalk<br><br>* lark_webhook: Lark<br><br>* mail_group: Mail |
|name |array |`\u8c03` |Alert strategy list. |
|note |string |\- |Relationships between alerts and multiple policies<br><br><br>* and: All policies must be satisfied simultaneously<br><br>* or: Meet any policy |
|we_chat_webhooks |array |\- |WeCom webhook address for configuring new error alert tasks. |
|wechat_at_conf |array |\- |WeCom account information configured for newly added error alert tasks |


<span id="a5f8c92a"></span>
#### **The alert_result data structure**


|**Field** |**Type** |**Sample value** |**DescriptionS** |
|---|---|---|---|
|detail_link |string |`https://console.bytedance.net/apmplus/webpro/data_search?aid=123456&end_time=1693309723&ev_type=js_error&filter_id=xxx&start_time=1693309123` |Link to the new error alert Click the link to go to the alert information page for this newly added error in the console. |
|details |object |\- |Detailed information about newly added error alerts. |
|history_link |string |`https://console.bytedance.net/apmplus/webpro/alarm_new_error/detail?aid=123456&rule_id=xxx&rule_name=xxx&status=true&time=xxx` |The link to historical error alerts. |
|sample_count |int |`1` |Sample size. |
|strategy |string |`JS\u9519\u8bef` |The category of new error alert. |
|user_count |int |`1` |Number of users. |


<span id=".6ZSZ6K-v5paw5aKe5oql6K2m5YiX6KGo"></span>
### Newly added error alert list

The new error alert list displays alert tasks for detecting new errors, including task name, creator, alert level, alert method, alert rule abstract, most recent update time, alert count in the past month, and monitoring status.


* Click the task name to quickly add filter criteria in the task details.

* In the **alert rule abstract** column, you can view the version number of the specified version.

* In the **Actions** column, click **edit** to reconfigure the new error alert task.

* In the **Actions** column, click **alert detail** to view the request error details for the new alert generated for this error.


<span id=".6K-35rGC6ZSZ6K-v6K-m5oOF"></span>
## Request error details

The request error details page displays an alert overview and an alert history list.


* **Alert status overview**: Displays a trend chart of alerts for the selected time range.

* **Alert list**: Displays historical alert content, alert time, alert detail, alert method, and creator.

* **alert detail**: Click to navigate to **data explore.** 

   * JavaScript error alert: You can view detailed data for this issue_id in **JS Errors**.

   * Static resource error alert: You can view the detailed data for this issue_id in **Resource Errors**.

   * Request error alert: You can view detailed data for this request path and request status code in **Requests**.
