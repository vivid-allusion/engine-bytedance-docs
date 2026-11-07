---
title: "Scheduled scaling management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/scheduled-scaling-management"
---

DBW provides scheduled scaling functionality, which is commonly used to handle predictable workload changes. You only need to configure rule\-based scaling policies, and DBW will automatically perform database scaling operations on schedule without manual intervention, achieving the optimal balance between performance and cost. This topic explains how to configure scheduled scaling rules in the DBW console.

<span id="kCWZkA2t"></span>
## Prerequisites


* A NDB for MySQL instance has been created, and its status is Running. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For details, refer to (veDB  [Enabling instance security control (NDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control?lang=en) and  [Applying for operation permissions](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket?lang=en)[ (NDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket?lang=en)[](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket?lang=en).


<span id="TUvIqqQl"></span>
## Precautions


* Scheduled instance specification adjustment and scheduled node count adjustment are mutually exclusive; both cannot be configured simultaneously.

* When configuring scheduled scaling rules, only higher\-specification configurations are supported as the target for scale\-up; selecting the same or lower specifications as a scale\-up target is not allowed. This ensures that scheduled operations can effectively address anticipated resource growth demands, such as business peak periods.

* If a scheduled scaling operation fails (e.g., due to insufficient resources or instance anomalies), the system will not retry automatically and will wait for the next scheduling cycle to reassess execution conditions.

* If the instance is in a state of specification change, migration, or other unsupported configuration changes, the scheduled scaling operation will be skipped and reevaluated in the next scheduling cycle. If scaling down fails after scaling up an instance, you can manually change the instance configuration. For details, see [Change instance configuration](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Changing_instance_configuration?lang=en).

* Scaling trigger conditions

   * Scale\-up condition: The current instance specification is lower than the target specification and meets the scaling adjustment start time.

   * Scale\-down condition: The current instance specification must exactly match the target specification and meet the time to revert to the original specification.

* Business impact

   * Scaling operations will interrupt ongoing Online DDL tasks. Schedule the operation time carefully.

   * During the operation, database connections may experience brief interruptions. It is recommended to perform the operation during off\-peak hours.

* Specification types cannot be changed across categories: When modifying the instance specification, the instance's specification type cannot be altered. For example, if the original instance is general\-purpose, only general\-purpose specifications can be selected. If the original instance is exclusive, only exclusive specifications can be selected.

* Currently, you cannot configure both CPU usage\-based auto scaling and scheduled scaling rules simultaneously. Only one can be enabled at a time. For details about auto scaling of node specifications, see [Node specification auto scaling management](https://docs.byteplus.com/en/docs/DBW/Auto_scaling_management?lang=en).

* If the instance undergoes another configuration change operation—such as a manual adjustment—during the scheduled scale\-up period, resulting in a mismatch between the instance's current specification and the target specification defined in the scheduled scaling policy at the time of restoration, the restoration operation will not be performed.

* Description of scheduling date validity:

   * Scheduled rules are triggered only when the specified date actually exists. For example:

      * If the scaling\-up rule is set to the 29th of each month, scaling up will not be performed in February (which has no 29th).

      * If the scaling\-down rule is set to the 2nd of each month, the system checks whether the current instance specification matches the target specification on that day. Scaling down is performed only when the condition is met.

   * Example scenario:

      * Assume the scaling\-up rule is set to the 29th of each month, and the scaling\-down rule is set to the 2nd of each month.

      * February 2025 does not have a 29th day, so scaling up will not be performed. On March 2, when checking the scale\-down conditions, if the current specification has not reached the target specification—for example, it is still at the original specification—the scale\-down will not be executed.

      * However, if you manually upgrade the instance to the target specification on March 1, the system will determine that the conditions are met on March 2 and perform the scaling\-down operation normally.

* Before using the AutoOps function, make sure that there is sufficient balance in the account to support changing the instance configuration. For more billing information about the product, see [Billing overview](https://docs.byteplus.com/en/docs/DBW/billing-description?lang=en).

* The interval between scheduled scaling up and reverting to the original specification must be at least 1 hour.

* Currently, scheduled scaling is only supported for instances with kernel versions 3.0.x.x and 2.0.x.x.


<span id="STHu78lG"></span>
## Advantages


* Prepare resources in advance to avoid delayed responses:


Complete scaling up before traffic peaks to prevent service delays or failures caused by instance cold starts or application warm\-ups.


* Controllable and predictable costs

   * Resources scale according to plan, facilitating budget management and cost accounting.

   * Scale down during off\-peak hours to avoid resource waste.

* Simplified operation and maintenance logic

   * For businesses with strong cyclical patterns and clear trends, complex monitoring metrics are unnecessary.

   * Reduce frequent scaling caused by metric fluctuations, also known as oscillation issues.


<span id="J30NBjgw"></span>
## Applicable scenarios

Scheduled scaling is suitable for business scenarios with predictable load patterns and known timeframes, as follows:


* Business systems with fixed working hours: For example, internal corporate systems like OA or HR platforms, which are used from 09:00 to 18:00 on weekdays and can be scaled down to minimal capacity at night.

* Education or exam platforms: Daily activities like classes or exams occur during fixed time slots, with traffic concentrated in specific periods, while weekends or holidays see almost no activity.

* E\-commerce mega promotion or flash sale event: Scale up 5\-10 minutes before the event starts, and scale down immediately after the event ends.

* Batch data processing tasks: Batch processing jobs are executed daily at 2:00 AM. Computing nodes can be scheduled to start, and resources are released upon task completion.

* Live streaming or media platforms: For example, for programs like Xinwen Lianbo airing at 7 PM daily, pre\-scaling is recommended to handle the concentrated viewer influx.

* Development and testing environments: Enable during workdays and automatically shut down after hours or on weekends to reduce costs.


Scheduled scaling achieves efficient resource allocation with minimal operational overhead, ensuring optimal performance while significantly lowering cloud service expenses.

<span id="tztS48Ny"></span>
## Enable scheduled scaling


<Tabs>
<Tab zoneid="cStmuQZ3t6" title="Schedule instance specification adjustment">
<TabTitle>Schedule instance specification adjustment</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **veDB MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, select **Configure AutoOps rules** \> **Scheduled scaling**.

6. On the **Scheduled scaling** panel, check **Enable scheduled scaling** and configure the following parameters.



<Tabs>
<Tab zoneid="ITBr2ttIes" title="Execute only once">
<TabTitle>Execute only once</TabTitle>


|Parameter |**Description** |
|---|---|
|**Perform operation** |Default is **Adjust instance specification**, which can not be modified. |
|**Target specification** |Select the target scale\-up specification from the drop\-down list. |
|**Recurrence interval** |Select **Execute only once** from the drop\-down list to perform the scaling once without repetition. |
|**Adjustment start time** |Select the start time for scaling out as needed and click **OK**. The scaling start time cannot be earlier than the current time. |
|**Time to revert to the original specification** |Set the time to revert to the original specification as needed, then click **OK**.<br><br>The interval between the adjustment start time and the time to revert to the original specification must be greater than or equal to 1 hour. |





</Tab>
<Tab zoneid="BR02LqCkXg" title="By day">
<TabTitle>By day</TabTitle>


|Parameter |**Description** |
|---|---|
|**Perform operation** |Default is **Adjust instance specification**, which can not be modified. |
|**Target specification** |Select the target scale\-up specification from the drop\-down list. |
|**Effective time** |Select the effective start and end dates as needed. |
|**Recurrence interval** |Select **By day** from the drop\-down list to repeat scaling operations daily. If the scaling operation is not completed within the previous cycle, it will be automatically skipped, and the system will re\-evaluate whether to perform scaling in the next cycle. |
|**Adjustment start time** |Select the start time for scaling up as needed and click **OK**. |
|**Time to revert to the original specification** |Set the time to revert to the original specification as needed, then click **OK**.<br><br><br>* The interval between the adjustment start time and the time to revert to the original specification must be greater than or equal to 1 hour.<br><br>* The interval between the adjustment start time and the previous time to revert to the original specification must be greater than or equal to 1 hour. |





</Tab>
<Tab zoneid="Zk9GQd8HYt" title="Week">
<TabTitle>Week</TabTitle>


|Parameter |**Description** |
|---|---|
|**Perform operation** |Default is **Adjust instance specification**, which can not be modified. |
|**Target specification** |Select the target scale\-up specification from the drop\-down list. |
|**Effective time** |Select the effective start and end dates as needed. |
|**Recurrence interval** |Select **Weekly** from the drop\-down list to repeat scaling operations weekly. If the scaling operation is not completed within the previous cycle, it will be automatically skipped, and the system will re\-evaluate whether to perform scaling in the next cycle. |
|**Adjustment start time** |Select the start time for scaling up as needed and click **OK**. |
|**Time to revert to the original specification** |Set the time to revert to the original specification as needed, then click **OK**.<br><br><br>* The interval between the adjustment start time and the time to revert to the original specification must be greater than or equal to 1 hour.<br><br>* The interval between the adjustment start time and the previous time to revert to the original specification must be greater than or equal to 1 hour. |





</Tab>
<Tab zoneid="mVWaLac3ge" title="Monthly">
<TabTitle>Monthly</TabTitle>


|Parameter |**Description** |
|---|---|
|**Perform operation** |Default is **Adjust instance specification**, which can not be modified. |
|**Target specification** |Select the target scale\-up specification from the drop\-down list. |
|**Effective time** |Select the effective start and end dates as needed. |
|**Recurrence interval** |Select **Weekly** from the drop\-down list to repeat scaling operations weekly. If the scaling operation is not completed within the previous cycle, it will be automatically skipped, and the system will re\-evaluate whether to perform scaling in the next cycle. |
|**Adjustment start time** |Select the start time for scaling up as needed and click **OK**. |
|**Time to revert to the original specification** |Set the time to revert to the original specification as needed, then click **OK**.<br><br><br>* The interval between the adjustment start time and the time to revert to the original specification must be greater than or equal to 1 hour.<br><br>* The interval between the adjustment start time and the previous time to revert to the original specification must be greater than or equal to 1 hour. |





</Tab>
</Tabs>



7. Click **OK**.


</Tab>
<Tab zoneid="x0CLdJQFSr" title="Schedule adjustment of the number of instance nodes">
<TabTitle>Schedule adjustment of the number of instance nodes</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **veDB MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, select **Configure AutoOps rules** \> **Scheduled scaling**.

6. On the **Scheduled scaling** panel, check **Enable scheduled scaling** and configure the following parameters.



<Tabs>
<Tab zoneid="SEdJwQPXS1" title="Execute only once">
<TabTitle>Execute only once</TabTitle>


|**Parameter** |**Description** |
|---|---|
|**Perform operation** |This operation uses **Adjust the number of instance nodes** as an example. |
|**Target count** |Select the number of nodes for instance scaling from the dropdown list. The target count cannot be lower than the current number of nodes. |
|**Recurrence interval** |Select **Execute only once** from the drop\-down list to perform the scaling once without repetition. |
|**Adjustment start time** |Select the start time for scaling out as needed and click **OK**. The scaling start time cannot be earlier than the current time. |
|**Time to revert to the original specification** |Set the time to revert to the original specification as needed, then click **OK**.<br><br>The interval between the adjustment start time and the time to revert to the original specification must be greater than or equal to 1 hour. |





</Tab>
<Tab zoneid="UtfasOLxxk" title="By day">
<TabTitle>By day</TabTitle>


|**Parameter** |**Description** |
|---|---|
|**Perform operation** |This operation uses **Adjust the number of instance nodes** as an example. |
|**Target count** |Select the number of nodes for instance scaling from the dropdown list. The target count cannot be lower than the current number of nodes. |
|**Recurrence interval** |Select **By day** from the dropdown list to repeat the scaling operation once every day within the effective time period. If the instance scaling is not completed in the previous cycle, it will be automatically skipped, and the system will check again in the next cycle to determine whether scaling can be performed. |
|**Effective time** |Select the start time and end time for the instance node scaling to take effect. |
|**Adjustment start time** |Select the start time for scaling out as needed and click **OK**. The scaling start time cannot be earlier than the current time. |
|**Time to revert to the original specification** |Set the time to revert to the original specification as needed, then click **OK**.<br><br><br>* The interval between the adjustment start time and the time to revert to the original specification must be greater than or equal to 1 hour.<br><br>* The interval between the adjustment start time and the previous time to revert to the original specification must be greater than or equal to 1 hour. |





</Tab>
<Tab zoneid="DpXUloQ1c9" title="Week">
<TabTitle>Week</TabTitle>


|**Parameter** |**Description** |
|---|---|
|**Perform operation** |This operation uses **Adjust the number of instance nodes** as an example. |
|**Target count** |Select the number of nodes for instance scaling from the dropdown list. The target count cannot be lower than the current number of nodes. |
|**Recurrence interval** |Select **Weekly** from the drop\-down list to repeat the scaling operation once per week during the effective period. If the scaling operation is incomplete in the previous cycle, it will be skipped automatically and re\-evaluated in the next cycle. |
|**Effective time** |Select the start time and end time for the instance node scaling to take effect. |
|**Adjustment start time** |Select the start time for scaling out as needed and click **OK**. The scaling start time cannot be earlier than the current time. |
|**Time to revert to the original specification** |Set the time to revert to the original specification as needed, then click **OK**.<br><br><br>* The interval between the adjustment start time and the time to revert to the original specification must be greater than or equal to 1 hour.<br><br>* The interval between the adjustment start time and the previous time to revert to the original specification must be greater than or equal to 1 hour. |





</Tab>
<Tab zoneid="TogG02e1JF" title="Monthly">
<TabTitle>Monthly</TabTitle>


|**Parameter** |**Description** |
|---|---|
|**Perform operation** |This operation uses **Adjust the number of instance nodes** as an example. |
|**Target count** |Select the number of nodes for instance scaling from the dropdown list. The target count cannot be lower than the current number of nodes. |
|**Recurrence interval** |Select **Monthly** from the drop\-down list. The scaling operation repeats once per month within the effective period. If the scaling operation is not completed in the previous cycle, it is automatically skipped, and the system checks again in the next cycle to determine if scaling can be performed. |
|**Effective time** |Select the start time and end time for the instance node scaling to take effect. |
|**Adjustment start time** |Select the start time for scaling out as needed and click **OK**. The scaling start time cannot be earlier than the current time. |
|**Time to revert to the original specification** |Set the time to revert to the original specification as needed, then click **OK**.<br><br><br>* The interval between the adjustment start time and the time to revert to the original specification must be greater than or equal to 1 hour.<br><br>* The interval between the adjustment start time and the previous time to revert to the original specification must be greater than or equal to 1 hour.<br><br>* If the corresponding day does not exist in the current month (e.g., February 30), the operation will be skipped. |





</Tab>
</Tabs>



7. Click **OK**.


</Tab>
</Tabs>


<span id="DnVSope6"></span>
## View scheduled scaling events

You can view scaling up events within the last 30 days at most.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **veDB MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, set the time range for the query events as needed. The target events to view include **Event ID**, **Event status**, **Trigger value**, **Trigger condition**, **Rule type**, **Before/After adjustment**, **Trigger time** and **Last update time**.


Before/After triggering indicates the node specifications before and after scheduled scaling up is triggered.

<span id="TMx1puG0"></span>
## Modify scheduled scaling rules


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **veDB MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, select **Configure AutoOps rules** \> **Scheduled scaling**.

6. On the **Scheduled scaling** control panel, configure the relevant parameters. For detailed parameter configuration, see [Enable scheduled scaling](https://docs.byteplus.com/en/docs/DBW/scheduled-scaling-management?TagIDs=2&lang=en#tztS48Ny).

7. Click **OK**.


<span id="0Ryc8jlm"></span>
## Disable scheduled scaling


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **veDB MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, select **Configure AutoOps rules** \> **Scheduled scaling**.

6. On the **Scheduled scaling** panel, uncheck **Enable scheduled scaling**.

7. Click **OK**.
