---
title: "Configure Hive Template Rules"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Configure_Hive_Template_Rules"
---

The template is designed to define monitoring validation rules for easy reuse later. This article introduces how to configure Hive template rules.

<span id="600962b1"></span>
## **Constraints**


* After all activated services expire, all quality rules will be retained, but they will be disabled and cannot be used. After repurchasing the service, you must re\-enable the rule before it can be used.


<span id="_1-前提条件"></span>
## Prerequisites

EMR_SERVERLESS_SPARK engine service must be purchased to use the corresponding engine functions.

<span id="_2-创建规则"></span>
## Create Rules


1. Log in to the DataLeap console.

2. Select **Overview \> Quality \> Rules \> Offline Rule \> Monitoring object** to directly access the monitoring object template rules page.

3. Select the project to manage from the project dropdown list at the top right of the page.

4. Select the engine and corresponding instance to configure from the **Engine** dropdown list.

5. Create a monitoring object.

   1. Click the  **+Hive monitoring object** button, and in the pop\-up window, set the monitoring object information.

   2. Click the **OK** button, and the object will be added successfully and displayed in the monitoring object list.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96518edf46cb4c4f9507e9fde2bf4d3d~tplv-goo7wpa0wc-image.image) </span>

6. Create monitoring rules.

   1. Click the **Create Rules** button for a monitoring object to open its new monitoring rule creation page.

   2. After setting the rule information, click the **Complete** or **Complete and test run** button to finish creating the rule.

      * Click the **Complete** button to finish creating the rule.

      * Click the **Complete and test run** button. In the pop\-up window, select the test run time, then click the **Confirm** button to complete the rule creation and start a test run directly.


The following table explains the parameters related to creating template rules. Parameters with \* before their names are required; those without \* are optional.


|Parameters |Description |
|---|---|
|\*Engine |The database storage engine for creating rules supports EMR_SERVERLESS_SPARK engines, selectable from the dropdown.<br><br><br>* EMR_SERVERLESS_SPARK: select an instance from the dropdown list; the default is Default. |
|**Create new monitoring object** ||
|\*Table name |Create the monitoring object's database and table names. Supports two setup methods: **enter by table** and **enter by database**.<br><br><br>* Enter by table: input **database.table**, then click the **Add** button to add a table. Multiple tables can be added in batches.<br><br>* Enter by database: select a database from the database dropdown, then choose the tables to monitor from the table dropdown, and click the **Add** button to add a table. Supports fuzzy search when selecting tables and allows adding multiple tables in batches.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only partition tables with permission can be added as monitoring objects.</div><br> |
|**Create rules** ||
|\*Monitoring object |Displays the monitoring object for which the rule is created and cannot be edited.<br><br>This parameter is configured when creating a new monitoring object. |
|\*Select partition |Automatically detected based on existing table partitions and editable.<br><br>If no partitions are available, you can add them via the **Add partition** button. Supports multiple partition expression options, selectable from a dropdown. For explanations related to partition expressions, see [Description of platform time variables and constants](https://docs.byteplus.com/docs/undefined/689d96727654f3051453d252). |
|**Rule configuration** ||
|\*Rule type |Supports template types such as table row count, duplication, null, outlier, and table field, selectable from a dropdown.<br><br><br>* Row count: calculates the number of rows in the partition, typically used to detect anomalies like empty partition data after task completion or to monitor row count fluctuations according to your needs. Definition of row count calculation: count(\*)<br><br>* Duplication: select one or more fields to calculate the duplication ratio, commonly used for primary key duplication checks; the calculation method is (count(\*) \- count(distinct key)) / count(\*).<br><br>* Null: special anomaly monitoring using NULL, empty string, or custom null types (e.g., unknown) to detect the null ratio of one or more fields.<br><br>* Outlier: calculate the number or ratio of outliers based on the provided list or expression of normal or abnormal values.<br><br>* Table field: select a field, then choose a calculation method such as sum(money), and monitor this metric. |
|\*Rule name |Monitoring rule name, auto\-filled and editable. |
|\*Attributes |Name of the table field to monitor; selectable from the dropdown.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When <strong>rule type</strong> is set to <strong>duplication</strong>, <strong>null</strong>, <strong>outlier</strong>, or <strong>table field</strong>, this parameter must be configured.</div><br> |
|\*Null type |Supports three options: NULL, empty string, and custom.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When <strong>rule type</strong> is set to <strong>null</strong>, this parameter must be configured.</div><br> |
|\*Matching logic |Supports two options: **list of normal values** and **list of outliers**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the <strong>rule type</strong> is set to <strong>outlier</strong>, this parameter must be configured.</div><br> |
|\*Matching method |Supports two options: **enumerated values** and **regular expression**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the <strong>rule type</strong> is set to <strong>outlier</strong>, this parameter must be configured.</div><br> |
|\*Match values |Content corresponding to the matching logic.<br><br><br>* When the **matching method** selects **enumerated values**, input enumerated values for matching. Add by clicking the **Add** button; multiple enumerated values can be set.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only one enumerated value can be entered at a time. Press Enter to complete the setting. If multiple enumerated values need to be entered, add them one by one by clicking the <strong>Add</strong> button.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Enter hive_none to represent a null value, enter hive_empty to represent an empty string.   </div><br>   <br><br>* When the **matching method** selects **regular expression**, input a regular expression for matching. For example, a mobile number matching example: ^1[34578]\d{9}$<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the <strong>rule type</strong> is set to <strong>outlier</strong>, this parameter must be configured.</div><br> |
|\*Calculation method |Method used to calculate a monitored attribute; supports sum, count, avg, and count distinct options.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the <strong>rule type</strong> is set to <strong>table field</strong>, this parameter must be configured.</div><br> |
|\*Alarm conditions |Refers to the conditions the metrics must meet for a rule to trigger an alarm. When monitoring metrics are calculated, an alarm is triggered if the alarm conditions are met.<br><br>Alarm conditions support alerts for numeric types, volatility, dynamic threshold, duplication ratio, null ratio, etc. The default relationship between multiple alarm conditions is **and**, which can be changed to **or**.<br><br><br>* Value: the calculated metric itself, such as sum(money), count(\*), etc. This metric is directly compared to the set threshold to determine whether to trigger an alarm. Example:<br><br>   * Monitoring rule: trigger an alarm when the row count exceeds 2000.<br><br>   * Alarm judgment: suppose the detected row count value is 2500; it is compared with the set threshold (2000). Since it exceeds the threshold, an alarm is triggered.<br><br>* Volatility (unit: %): calculates the ratio of the current metric result to the metric over a certain period or at a specific point in time, then compares the calculated volatility with the set threshold to determine if an alarm should be triggered. Currently supported volatility types and calculation methods include:<br><br>   * Volatility compared to the previous cycle: (current detected value \- previous cycle detected value) / previous cycle detected value<br><br>   * Volatility compared to 1 day ago: (current detected value \- detected value 1 day ago) / detected value 1 day ago<br><br>   * Volatility compared to 7 days ago: (current detected value \- detected value 7 days ago) / detected value 7 days ago<br><br>   * Volatility compared to the 7\-day average: (current detected value \- average detected value over 7 days) / average detected value over 7 days<br><br>   * Volatility compared to the 30\-day average: (current detected value \- average detected value over 30 days) / average detected value over 30 days<br><br>   After selecting a volatility type from the dropdown, choose a judgment method and set the volatility value. Each volatility type supports multiple judgment methods such as \>, <, ∈ (belongs to), ∉ (does not belong to); volatility values have positive and negative distinctions, with positive values indicating growth fluctuations and negative numbers indicating reduced fluctuations. Examples of specific settings are as follows:<br><br>   * Monitoring rule: set the volatility of row count to **volatility before 7 days ∉**   **`-20%`**  ** \- ** **`20%`** , which means an alarm will trigger if the row count volatility compared to 7 days ago falls outside the range of \-20% to 20%.<br><br>   * Monitoring process: After calculating the number of rows in the table for the current day (assumed to be 2,500), it is compared with the row count from 7 days ago (assumed to be 2,000). The volatility is calculated as a 25% increase, resulting in an alarm.<br><br>* Dynamic threshold: Predicts the row count range for the next partition based on historical partition data. An alarm triggers if the new partition's row count falls outside this range. See [Dynamic Threshold Instructions](https://docs.byteplus.com/docs/dataleap/Configure_Hive_Template_Rules#a-1-%E5%8A%A8%E6%80%81%E9%98%88%E5%80%BC%E4%BD%BF%E7%94%A8%E8%AF%B4%E6%98%8E) for applicable scenarios of the dynamic threshold.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Dynamic thresholds cannot be configured with other alarm conditions simultaneously. If <strong>alarm conditions</strong> are set to <strong>dynamic threshold</strong>, no other alarm condition types can be added.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Alarm condition options vary according to the rule type; refer to the actual options on the page.</div><br> |
|**Execution method** ||
|* Running method |Execution methods for monitoring rules include **RelateStudioTask**, **Regular scheduling**, and **Do not set now**.<br><br><br>* RelateStudioTask: executes according to the scheduling time of the associated data development task.<br><br>* Regular scheduling: set the execution time for monitoring rules yourself.<br><br>* Do not set now: No automatic scheduling, can be manually scheduled as needed. |
|* Task name |Search and select the name of the related task by task name keywords or ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the <strong>Running method</strong> is set to <strong>RelateStudioTask</strong>, this parameter must be configured.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Currently, only offline tasks with scheduling frequency at the minute/hour/day/week/month level under the current project are supported for association.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Tasks of Sensor type are not supported for association yet.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The execution of monitoring rules will start after each task run completes (including rerun, backfill, and activation scheduling).</div><br> |
|\*rule strength |Provides two configuration options: strong and weak.<br><br><br>* When **strong** is selected, set the **breaking method**. After the related task completes, the strong rule phase starts, where the breaking method determines the downstream task's operation.<br><br>* When **weak** is selected, after the related task completes, the weak rule phase starts. If a quality issue is detected in the related task, the rule sends an alarm notification but does not block the downstream task.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When <strong>running method</strong> is set to <strong>RelateStudioTask</strong>, this parameter must be set.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Since dynamic thresholds may cause false alarms, choose strong rules carefully when <strong>alarm conditions</strong> are set to <strong>dynamic threshold</strong>.</div><br> |
|\*breaking method |For strong rules, choose one of the following two breaking methods:<br><br><br>* **Before rule execution completes, the instance remains in running status**: it means the associated task instance stays running until the quality rule finishes. If a strong rule alarm triggers, the associated task instance status changes to failed, blocking downstream tasks; if no alarm triggers, the associated task instance is set to successful and triggers downstream task execution.<br><br>* **If rule execution exceeds X minutes without ending, the instance is directly set to successful**: it means when the quality rule runs beyond the set time, the associated task instance status is directly set to successful, but the rule continues to run and can still trigger alarm notifications. At this point, downstream tasks still trigger and run, but a data quality contamination risk may exist, requiring timely monitoring of results. The timeout period can be set freely within the range of 0 to 200. |
|\*Execution frequency |Task monitor rule execution frequency offers three options: minute\-level, hour\-level, and day\-level.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When <strong>execution method</strong> is set to <strong>regular scheduling</strong>, this parameter must be set.</div><br> |
|\*Execution time |Set specific execution times based on the execution frequency.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When <strong>execution method</strong> is set to <strong>regular scheduling</strong>, this parameter must be set.</div><br> |
|\*Operation queue |The rules use an operation queue and support two options: default queue or self\-specified queue.<br><br><br>* Use default queue: use the system's default engine queue without manual selection.<br><br>* Self\-specified queue: select the engine queue to use; the dropdown lists queues bound to the current project. If you have not applied for queues, please go to the corresponding console to apply.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Queues specified manually only show options that support batch task execution.</div><br> |
|**Alarm settings** ||
|\*Alarm channel |Supports alarm methods including **Email + Site message** and **Webhook**, with multiple selections supported. |
|\*hookUrl |Webhook request URL starting with http or https.<br><br>Select http or https from the dropdown and enter the Webhook URL. For detailed configuration instructions, refer to **Webhook Usage Guide**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter must be set when <strong>Alarm channel</strong> is set to <strong>Webhook</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After setting the Webhook, notification messages will be actively pushed to the corresponding hookUrl.</div><br> |
|\*Receivers |Users who receive alarms.<br><br>When the **alarm channel** is set to **Email + Site message**, you must select the users or duty schedule receiving the alarms.<br><br><br>* User: Enter user account keywords and select from the dropdown list; multiple selections are supported.<br><br>* Duty Schedule: Enter the duty schedule name keywords and select from the dropdown list. After setting, alarm messages will be sent to recipients in the duty schedule. |
|\*Alarm sending |The number of the alarm sends. You can configure the number of sends as needed. The default is 1 time. |
|\*Transmission interval |The interval time for sending alarms, default 5 minutes, editable. |
|\*Do not disturb the alarm. |You can choose whether to enable alarm do not disturb.<br><br>When **On** is selected, you can set the do not disturb period as needed. |
|**Advanced settings** ||
|Retry condition |Failed to run |
|Operation parameters |Configure operation parameters before the SQL statement as needed, such as “set parameter 1 =;”. |
|Filter SQL |Condition statements after where, with syntax logic consistent with HSQL. No need to enter where, for example type='xxx'. |
|Custom alarm |Customize alarm time, supporting selection of Beijing or UTC time as needed from the dropdown. |


<span id="_3-管理规则"></span>
## Manage Rules

You can manage created monitoring rules for monitoring objects by following these steps:


1. Log in to the DataLeap console.

2. Select **Data quality \> Rules \> Offline Rule \> Monitoring object** to go directly to the template rules page of the monitoring object.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f54ea0ee033a4dfdbee240dbc17d5f73~tplv-goo7wpa0wc-image.image) </span>

3. Select the project to manage from the project dropdown list at the top right of the page.

4. The following operations can be performed:

   * Set search criteria to find monitoring objects that meet the conditions.

   * Manage monitoring objects

      * Hover over the **Latest alarm** count in the row of a monitoring object in the list to display the latest alarm information. Click the **View** button of an alarm to see detailed information on the result details page and perform the following operations:

         * Click the **View rule** button to see the detailed information of the rule.

         * Click the **Run log** button to view the monitoring run log of the rule.

         * Click the  **...**   **\> Execution records** button to view detection execution records.

         * Click the  **...**   **\> View SQL** button to see the SQL statements executed on the day of this rule check.

         * Click the  **...**   **\> Rerun** button and confirm to rerun this monitoring rule.

      * Click the  **...**   **\> Delete object** button in the row of a monitoring object in the list and confirm deleting the object and all its rules.

      * Click the  **...**   **\> Add Partition** button in the row of a monitoring object in the list and set partition info in the popup window to add a new partition to this object.

   * Manage monitoring object partitions

      * Click the **New Rule** button in the **Action** column of an object partition to add a monitoring rule on the new rule page as needed.

      * Click the **Modify Expression** button in the **Action** column of a partition to change the partition expression information in the pop\-up window.

   * Manage rules under partition

      * Click the **View SQL** button in the **Action** column of a rule name to view the SQL statement of the rule.

      * Click the **Edit** button in the **Action** column of a rule name to modify its rule information on the edit rules page.

      * Click the  **...**   **\> View** button in the **Action** column of a rule name to check rule configuration and test run records on the rule details page, and you can also copy, test run, or rerun existing records of the rule.

      * Click the  **...**   **\> Test** button in the **Action** column of a rule name and set the test run time in the pop\-up window to start a new test run.

      * Click the  **...**   **\> On/Off** button in the **Action** column of a rule name, then click **Confirm** in the confirmation dialog to turn the rule on or off.

      * Click the  **... \> Delete** button in the **Action** column of a rule name, then click the **Confirm** button in the popup to delete the rule.

      * Click the  **...**   **\> Share** button in the **Action** column of a rule name to copy the corresponding object's link.

      * Click the  **...**   **\> Copy** button in the **Action** column of a rule name, then edit the copied rule information on the copy rule page.

      * Click the  **...**   **\> View 7\-day results** button in the **Action** column of a rule name to jump to the **run result** page and check the 7\-day monitoring results of the rule up to the current day.

      * Click the  **...**   **\> Transfer owner** button in the **Action** column of a rule name, and select a new owner for the rule in the popup window.

      * Select one or more rules, then click the corresponding button to perform batch operations.

         * Batch enable/disable

         * Batch test run

         * Batch delete

         * Batch modify alarms

         * Batch transfer owner

         * Batch modify rule strength


<span id="8c4289e9"></span>
## Subsequent Operations

After running the rule, you can view the results and alarm status on the **run result** page to find and analyze issues. For operations managing rule run results, please see .

<span id="附录a：规则说明"></span>
## Appendix: Rule Description

<span id="a-1-动态阈值使用说明"></span>
###   Dynamic Threshold Instructions

When creating template rules, if the **rule type** is set to **row count**, you can configure dynamic threshold alarms.

The dynamic threshold predicts the row count range of the next partition based on historical partition data. An alarm triggers if the new partition’s row count falls outside this range.

Analysis shows that data distribution for table row count mainly follows these patterns:


|**distribution** |monotonically non\-decreasing (A) |overall rising with occasional decreases (B) |constant (C) |low frequency of change (D) |other |
|---|---|---|---|---|---|
|**chart example** |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_94c05349f2a04249fd719308aa49f8e0.png) </span> |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0bb56ead4b320da31bae5aa740b2cbd1.png) </span> |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_731ae5320107460b0c25c9a3c0b28516.png) </span> |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7af55ec9b12f90f31714fb56c6e4ba09.png) </span> |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dc88e8b145948208eb8e7c505c1ec4d1.png) </span> |


The dynamic threshold performs better on the four distributions mentioned above: A, B, C, and D. Therefore, before enabling dynamic threshold alarms, review the historical table row count trend to determine if this alarm condition is appropriate.

<span id="2"></span>
### Webhook Instructions

When creating monitoring rules, if you choose Webhook as the alarm method, you must register the Webhook URL. Subsequent alarms will be sent to the registered URL. You can develop follow\-up issue handling processes based on requests from the URL.

<span id="a-2-1-webhook-配置"></span>
#### WebHook Configuration


1. Select **Alarm methods** from the dropdown list, then choose **Webhook**.

2. Configure **WebHook**: select **http** or **https** from the dropdown list, then enter the hookUrl.

   Example of a URL address:

   ```json
   volc_quality_test.volcwebhook.xxx/xx/webhook
   ```
   


<span id="a-2-2-hookurl-验证"></span>
#### HookUrl Verification

After entering the hookUrl, click the displayed **Verify** button to verify.

During verification, a request containing a challenge—an unpredictable integer—is sent to the hookUrl. The challenge must be returned exactly as received to pass verification. Verification example:


* **Verification request body**

   ```json
   {
       "source": null
       "region": null
       "type": null
       "rule_name": null
       "callback_url": null
       "target_type": null
       "target": null
       "content": null
       "event_time": "2020-03-01 00:00:00", // alarm time, message notification time
       "owners": null
       "challenge": 1230201 // random integer
   }
   ```
   

* **Response body example**

   ```json
   {
       "status": 0,  // status code, 0
       "data": {
           "challenge": 1230201 // pass the original value
       }
   }
   ```
   


<span id="a-2-3-webhook-请求"></span>
#### Webhook Request

Configuring URL alarm will send a request to the URL address. The specific example is as follows:


* **Request body example**

   ```json
   {
       "source": "quality",  // Chinese name of the source system
       "region": "cn",     // deployment environment of the source system
       "type": 1,          // alarm/message: enumeration values: 1 for alarm, 2 for message
       "rule_name": "xxx_rule",       // rule name generating events in the source system
       "callback_url": "url_to_rule", // callback URL of the rule generating events in the source system
       "target_type": "table",        // general category distinguishing described objects, such as: task, database, table
       "target": "test_tb",           // specific event object description, generally including: object name and specific name value
       "content": "alarm content",    // detailed event description, either alarm content or notification content
       "event_time": "2020-03-01 00:00:00", // alarm time, message notification time
       "owners": "test,test2"         // direct person in charge of this event
       "challenge": null
   }
   ```
   

* **Response body example**

   ```json
   {
       "status": 0,  // status code, 0
       "data": null
   }
   ```
   


<span id="a-2-4-网络要求"></span>
#### Network Requirements

Ensure the message service can access the network of hookUrl. The description of the IP/domain network for hookUrl is as follows:


* If the IP/domain is on the public network or public service area, it can be accessed.

* If the IP/domain is in the private network of the selling area, access requires registering a shuttle server and forwarding through the shuttle.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Provide the service VPC ID, IP, and port, and contact the tenant admin to register the shuttle server.   </div>
