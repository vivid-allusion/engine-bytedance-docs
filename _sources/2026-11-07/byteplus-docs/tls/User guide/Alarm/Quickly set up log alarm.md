---
title: "Quickly set up log alarm"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Quickly_set_up_log_alarm"
---

This article introduces the steps to create content templates, set up Webhook integration configurations, create notification groups, create alarm policies (including sending raw logs in alarm notifications), and view alarm records to help you quickly get started with log alarm features.

<span id="91ce48fe"></span>
## Background information

The log service provides an all\-in\-one alarm feature for real\-time monitoring and timely response to alarm events. This case sets an alarm policy based on website error logs by creating a log topic dedicated to storing website error logs. The alarm policy uses the statement `* | SELECT COUNT(*) AS total` to count the number of error logs. When the log count in this topic is greater than 0, it indicates the website has error logs, triggering the alarm condition `$1.total>0`, and promptly sending alarm notifications to the Feishu bot.

<span id="5705dc2e"></span>
## Prerequisites


* The website error logs have been collected into the log service. For detailed steps, please refer to [Collection Overview](https://docs.byteplus.com/docs/tls/data_collection_overview).

* The Feishu bot has been created. For detailed steps, please refer to [Custom Bot User Guide](https://open.feishu.cn/document/client-docs/bot-v3/add-custom-bot).


<span id="72821ca5"></span>
## Step one create content template

A content template is a predefined text template. The log service sends alarm notifications to specified notification channels according to the content defined in the template. The log service provides a default template default\-template for your convenience. This example creates a custom content template based on the default template.


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **common features** \> **log alarm** \> **notification management**.

4. On the **notification management** page, under the **content template** tab, click **create content template**.

5. Fill in the content template configuration.

   1. Set the template name, for example **Feishu content template**.

   2. Set **notification content** in the **Feishu** area.

      For detailed parameter descriptions, refer to [creating content templates](https://docs.byteplus.com/docs/tls/content_templates).

      
      |configuration |Description |Example |
      |---|---|---|
      |title |Subject of the alarm notification content. |TLS alarm |
      |content |Alarm notification content supports inserting content variables, content functions, and others. For details, please refer to [content variables](https://docs.byteplus.com/docs/tls/content_variables) and [content functions](https://docs.byteplus.com/docs/tls/content_functions). |```Plain```<br>```Dear user, hello! \nYour account (main account ID: {{AccountID}}) log service {%if NotifyType==1%}triggered an alarm{%else%}alarm recovered{%endif%}\nalarm policy: {{Alarm}}\nalarm log topic: {{AlarmTopicName}}\ntrigger time: {{StartTime}}\ntrigger condition: {{Condition}}\ncurrent query result: [{%-for x in TriggerParams-%}{{-x-}} {%-endfor-%}];\nlogin-free link: {{SignInUrl}}```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>NotifyMsg</code> variable references the <strong>notification content</strong> in the alarm policy.</div><br> |
      


<span id="3ad99857"></span>
## Step 2 create webhook integration configuration

The webhook integration configuration manages your Feishu bot webhook address.


1. On the **notification management** page, under the **webhook integration** tab, click **create webhook integration**.

2. In the **create webhook integration configuration** dialog, complete the configurations below and click **create**.

   For detailed parameter descriptions, refer to [creating webhook integration configuration](https://docs.byteplus.com/docs/6470/1218713).

   
   |Configuration |Description |Example |
   |---|---|---|
   |Name |Name of the webhook integration configuration. |Feishu webhook |
   |Type |Notification channel type, using Feishu as an example in this case. |Feishu |
   |Request address |Webhook URL for the Feishu robot. For how to obtain it, see [custom robot user guide](https://open.feishu.cn/document/client-docs/bot-v3/add-custom-bot). |https://open.feishu.cn/open\-apis/bot/v2/hook/b6\*\*0c |
   |Encryption key |Webhook encryption key. Optional. Enter the Feishu robot's signature key here only if the **security setting** for the Feishu robot is set to **signature verification**. |/ |
   


<span id="4912d10f"></span>
## Step 3 create notification group

A notification group manages alarm policy actions and notification recipients.


1. On the **notification management** page, under the **notification group** tab, click **create notification group**.

2. On the **Create Notification Group** page, complete the configuration and click **Create Notification Group**.

   For detailed parameter descriptions, please refer to [Create Notification Group](https://docs.byteplus.com/docs/tls/create_alarm_notification_groups).


<span id="083c6c78"></span>
## Step 4 create alarm policy

The alarm policy requires configuring basic information, monitoring tasks, and alarm notifications. The log service regularly analyzes logs based on the alarm policy and periodically sends alarms that meet the trigger conditions to the specified notification targets.


1. In the left navigation bar, select **Common Functions** \> **log alarm** \> **alarm policy**.

2. On the **alarm policy** page, click **Create Alarm Policy**.

3. On the **Create Alarm Policy** page, complete the following configuration.

   For detailed parameter descriptions, please refer to [Create Alarm Policy](https://docs.byteplus.com/docs/tls/create_alarm_policies).

   1. Fill in the **basic information** of the alarm policy.

      
      |Configuration |Description |Example |
      |---|---|---|
      |Alarm policy name |Name of the alarm policy. |Error log alarm |
      |Project |The project where the log topic to be monitored is located. |`test**` |
      

   2. Configure **monitoring tasks**

      
      |configuration |Description |Example |
      |---|---|---|
      |Execute task |Configuration information related to the monitoring task; the backend executes the monitoring task regularly based on this configuration.<br><br><br>1. Click **edit.** <br><br>2. Complete the following configuration in the **execution statement** dialog box.<br><br>   * **Monitoring target**: the log topic to be monitored.<br><br>   * **Query statement**: the query and analysis statement; each task regularly retrieves and analyzes data using this statement. For details on the query and analysis statements, refer to [query overview](https://docs.byteplus.com/docs/tls/Query-overview-2) and [analysis overview](https://docs.byteplus.com/docs/tls/Analysis-overview).<br><br>   * **Query time range**: the time range of data considered each time the query and analysis statement is executed. You can specify any period within 1 day before the task execution time.<br><br>3. Click **execute preview** to preview the query and analysis results of the above statements within the specified time range.<br><br>4. Click OK. |* Monitoring target: `test**`<br><br>* Query statement: `* \| SELECT COUNT(*) AS total`<br><br>* Query time range: last 15 minutes |
      |trigger condition |The log service determines whether the query and analysis results meet the trigger conditions.<br><br><br>* Trigger condition:<br><br>   * **Has data**: triggers an alarm when data exists in the query and analysis results.<br><br>   * **Has a specific number of records**: triggers an alarm when the query and analysis results contain N records.<br><br>   * **Data matched**: triggers an alarm when the query and analysis results contain data that meet the condition expression.<br><br>   * **Specific data matched**: triggers an alarm when the query and analysis results contain N pieces of data that meet the alarm expression.<br><br>* Alarm level: supports setting the alarm level to notification, warning, or critical. |**Data matched**,  **$1.total\>0**, **notification** |
      |NoData alarm |After activation, an independent no\-data alarm triggers when the result of the set operation is an empty set. |off |
      |alarm recovery |Send a recovery notification when the alarm recovers. |Enable |
      |execution cycle |Execution cycle of the monitoring task. |Execute every 10 minutes |
      

   3. Configure **alarm notifications**

      
      |Configuration |Description |Example |
      |---|---|---|
      |Alarm sending interval |The sending cycle for alarm notifications. When the alarm triggers reach the specified limit, the log service sends notifications at the defined intervals. |If the trigger condition is met for 1 monitoring cycle continuously, the sending cycle will be set to send an alarm every 30 minutes uniformly. |
      |notification group |Select the notification group you created in [Step three Create notification group](https://docs.byteplus.com/docs/6470/1218714#4912d10f). |Feishu notification group |
      |Additional notification content |Alarm notification content supports directly clicking **insert variable** to reference content variables. Refer to [content variables](https://docs.byteplus.com/docs/tls/content_variables) for supported variables.<br><br>The content entered here will only appear in the sent alarm if referenced by the `NotifyMsg` variable in the **content template** created in [step one create content template](https://docs.byteplus.com/docs/6470/1218714#72821ca5).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The default <strong>content template</strong> has fixedly added the <code>NotifyMsg</code> variable.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If using a custom content template, ensure the <code>NotifyMsg</code> variable is added.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the original log is too long or contains special characters causing alarm sending failure, add the escapejs filter for unicode encoding. Refer to <a href="https://docs.byteplus.com/docs/tls/content_variables#querylog">QueryLog</a>.</div><br> |Click the link `{{DetailUrl}}` to view execution history information.<br><br>Original log: `{{toJson(QueryLog)}}` |
      

   4. Click **Test alarm policy**

      To facilitate troubleshooting in abnormal scenarios and preview alarm notifications in advance, it is recommended to use the alarm test feature when creating alarm policies. For detailed information on the alarm test feature, refer to [alarm policy testing](https://docs.byteplus.com/docs/tls/alarm_tests).

4. Click **Create alarm policy**

   After creating the alarm policy, the policy is enabled by default. Log Service will continuously run monitoring tasks and send alarm notifications according to the alarm policy.


<span id="eaf42520"></span>
## Step five View alarm records

After the alarm policy takes effect, monitoring tasks execute periodically and record each execution status.


1. In the left navigation bar, select **Common Functions** \> **log alarm** \> **Alarm History**.

2. View alarm records on the **alarm history** page.

   For detailed instructions, see [view execution information](https://docs.byteplus.com/docs/6470/103029#.5p-l55yL5omn6KGM5L-h5oGv).
