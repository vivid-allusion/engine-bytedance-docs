---
title: "Creating alarm strategies"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/create_alarm_policies"
---

Log Service supports configuring alarm policies based on data in log topics. After activating the alarm policy, Log Service periodically analyzes the data and regularly sends alarms that meet the trigger conditions to designated contacts. This topic explains the steps to create an alarm policy.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The monitored log topic has indexing configured, and the relevant fields have statistics enabled. For detailed steps, see [Configure Index](https://docs.byteplus.com/docs/tls/Configure-indexes-2).

* The IAM user has been created, with the phone number and email address configured in personal information and verified through both phone and email. 

* The notification group has been created. For detailed steps, see [Create Alarm Group](https://docs.byteplus.com/docs/tls/create_alarm_notification_groups).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Note


* By default, up to 10 alarm policies can be created per log topic. By default, up to 100 alarm policies can be created per log project. To increase the quota, make changes in the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ServiceCode=TLS). For specific operations, see [Apply for Resource Quota](https://docs.byteplus.com/en/docs/tls/Apply_for_resource_quota).

* If the alarm policy is modified, the **execution cycle** and **alarm sending cycle** will restart timing.

* After creating an alarm policy, the policy is enabled by default. The log service continuously runs monitoring tasks and sends alarm notifications according to the policy.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the target log project is located.

3. In the left navigation bar, select **Common Features** \> **Log Alarm** \> **Alarm Policy**.

4. On the **Alarm Policy** page, click **Create Alarm Policy**.

5. Fill in the **basic information** of the alarm policy.

   
   |Configuration |Description |
   |---|---|
   |Alarm policy name |Name of the alarm policy. |
   |project |The project that contains the log topic to be monitored. |
   

6. Configure the **monitoring task**.

   
   |configuration |Description |
   |---|---|
   |execute task |Configuration information related to the monitoring task. The system executes the monitoring task regularly based on this configuration.<br><br><br>1. Click **Edit.** <br><br>2. In the **Execute Statement** dialog, complete the following configuration.<br><br>   * **Monitoring target**: The log topic to be monitored.<br><br>   * **Query time range**: The time range of the data when each query and analysis statement executes. You can specify any period within 1 day before the task execution time.<br><br>   * **Query statement**: The query and analysis statement. Each task regularly performs retrieval and analysis using this statement. For details on query and analysis statements, please refer to [Query Overview](https://docs.byteplus.com/docs/tls/Query-overview-2) and [Analysis Overview](https://docs.byteplus.com/docs/tls/Analysis-overview).<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When setting <strong>query statements</strong> as query\-only, subsequent <strong>trigger conditions</strong> must be set to <strong>data exists</strong> or <strong>specific data exists</strong>.      </div><br>      <br><br>3. Click **Preview Execution** to preview the query and analysis results within the specified time range.<br><br>   You can use the preview function to check and debug query statements, such as verifying compliance with query and analysis syntax and obtaining expected results.<br><br>4. Click **OK.** <br><br><br>If you need to add multiple execution statements, click **Add Statement** and repeat the configuration above. Add up to 3 execution statements. |
   |set operation |The log service treats a query and analysis result as a single set and triggers an alarm based on the set results.<br><br>When configuring multiple execution statements, multi\-set correlation monitoring is supported. Supported set operations include Cartesian product, left join, right join, inner join, and full join. For details, refer to [multi-statement set operations](https://docs.byteplus.com/docs/tls/Multi-set-operations).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Supports monitoring of up to three associated sets.</div><br> |
   |Trigger condition |The log service determines whether the query and analysis set results meet the trigger conditions.<br><br><br>* **Trigger condition**:<br><br>   * **Data present**: trigger the alarm when query and analysis results contain data.<br><br>   * **Specific number of entries present**: trigger the alarm when query and analysis results contain N entries.<br><br>   * **Data match**: trigger the alarm when query and analysis results contain data that meet the condition expression.<br><br>      Support referencing query and analysis results using the expression `$N.keyname`. For expression syntax, see [alarm trigger condition expression](https://docs.byteplus.com/docs/tls/trigger_condition_expressions). For example, `$1.count>=100` means an alarm triggers when the query and analysis result count is ≥100 in the first execution statement.<br><br>      * `$N` indicates the number of the current monitoring task's execution statement.`N`For details, see [view execution statement number](https://docs.byteplus.com/docs/tls/create_alarm_policies#.5aaC5L2V5p-l55yL5omn6KGM6K-t5Y-l57yW5Y-377yf).<br><br>         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div><br>         <br><br>         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">When duplicate fields exist in results from different execution statements, the log service determines by execution statement number.         </div><br>         <br><br>      * `keyname` refers to the field name in the query and analysis results.<br><br>   * **Specific data entries match**: an alarm triggers when N entries in the query and analysis results satisfy the alarm expression.<br><br>* **Alarm level**: supports setting alarm levels to notification, warning, or critical.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When adding multiple trigger conditions, you can freely reorder them by dragging. Query and analysis results match trigger conditions one by one in order; once the results meet the first trigger condition, subsequent trigger conditions are not matched. When adding multiple trigger conditions, configure them in order from highest to lowest priority.   </div><br>    |
   |NoData alarm |When enabled, a separate no\-data alarm triggers if the set operation results in an empty set. |
   |Alarm recovery |When enabled, send a corresponding recovery notification when the alarm is restored. |
   |Execution cycle |Monitor task execution cycles with the following configuration options:<br><br><br>* Set interval: Execution cycles range from 1 to 1440 minutes, meaning the longest interval is once per day.<br><br>* Set execution time: Execute once daily at a specified time.<br><br>* Set Cron expression: Schedule alarm tasks using a Cron expression. The minimum granularity for Cron expressions is minutes, using a 24\-hour format. For example, `0 18 * * *` means the alarm task runs daily at 18:00.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">It is recommended to set the <strong>execution cycle</strong> longer than the <strong>alarm sending cycle</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Proper time configuration improves the timeliness of monitoring tasks and avoids missed or false alarms. For details, refer to <a href="https://docs.byteplus.com/en/docs/tls/Alarm_Monitoring_Task_Timeliness">alarm monitoring task timeliness</a>.</div><br> |
   

7. Configure the **alarm notification**.

   
   |Configuration |Description |
   |---|---|
   |Alarm sending cycle |The alarm notification sending interval: when the alarm continues to trigger up to the specified limit, the log service sends alarm notifications at the specified intervals. That is, after continuously meeting the trigger condition for several monitoring periods, an alarm is sent at specified intervals. Notification frequency supports unified multi\-channel settings or individual settings for each channel.<br><br><br>* Set a unified sending cycle: all channels follow the same alarm sending cycle. The sending interval can be set between 10 and 1440 minutes, with a default alarm every 30 minutes.<br><br>* Set sending cycles separately: alarm sending cycles can be set individually for phone calls, SMS, email, and custom Webhook channels. The sending cycle for phone and SMS channels can be set from 10 to 1440 minutes, while email and custom Webhook channels support a cycle from 1 to 1440 minutes.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Custom Webhooks include Feishu, WeCom, DingTalk, and other custom Webhook addresses.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The alarm frequency configuration filters out insignificant occasional cases. For example, triggering conditions must be met continuously for 5 monitoring cycles, meaning notification occurs only after 5 cumulative alarms.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Notification frequency configuration prevents frequent alarm notifications. For example, notifying once every 30 minutes means only one alarm notification is received within 30 minutes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Alarm messages via phone and SMS channels are subject to log service notification rate limits. For example, each phone number can receive a maximum of 10 alarm SMS notifications per minute. For detailed rate limits, see <a href="https://docs.byteplus.com/docs/tls/Limits#.5ZGK6K2m">Usage Restrictions</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The request rate limit for Feishu custom bots is 100 times/minute and 5 times/second per tenant per bot. An error 11232 appears when the limit is exceeded. For details, refer to the <a href="https://open.larkoffice.com/document/server-docs/api-call-guide/frequency-control">Feishu rate control policy</a>.</div><br> |
   |notification group |Specify the notification channels for alerts through the alarm notification group. The notification group is a virtual group of alarm contacts. The log service sends alarm notifications to all members in the group based on configured notification channels and message templates.<br><br>You can click **Create notification group** to create a new one, or click **Associate notification group** to add an existing group. For notification group details, refer to [Create Notification Group](https://docs.byteplus.com/docs/tls/create_alarm_notification_groups). |
   |Additional notification content |Additional content for alarm notifications enhances the details of alarm alerts.<br><br>The content entered here must be referenced through the **content template** using the `NotifyMsg` variable to appear in the sent alarm.<br><br><br>* Click **Add raw logs** to insert the raw logs of the executed query results that triggered the alarm with one click.<br><br>* Click **Insert variable** to quickly add variables. Supported content can be found in [content variables](https://docs.byteplus.com/docs/tls/content_variables) and [content functions](https://docs.byteplus.com/docs/tls/content_functions).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The default <strong>content template</strong> has the <code>NotifyMsg</code> variable fixedly added.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If using a custom content template, make sure to include the <code>NotifyMsg</code> variable.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If raw logs are too long or contain special characters causing alarm sending to fail, add an escapejs filter for unicode encoding. See <a href="https://docs.byteplus.com/docs/tls/content_variables#querylog">QueryLog</a> for details.</div><br> |
   

8. Click **Test Alarm Policy**.

   To facilitate troubleshooting in abnormal scenarios and preview alarm notifications in advance, it is recommended to debug using the alarm test function when creating an alarm policy. For detailed information about the alarm test function, please refer to [Alarm Policy Testing](https://docs.byteplus.com/docs/tls/alarm_tests).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The test function only checks whether the alarm policy configuration is correct and does not perform actual alarm monitoring tasks.   </div>
   

9. Click **Create Alarm Policy**.

   After creating an alarm policy, it is enabled by default. The log service continuously runs monitoring tasks according to the alarm policy and sends alarm notifications.


<span id=".5bi46KeB6Zeu6aKY"></span>
## Related actions

<span id=".5aaC5L2V5p-l55yL5omn6KGM6K-t5Y-l57yW5Y-377yf"></span>
### View execution statement number

When creating an alarm policy, each execution statement has a corresponding number, located in the **Monitoring Task \> Execution Task** area. The exact location is shown below.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_526a4a79de44d16976e5b3ba970746d7.png) </span>

&nbsp;
