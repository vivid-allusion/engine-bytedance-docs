---
title: "Configure Dual-data-source Validation Rules"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Configure_Dual-data-source_Validation_Rules"
---

Dual\-data\-source validation uses aggregation metrics to perform aggregation data comparison between any two data sources, such as whether the row count between different tables of the same type of data source is consistent, or whether the total sum of the same field (SUM) in two tables of different data sources is consistent, and so on. This feature supports creating validation rules using custom SQL. This article explains how to configure dual\-data\-source validation rules.

<span id="6f99a106"></span>
## Constraints


* After all activated services expire, all quality rules will be retained, but they will be disabled and cannot be used. After repurchasing the service, you must re\-enable the rule before it can be used.


<span id="_1-前提条件"></span>
## Prerequisites


* You have purchased the corresponding engine services.

* The network between both data sources is connected or they are within the same VPC.


<span id="_2-创建规则"></span>
## Create Rules


1. Log in to the DataLeap console.

2. Select **Overview \> Quality \> Rules \> Batch Rule \> Monitoring object** to open the monitoring object page.

3. In the project dropdown at the top right, select the project to manage.

4. Click the **Dual\-data\-source validation** tab to open the dual\-data\-source validation page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/748235f639534319b9b69f4714d06957~tplv-goo7wpa0wc-image.image) </span>

5. Click **New \> Create a new rule (direct connection to the engine execution)**  to open the creation page for direct engine rules.

6. After setting the related parameters, click the **Next** button step by step as prompted. After finishing, click the **Create rule** button to complete the creation.


The table below explains the parameters related to creating dual\-data\-source validation rules. Parameters marked with \* before the name are required, while those without \* are optional.


|Parameters |Description |
|---|---|
|**Dual\-data\-source check logic \- Select Data Source A** ||
|\*Data source type |Select the type of Data Source A to compare; options available in the dropdown.<br><br><br>* **Direct engine execution** supports options: **EMR Serverless Hive**, **ByteHouse cloud data warehouse**, **ByteHouse CE**. |
|\*Data source |The selected type of datasource is used. A registered datasource already in the console is auto\-filled, with other options available in the dropdown.<br><br>For related instructions on registering a datasource, see [Datasource Management](https://docs.byteplus.com/docs/dataleap/data_source_management). |
|\*Queue |Run queue in use. After selecting the **data source**, you can use the dropdown to select the queue corresponding to EMR Serverless Hive.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the <strong>data source</strong> is set to <strong>EMR Serverless Hive</strong>, this parameter must be configured.</div><br> |
|\*calculation group |The compute group corresponds to the selected data source.<br><br><br>* When the **data source type** is **ByteHouse cloud data warehouse**, after selecting a **data source**, you can use the dropdown to select compute groups that have already been created in the **ByteHouse cloud data warehouse console**.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Ensure that the resource group VPC and the network where the data source is located are already connected, either because the data source is within the resource group VPC or because connectivity has already been established through a public network, a dedicated line, or other networking solutions.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">In ByteHouse cloud data warehouse, you can only select compute groups that have <strong>enabled auto start\-stop</strong> or are <strong>currently running</strong>.</div><br> |
|\*XX query statement |Enter the query statement according to the selected type.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only single\-row aggregated data comparison is supported.</div><br> |
|**Dual\-data\-source validation logic \- select Data Source B** ||
|\*Data source type |Select the type of Data Source B for comparison from the dropdown.<br><br><br>* **Direct engine execution** supports options: **EMR Serverless Hive**, **ByteHouse cloud data warehouse**, **ByteHouse CE**. |
|\*Data source |The selected datasource type automatically fills in a registered datasource from the console. Other options are available in the dropdown. |
|\*Queue |Run queue in use. After selecting the **data source**, you can use the dropdown to select the queue corresponding to EMR Serverless Hive.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the <strong>data source</strong> is set to <strong>EMR Serverless Hive</strong>, this parameter must be configured.</div><br> |
|\*calculation group |The compute group corresponds to the selected data source.<br><br><br>* When the **data source type** is **ByteHouse cloud data warehouse**, after selecting a **data source**, you can use the dropdown to select compute groups that have already been created in the **ByteHouse cloud data warehouse console**.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Ensure that the resource group VPC and the network where the data source is located are already connected, either because the data source is within the resource group VPC or because connectivity has already been established through a public network, a dedicated line, or other networking solutions.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">In ByteHouse cloud data warehouse, you can only select compute groups that have <strong>enabled auto start\-stop</strong> or are <strong>currently running</strong>.</div><br> |
|\*XX query statement |The query statement corresponding to the selected type, enter as needed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only supports single\-line aggregated data comparison.</div><br> |
|**Dual\-data\-source check logic \- relevance dimension** (allows fine\-grained comparison of checked fields through related dimensions) ||
|source dimension |Dimension fields generated by the query statement from source data source A; multiple can be configured.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Configuring multiple dimension fields may increase validation task execution time.</div><br> |
|target dimensions |Dimension fields generated by the query statement from target data source B; multiple can be configured. |
|**Dual\-data\-source validation logic \- field mapping and logic check** ||
|\*source field |Indicator fields generated by the query statement from source data source A; at least one must be configured. |
|\*target field |Indicator fields generated by the query statement from target data source B; at least one must be configured. |
|\*alarm conditions |Alarm conditions refer to the criteria that indicators must meet to trigger an alarm. After the monitoring metrics are calculated, an alarm is triggered if the alarm conditions are met.<br><br>Alarm conditions support two options: **not equal** and **the absolute value of the difference is greater than**.<br><br><br>* Not equal: An alarm is triggered if metric A is not equal to metric B.<br><br>* The absolute value of the difference is greater than: An alarm is triggered if the absolute difference between metric A and metric B exceeds the set value.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A set of metric fields can have one alarm condition, and the alarm relation between multiple sets of fields is <strong>or</strong>.</div><br> |
|**Set monitoring rule** ||
|\*Rule name |The name of the monitoring rule, automatically generated based on the selected source types and dates of both ends, with manual modification supported. |
|Description |Description of the rule. |
|**set monitoring rule \- execution method** ||
|\*execution method |Execution methods for monitoring rules support **relate task**, **regular scheduling**, and **do not set** options.<br><br><br>* relate task: execute according to the scheduling time of the associated data development task.<br><br>* regular scheduling: set the execution time of the monitoring rule manually.<br><br>* do not set: no automatic scheduling; manual scheduling is available as needed. |
|\*task name |Search and select the task name to relate by task name keyword or ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When <strong>execution method</strong> is set to <strong>task</strong>, this parameter must be configured.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only supports associating offline tasks with scheduling frequencies of minute/hour/day/week/month within the current project.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Each time this task completes running (including rerun, backfill, and online scheduling), it will trigger the execution of monitoring rules.</div><br> |
|\*rule strength |Provides strong and weak configuration options.<br><br><br>* When **strong** is selected, you must set the **breaking method**. After the related task completes, it enters the strong rule execution phase, where the breaking method determines the downstream task's operation.<br><br>* When **weak** is selected, after the related task completes, it enters the weak rule execution phase. If an abnormality is found in the related task quality, this rule sends an alert notification but does not block downstream task operation.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When <strong>execution method</strong> is set to <strong>task</strong>, this parameter must be configured.</div><br> |
|\*Breaking methods |If it is a strong rule, you can choose one of the following two breaking methods:<br><br><br>* **Before the rule finishes running, the instance remains in a running state**: This means before the quality rule finishes, the related task instance stays running. If a strong\-rule alert triggers during this time, the related task instance status is set to failed, blocking downstream task execution. If no alert triggers, the related task instance is set to successful, triggering downstream task execution.<br><br>* **If the rule runs for more than X minutes without ending, set the instance as successful immediately**: This means if the quality rule runs beyond the set time, the related task instance status is directly set to successful, but the rule continues running and can still trigger alert notifications. At this point, downstream tasks remain triggered, but there may be a risk of data quality contamination, so monitoring results require timely attention. The timeout period can be set manually, with a range of 0 to 200. |
|\*Execution frequency |The task monitor rule execution frequency offers three options: minute\-level, hour\-level, and day\-level.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When <strong>execution method</strong> is set to <strong>regular scheduling</strong>, this parameter must be configured.</div><br> |
|\*Execution time |Set the specific execution time according to the execution frequency.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When <strong>execution method</strong> is set to <strong>regular scheduling</strong>, this parameter must be configured.</div><br> |
|**Alarm settings** ||
|\*Alarm channel |Supports alarm methods including **email+site message** and **Webhook**, with multiple selections supported. |
|\*hookUrl |Webhook request URL starting with http or https.<br><br>Select http or https from the dropdown, then enter the Webhook URL. For detailed configuration instructions, refer to [Webhook Instructions](https://docs.byteplus.com/docs/dataleap/Configure_Hive_Template_Rules#2).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When <strong>alarm channel</strong> is set to <strong>Webhook</strong>, this parameter must be configured.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After setting the webhook, notification messages will be actively pushed to the corresponding hookUrl.</div><br> |
|\*alarm receivers |Users who receive alarm notifications. You can select the user or duty schedule to receive the alarm.<br><br><br>* User: Enter the user account keyword and select from the dropdown list. Multiple selections are supported.<br><br>* Duty schedule: Enter the duty schedule name keyword and select from the dropdown list. After setting, alarm messages will be sent to the recipients in the duty schedule. |
|\*alarm sending |The number of times the alarm will be sent. You can configurable number of sends, default is 1 time. |
|\*Sending interval |The interval time for alarm sending, default is 5 minutes, editable. |
|Do not disturb the alarm. |You can choose whether to enable do not disturb for alarms.<br><br>When **On** is selected, set the do not disturb period as needed. |


<span id="_3-管理规则"></span>
## Manage Rules

You can manage created dual\-data\-source validation rules by following these steps:


1. Log in to the DataLeap console.

2. Select **Data quality \> Rules \> Batch Rule \> Monitoring object \> Dual\-data\-source validation** to enter the dual\-data\-source validation page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/748235f639534319b9b69f4714d06957~tplv-goo7wpa0wc-image.image) </span>

3. In the project dropdown list at the top right of the page, select the project you want to manage.

4. You can perform the following operations:

   * Set search criteria to find matching monitoring rules.

   * Click the **Test** button in the **Action** column of a rule name, then in the popup window, set the test run time to start a new test run.

   * Click the **On/off** button in the **Action** column of a rule name, then in the confirmation dialog box, click **Confirm** to enable or disable the rule.

   * Click the **Edit** button in the **Action** column of a rule name to modify its rule information on the edit rules page.

   * Click the  **...**   **\> Delete** button in the **Action** column of a rule name, then click the **Confirm** button in the pop\-up confirmation dialog to delete the rule.

   * Click the  **...**   **\> Task** button in the **Action** column of a rule name to set the associated task for the rule in the pop\-up window.

   * Click the  **...**   **\> Share** button in the **Action** column of a rule name to copy the link of the corresponding object.

   * Click the  **...**   **\> Last 7\-day results** button in the **Action** column of a rule name to jump to the **run result** page to view the 7\-day monitoring results of the rule up to the current day.

   * Click the  **...**   **\> Transfer Owner** button in the **Action** column of a rule name to open a popup window where you can transfer the rule to a new owner.

   * Select one or more rules, then click the corresponding button to perform batch operations.

      * Batch Transfer Owner

      * Batch Modify rule Strength


<span id="eec64668"></span>
## Subsequent Operations

After the rule runs, you can view its run result and alarm status on the **run result** page to locate and analyze issues. See [Manage Dual-data-source Validation Rule Run Results](https://docs.byteplus.com/docs/dataleap/Manage_Dual-data-source_Validation_Rule_Run_Results) for instructions on managing rule run results and related operations.
