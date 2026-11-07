---
title: "Configure Hive Custom Rules"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Configure_Hive_Custom_Rules"
---

This feature supports creating Hive custom rules using custom SQL. The following will guide you on configuring and managing rules.

<span id="a7c61ded"></span>
## Use Cases

If the monitoring templates provided by the platform cannot meet your monitoring needs in the following situations, you can create Hive custom rules using custom SQL.


* You need to convert data fields into certain metrics for monitoring through complex logic or calculation methods.

* A metric measuring consistency requires a join across multiple tables to obtain.


<span id="256b971f"></span>
## Constraints


* After all activated services expire, all quality rules will be retained, but they will be disabled and cannot be used. After repurchasing the service, you must re\-enable the rule before it can be used.


<span id="_1-前提条件"></span>
## Prerequisites

Having purchased EMR_SERVERLESS_SPARK engine services is required to use the corresponding engine features.

<span id="_2-创建规则"></span>
## Create Rules


1. Log in to the DataLeap console.

2. Select **Overview \> Quality \> Rules \> Offline Rule \> Monitoring object** to enter the monitoring object page.

3. In the upper right project's dropdown list, select the project you want to manage.

4. Click the **Hive custom rules** tab to enter the custom rules management page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/491c23dd01264a559ac9e05ed2b47926~tplv-goo7wpa0wc-image.image) </span>

5. Click the  **+ New Rule** button to enter the new custom rule page.

6. Complete the following settings in sequence:

   1. set rule parameters, then click the **next** button.

   2. set monitoring logic, then click the **next** button.

      1. enter SQL statements that comply with Hive syntax.

      2. click the **parse SQL** button to auto\-fill the field monitoring logic.

      3. modify or add SQL field monitoring settings as needed.

      4. set advanced parameters if necessary.

   3. configure alarm settings.

7. click the **create rules** button to complete rule creation.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">SQL statements support join and group by. After group by, dimension fields must be set.</div>


* <div data-tips="true" data-tips-type="tip">To improve alarm result readability, use as to abbreviate complex metric names. The monitor will execute the SQL and determine alarms.</div>


* <div data-tips="true" data-tips-type="tip">The maximum number of output rows from SQL is 200. Excess rows will be truncated. Control data volume reasonably.</div>



the following table explains the parameters related to creating custom rules. parameters marked with \* are required; those without \* are optional.


|Parameters |Description |
|---|---|
|**Rule information** ||
|\*Rule name |Monitoring rule name, auto\-filled and editable. |
|Description |Rule description. |
|**Operation settings** ||
|\*Engine |The database storage engine for creating rules supports the option EMR_SERVERLESS_SPARK, selectable from a dropdown menu.<br><br><br>* EMR_SERVERLESS_SPARK: select an instance from the dropdown list, defaulting to default. |
|\*Running method |The monitoring rule’s execution method supports three options: **RelateStudioTask**, **Regular scheduling**, and **Do not set now**.<br><br><br>* RelateStudioTask: executes according to the scheduling time of the associated data development task.<br><br>* Regular scheduling: set the execution time for monitoring rules yourself.<br><br>* Do not set now: do not execute automatically; run manually as needed. |
|\*Task name |The name of the associated task. After searching by task name keyword or task ID, select from the dropdown.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When <strong>Running method</strong> is set to <strong>RelateStudioTask</strong>, this parameter must be set.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Currently, only offline tasks with scheduling frequency at minute/hour/day/week/month levels under the current project are supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Tasks related to Sensor type are not supported yet.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Each time the task completes running (including rerun, backfill, and activated scheduling), it triggers the execution of the monitor rules.</div><br> |
|\*Strength |Provides two options: strong and weak.<br><br><br>* When **strong** is selected, set the **breaking methods**. After the associated task is completed, it will enter the strong rule execution phase. The downstream task execution depends on the breaking methods.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After task completion, it enters the strong rules operation phase, which increases task running time. Configure reasonably according to your needs.   </div><br>   <br><br>* When **weak** is selected, after the associated task completes, it will enter the weak rule execution phase. If an abnormality in the associated task quality is detected, the rule will send an alarm notification but will not block downstream task execution. |
|\*breaking methods |If it is a strong rule, the following two breaking methods can be selected:<br><br><br>* **Before the rule execution completes, the instance remains in the running state**: This means the associated task instance stays running until the quality rule finishes. If a strong rule alarm triggers during this period, the instance status changes to failed, blocking downstream tasks; if no alarm triggers, the instance is marked successful and downstream tasks are triggered.<br><br>* **If the rule runs longer than X minutes without completion, the instance is set directly to successful**: This means if the quality rule exceeds the set time, the associated task instance status changes directly to successful, though the rule continues running and can still trigger alarms. At this point, downstream tasks are still triggered but may face data quality contamination risks, so monitoring results should be checked promptly. The timeout period can be set by the user, ranging from 0 to 200. |
|\*execution frequency |The task monitoring rule execution frequency offers three options: minute\-level, hourly\-level, and daily\-level.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Set this parameter when <strong>running method</strong> is set to <strong>regular scheduling</strong>.</div><br> |
|\*Execution time |Set the specific execution time according to the execution frequency.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Set this parameter when <strong>running method</strong> is set to <strong>regular scheduling</strong>.</div><br> |
|\*Queue |The queue used by the rule supports two options: use the default queue or specify a queue manually.<br><br><br>* Use the default queue: use the system's default engine queue without manual selection.<br><br>* Specify the queue manually: select an engine queue from the dropdown, which lists queues bound to the current project. If you have not applied for queue, please go to the corresponding console to apply.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only queues supporting batch task execution are displayed.   </div><br>    |
|**Rule logic** ||
|\*Custom SQL |SQL statements conforming to Hive syntax, supporting join and group by. Set dimension fields after group by. |
|\*Field Name |SQL field name. Automatically filled after parsing the SQL statement and editable. |
|\*Field Type |Supports two options: dimension and metric. After parsing the SQL statement, it auto\-fills and can be edited.<br><br><br>* dimension: after a rule alarm, dimension information is reported to help users analyze the alarm content. Example: for dimension app=toutiao, the metric DAU triggers an alarm. Users can set multiple dimensions.<br><br>* metric: the specific monitored metric that requires setting alarm conditions. multiple metrics are independent; if any meets the alarm conditions, it triggers a rule alarm.<br><br><br>currently, custom SQL mainly supports the following monitoring scenarios:<br><br><br>* when all fields’ **field type** are set to **metrics**, multi\-metric monitoring (single row, multiple columns) is possible. for example, monitoring DAU, MAU, and average online duration per user for a product line.<br><br>* when at least one field’s **field type** is set to **dimension**, multi\-metric and multi\-dimension monitoring (multiple rows and columns) is possible. For example, monitoring indicators such as DAU, MAU, and average online duration across multiple product lines; once an alarm is triggered, it identifies which product line and which indicator caused it.<br><br>   1. Monitoring configuration example:<br><br>      * Custom SQL statement: `SELECT APP,DAU,MAU from databases.table group by APP;`<br><br>      * Set **APP** as **dimension**, **DAU** and **MAU** as **metrics**, and define monitoring thresholds for the metrics.<br><br>   2. An alarm is triggered when actual results do not meet monitoring expectations; example alarm messages are as follows:<br><br>      * APP=toutiao, metric DAU is XXX, alarm triggered.<br><br>      * APP=douyin, metric MAU is XXX, alarm triggered.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If set to monitor only <strong>metrics</strong>, it allows only single\-row monitoring, meaning it monitors only the first row detected by the input custom SQL statement. To monitor multiple rows, you must set at least one <strong>dimension</strong> field.</div><br> |
|\*Alarm conditions |After parsing the SQL statement, fields are auto\-filled and can be edited.<br><br>Supports alarms for values, volatility, and more. See [Configure Hive Template Rules](https://docs.byteplus.com/docs/dataleap/Configure_Hive_Template_Rules) parameter description for details.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">One metric field can have multiple alarm conditions. The relationship between multiple alarm conditions defaults to <strong>and</strong> and can be changed to <strong>or</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The alarm relationship between multiple fields is <strong>or</strong>.</div><br> |
|**Advanced parameter settings** ||
|Rule retry conditions |Failed to run |
|Operation parameters |Configure operation parameters before the SQL statement as needed, such as "set parameter 1 =;". |
|Filter conditions |Condition statement after where, syntax follows HSQL logic. No need to input Where, for example, type='xxx'. |
|Custom alarm time |Supports setting Beijing or UTC time as needed, selectable from the dropdown. |
|**Alarm settings** ||
|\*alarm channel |Supports alarm methods including **Email + Site message** and **Webhook**. |
|\*hookUrl |Webhook request URL starting with http or https.<br><br>Select http or https from the dropdown and enter the Webhook URL. For detailed configuration instructions, refer to the **template rules** section of [Webhook Instructions](https://docs.byteplus.com/docs/dataleap/Configure_Hive_Template_Rules#2).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the <strong>alarm channel</strong> is set to <strong>Webhook</strong>, this parameter must be configured.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After setting the Webhook, notification messages will be actively pushed to the corresponding hookUrl.</div><br><br><br>   <div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c63cc9def9b438c9cdf741647a46586~tplv-goo7wpa0wc-image.image" />   </div><br>    |
|\*alarm receivers |Users who receive alarms.<br><br><br>* When **alarm channel** is set to **email + Site message**, you must select users or duty schedules to receive the alarms.<br><br>   * User: enter the user account keyword and select from the dropdown list; multiple selections are supported.<br><br>   * Duty schedule: enter the duty schedule name keyword and select from the dropdown list. After setting, alarm messages will be sent to recipients in the duty schedule. |
|* alarm sending |Number of alarm sends. You can configure the number of sends as needed. The default is 1 time. |
|\*Sending interval |Interval for alarm sending, default is 5 minutes and editable. |
|\*Do not disturb the alarm. |Option to enable or disable do not disturb for alarms.<br><br>When **On** is selected, you can set the do not disturb time period as needed. |


<span id="_3-管理规则"></span>
## Management Rules

For the created custom rules, you can perform the following management operations:


1. Log in to the DataLeap console.

2. Select **Data quality \> Rules \> Offline Rule \> Monitoring object \> Customized rules** to enter the customized rules page for the monitoring object.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/491c23dd01264a559ac9e05ed2b47926~tplv-goo7wpa0wc-image.image) </span>

3. Choose the project to manage from the project dropdown list at the top right of the page.

4. You can perform the following operations:

   * Set search criteria to find matching monitoring rules.

   * Click the **Test** button in the **Action** column of a rule, then set the test run time in the pop\-up window to start a new test run.

   * Click the **On/off** button in the **Action** column of a rule, then click the **Confirm** button in the confirmation dialog to enable or disable the rule.

   * Click the **Edit** button in the **Action** column of a rule to modify its rule information on the edit rules page.

   * Click the  **...**   **\> Delete** button in the **Action** column of a rule name , then click **Confirm** in the pop\-up dialog to delete the rule.

   * Click the  **...**   **\> Share link** button in the **Action** column of a rule name to copy the corresponding object's link.

   * Click the  **...**   **\> Last 7\-day results** button in the **Action** column of a rule name to go to the **run result** page and view the monitoring results for the last 7 days up to the current day.

   * Click the  **...**   **\> Transfer owner** button in the **Action** column of a rule name to select a new owner for the rule in the pop\-up window.

   * Select one or more rules, then click the corresponding button below the list to perform batch operations.

      * Batch enable/disable

      * Batch test run

      * Batch delete

      * Batch modify alarm receivers

      * Batch transfer owners

      * Batch modify rule strength


<span id="b3ec0bb0"></span>
## Subsequent Actions

After the rule runs, check the run result page to view the rule’s outcome, alarm status, and troubleshoot issues. Refer to [Manage Hive Customized Rules Run Results](https://docs.byteplus.com/docs/dataleap/Manage_Hive_Customized_Rules_Run_Results) for instructions on managing rule run results.
