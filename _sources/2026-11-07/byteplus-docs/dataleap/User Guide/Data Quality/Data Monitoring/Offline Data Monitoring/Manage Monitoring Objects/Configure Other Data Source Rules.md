---
title: "Configure Other Data Source Rules"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Configure_Other_Data_Source_Rules"
---

This feature allows data quality support to monitor data sources other than Hive, meeting diverse data monitoring needs across scenarios. This article introduces how to configure other data source rules.

<span id="5cd91b8c"></span>
## Constraints


* After all activated services expire, all quality rules will be retained, but they will be disabled and cannot be used. After repurchasing the service, you must re\-enable the rule before it can be used.

* Only the current project administrator or the respective owner of the table, rule, or similar can perform add, delete, or modify operations.


<span id="b0150859"></span>
## Prerequisites


* The current project has bound the Bytehouse Cloud Data Warehouse Edition engine as needed and created the corresponding data source/instance. For related operating instructions, see [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project) and [Configure a ByteHouse Cloud Data Warehouse Edition data source](https://docs.byteplus.com/docs/dataleap/69128).

* ByteHouse Enterprise Edition cluster has been created. For related operating instructions, see [Create a Cluster](https://docs.byteplus.com/en/docs/bytehouse/create-a-cluster).

* Metadata for the required data types has been collected. For related operating instructions, see [Metadata Ingestion](https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion).


<span id="3b9592fc"></span>
## Create Rules


1. Log in to the DataLeap console.

2. Select **Overview \> Quality \> Data monitoring \> Batch Data monitoring \> Monitoring object** to enter the monitoring object page.

3. In the upper right corner of the page, select the project to manage from the project dropdown list.

4. Click the **Other data sources** tab to enter the other data sources page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a62775fb2b4c4061ae6a9b12056e0988~tplv-goo7wpa0wc-image.image) </span>

5. Click the **Create Rules** button. In the pop\-up side window for creating rules, set the rule information and click the **Confirm** button to complete rule creation.


The table below explains the parameters related to monitoring rule configuration. Parameters marked with \* before the name are required; those without \* are optional.


|Parameters |Description |
|---|---|
|**Rules basic information** ||
|\*Rule name |Monitoring rule name, set by yourself. |
|\*Data source/engine type |Selected datasource/engine type, supporting **ByteHouse Enterprise Edition** and **ByteHouse Cloud Data Warehouse Edition**. Options available in dropdown. |
|\*Datasource/instance |Configure data sources/instances for the rule; select from the dropdown the created production environment instance.<br><br>You can only set this parameter after selecting **ByteHouse cloud data warehouse edition** as the **data source/engine type**. |
|\*Engine |Configure the rule engine; select from the dropdown an engine created on the ByteHouse Enterprise Edition engine side.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter can only be set after selecting <strong>Data source/engine type</strong> as <strong>ByteHouse Enterprise Edition</strong>.</div><br> |
|Description |Description of monitoring rules for subsequent management. |
|**Rule configuration** ||
|\*Template type |The selected template type supports two options: **template** and **custom**.<br><br><br>* Template: supports options like row count, duplication, null value, outlier, table fields, etc., selectable from the dropdown. For detailed descriptions of rule configuration items for each template type, refer to [Configure Hive Template Rules](https://docs.byteplus.com/docs/dataleap/Configure_Hive_Template_Rules)parameter description.<br><br>* Custom: create rules using SQL statements that match syntax specifications. |
|\*XX query statement |Query statement corresponding to the selected data source type, such as Doris query statement, input as needed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The page will display syntax prompts for the corresponding source types: ByteHouse Enterprise Edition syntax guide, and ByteHouse Cloud Data Warehouse Edition syntax guide for quick reference.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter must be set when <strong>Template type</strong> is set to <strong>Custom</strong>.</div><br> |
|**Alarm conditions** ||
|\*Field name |SQL field name. Automatically filled after parsing the SQL statement; editable.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter must be set when <strong>Template type</strong> is set to <strong>Custom</strong>.</div><br> |
|\*Field type |Supports two options: Dimension and Metric. Automatically filled after parsing the SQL statement; editable.<br><br><br>* Dimensions: after a rule alarm, dimension information is reported to help users analyze the alarm details. For example: under the dimension app=toutiao, the metric DAU triggers an alarm. Users can set multiple dimensions.<br><br>* Metric: the specific metric being monitored, requiring alarm conditions to be set. Metrics are independent; any single metric meeting the alarm condition will trigger the rule alarm.<br><br><br>Currently, custom SQL mainly supports the following monitoring scenarios:<br><br><br>* When all fields' **Field Types** are set to **Metrics**, multi\-metric monitoring (single row, multiple columns) is possible. For example, monitoring DAU, MAU, and average online time per user for a product line.<br><br>* When at least one field's **Field Type** is set to **Dimensions**, multi\-metric and multi\-dimension monitoring (multiple rows and columns) is possible. For example, monitoring DAU, MAU, and average online time per user for multiple product lines; if an alarm triggers, it indicates which product line and metric caused it.<br><br>   1. Monitoring configuration example:<br><br>      * Custom SQL statement: `SELECT APP,DAU,MAU from databases.table group by APP;`<br><br>      * Set **APP** as **Dimensions**, **DAU** and **MAU** as **Metrics**, and define monitoring thresholds for the metrics.<br><br>   2. An alarm triggers when actual results do not meet monitoring expectations. The alarm message example is as follows:<br><br>      * APP=toutiao, metric DAU is XXX, alarm triggered.<br><br>      * APP=douyin, metric MAU is XXX, alarm triggered.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When monitoring is set for <strong>Metrics</strong> only, single\-row monitoring is allowed, meaning it only monitors the first row of data detected by the input custom SQL statement. At least one <strong>Dimension</strong> field must be set to enable multi\-row monitoring.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter must be set when <strong>Template type</strong> is set to <strong>Custom</strong>.</div><br> |
|\*Alarm conditions |Automatically filled after parsing the SQL statement.<br><br>Only alarms with **numeric** types are supported, meaning defined calculated metrics themselves, such as sum(money), count(\*), etc. These metrics are directly compared to set thresholds to determine if an alarm occurs. Example:<br><br><br>1. Monitor rule: trigger alarm when the table row count exceeds 2000.<br><br>2. Alarm judgment: suppose the monitored table row count is 2500, which exceeds the set threshold (2000), triggering an alarm.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">One alarm condition can be set per field; the alarm relationship between multiple fields is <strong>Or</strong>.</div><br> |
|**Operation settings** ||
|\*Scheduling settings |Supports three options: **Task scheduling**, **Regular scheduling**, or **Do not set now**.<br><br><br>* Task scheduling: execute according to the scheduling time of the associated development task.<br><br>* Regular scheduling: set the execution time of the monitor rule manually.<br><br>* Do not set now: disables automatic scheduling; manual scheduling can be performed as needed.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>ByteHouse Cloud Data Warehouse Edition</strong> datasources must have a calculation group set before their rules can be test run. The scheduling mode <strong>Do not set now</strong> does not support calculation group settings, so this mode does not support test runs.   </div><br>    |
|\*Task |The name of the scheduling task related to data development. You can search and select by task name keyword or ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When <strong>Schedule Settings</strong> selects <strong>Task scheduling</strong>, this parameter must be set.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Currently, only offline tasks in the current project with scheduling frequencies of minute/hour/day/week/month are supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Each time this task finishes running (including reruns, backfills, and active scheduling), it triggers rule execution monitoring.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When <strong>Datasource/Engine type</strong> is <strong>ByteHouse Cloud Data Warehouse Edition</strong>, the run results vary for different task types.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the associated task is a <strong>non\-ByteHouse Cloud Data Warehouse Edition</strong> type, the <strong>run results</strong> page still shows the datasource name and production environment identifier configured in the rule.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the associated task is a <strong>ByteHouse Cloud Data Warehouse Edition</strong> type, the <strong>run results</strong> page shows the actual running datasource name and environment identifier.</div><br> |
|\*Strength |Provides two configuration options: strong and weak.<br><br><br>* When **strong** is selected, the **breaking method** must be set. After the related task completes, the process enters the strong rule execution phase, where the breaking method determines the downstream task operation.<br><br>* When **weak** is selected, after the related task completes, the process enters the weak rule execution phase. If it detects an issue with the related task’s quality, an alarm notification is sent, but downstream tasks continue running without blockage.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When <strong>Schedule Settings</strong> selects <strong>Task scheduling</strong>, this parameter must be set.</div><br> |
|\*calculation group |Computing resource cluster in ByteHouse. Select from the calculation groups created in the **ByteHouse Cloud Data Warehouse Edition Console** via dropdown.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only calculation groups that <strong>have auto start/stop enabled</strong> or are <strong>currently enabled</strong> can be selected.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter must be set when all of the following conditions are met:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Select <strong>Datasource type</strong> <strong>ByteHouse Cloud Data Warehouse Edition</strong></div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Select <strong>Schedule Settings</strong> <strong>Task scheduling</strong> or <strong>Regular scheduling</strong></div><br> |
|\*Breaking methods |If using strong rules, choose one of the following breaking methods:<br><br><br>* **The Dorado instance will remain running until the running of the rule ends**: This means the associated task instance remains running until the quality rule finishes. If a strong rule alert triggers during this period, the associated task instance status changes to failed, blocking downstream tasks. If no alert triggers, the associated task instance is marked successful and triggers downstream tasks.<br><br>* **If the rule runs longer than x minutes without finishing, directly set the Dorado instance as succeeded**: This means if the quality rule exceeds the set time, the associated task instance status is directly set to successful while the rule continues running and can still trigger alerts. At this point, downstream tasks continue to run but data quality risk may exist, requiring prompt monitoring. The timeout period can be set freely within the range of 0 to 200. |
|\*Execution frequency |Task monitor rule execution frequency offers three options: minute level, hour level, and day level.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Set this parameter when <strong>Schedule Settings</strong> selects <strong>Regular scheduling</strong></div><br> |
|\*Execution date |Set the specific execution time according to the execution frequency.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Set this parameter when <strong>Schedule Settings</strong> selects <strong>Regular scheduling</strong></div><br> |
|**Alarm settings** ||
|\*Alarm channel |Supports alarm methods including Email + Site messages, WebHook. |
|\*hookUrl |Webhook request URL, starting with http or https.<br><br>Select http or https from the dropdown, then enter the Webhook URL. For detailed configuration instructions, see the **template rules** in the [Webhook Instructions](https://docs.byteplus.com/docs/dataleap/Configure_Hive_Template_Rules#2).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Set this parameter when <strong>alarm channel</strong> is set to <strong>Webhook</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After setting Webhook, notification messages will be actively pushed to the corresponding hookUrl.</div><br> |
|\*Alarm recipients |Users who receive alarms.<br><br><br>* When **alarm channel** is set to **Email + Site message**, you must select users or duty schedules to receive alarms.<br><br>   * User: enter user account keywords and select from the dropdown; multiple selections are supported.<br><br>   * Duty schedule: enter duty schedule name keywords and select from the dropdown. After setting, alarm messages will be sent to recipients in the duty schedule. |
|\*alarm sending |Number of alarm sendings. You can configure the number of sendings as needed, default is 1 time. |
|\*Sending interval |The interval time for sending alarms, default is 5 minutes and editable. |
|\*Do not disturb the alarm. |You can choose whether to enable do not disturb for alarms.<br><br>When **On** is selected, set the do not disturb time period as needed. |


<span id="df3c693c"></span>
## Management Rules

Perform management operations on monitoring objects with created monitoring rules by following these steps:


1. Log in to the DataLeap console.

2. Select **Data Quality \> Rules \> Batch Data \> Monitoring Object \> Other data sources** to enter the Other data sources page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/448321e30145484daa786c2028289fb6~tplv-goo7wpa0wc-image.image) </span>

3. Choose the project to manage from the project dropdown list at the top right of the page.

4. You can perform the following operations:

   * Set search criteria to find matching monitoring objects.

   * Click the **rule name** of a rule to view its configuration details on the rule details page, where you can also copy or edit the rule.

   * Click the **Test** button in the **Action** column for a rule, then set the test run time in the popup window to start a new test run.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the rule does not have scheduling set, that is, <strong>Schedule Settings</strong> selects <strong>Do not set now</strong>, test run is not allowed.      </div>
      

   * Click the **On/Off** button in the **Action** column of a rule name. In the pop\-up confirmation dialog, click **Confirm** to enable or disable the rule.

   * Click the **Edit** button in the **Action** column of a rule name to modify its rule information on the edit rule page.

   * Click the  **...**   **\> Delete** button in the **Action** column of a rule name. In the pop\-up confirmation dialog, click **Confirm** to delete the rule.

   * Click the  **...**   **\> Copy** button in the **Action** column of a rule name. On the copy rule page, you can edit the copied rule information.

   * Click the  **...**   **\> Share** button in the **Action** column of a rule name to copy the corresponding object's link.

   * Click the  **...**   **\> Last 7\-day results** button in the **Action** column of a rule name, which jumps to the **run result** page to view the 7\-day monitoring results of the rule up to the current day.

   * Click the  **...**   **\> Transfer owner** button in the **Action** column of a rule name to choose a new owner for the rule in the pop\-up window.

   * Select one or more rules and click the corresponding button to perform batch operations.

      * Batch open/close

      * Batch test

      * Batch Delete

      * Batch modify receivers

      * Batch transfer owner

      * Batch Modify rule strength


<span id="5d2cbc00"></span>
## Subsequent Actions

After the rule runs, you can check the run result page to view the rule's execution results, alarm status, and to identify and analyze issues. For instructions on managing rule run results, see [Manage Other Datasource Rule Run Results](https://docs.byteplus.com/docs/dataleap/Manage_Other_Datasource_Rule_Run_Results).
