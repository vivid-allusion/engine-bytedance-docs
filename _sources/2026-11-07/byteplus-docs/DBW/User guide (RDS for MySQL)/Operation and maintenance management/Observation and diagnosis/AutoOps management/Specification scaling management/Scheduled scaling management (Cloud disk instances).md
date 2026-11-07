---
title: "Scheduled scaling management (Cloud disk instances)"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/scheduled-scaling-management-cloud-disk-instances"
---

DBW provides scheduled scaling functionality, which is commonly used to handle predictable workload changes. You only need to configure rule\-based scaling policies, and DBW will automatically perform database scaling operations on schedule without manual intervention, achieving the optimal balance between performance and cost. This article describes how to configure scheduled scaling rules for cloud disk instances in the DBW console.

<span id="2VCpjRZd"></span>
## Prerequisites


* An RDS for MySQL cloud disk instance has been created. For detailed operations, see [Create a cloud disk instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1?lang=zh).

* The target instance has security control enabled, and the current account has the operation and maintenance read\-only or read/write permissions of the target instance. For more information, refer to [Enabling instance security control (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql), and [Applying for operation permissions (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket).


<span id="YNa7gMri"></span>
## Billing

Enabling the scheduled scaling feature itself incurs no additional fees. Once a specification change is triggered by a rule, the instance fees will be recalculated based on the new specifications and the current billing method. For more billing information, refer to [Billing items and prices of RDS for MySQL](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price).

<span id="MIc1tHvW"></span>
## Precautions


* **Applicability and configuration limits**

   * Applicable Instances: Only applicable to instances with a storage type of High performance cloud disk, Cloud ESSD FlexPL, or Cloud ESSD PL0. For specification details of RDS for MySQL instances, see [Product specifications](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications?lang=zh).

   * Policy Conflict: Scheduled scaling and automatic scaling (based on CPU utilization) cannot be configured simultaneously for the same instance. Only one can be enabled at a time. For more information about automatic scaling, see [Automatic scaling management (Cloud disk edition)](https://docs.byteplus.com/en/docs/DBW/auto-scaling-management-cloud-disk-instances?lang=zh).

   * This feature is in beta. To use it, [Submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

   * Specification constraints:

      * Scale\-up only: The target specification for scheduled scaling must be higher than the current specification. Selecting the same or a lower specification is not supported.

      * No cross\-type changes allowed: You cannot change the specification type during a specification change (e.g., General\-Purpose instances can only be changed to General\-Purpose, and Dedicated instances can only be changed to Dedicated).

   * Time interval restriction: The time interval between scheduled scale\-up and scale\-down (restoring to the original specification) must not be less than 1 hour.

   * Account balance requirement: Ensure your account balance is sufficient before use. Once a specification change is triggered, the instance fees will be recalculated based on the new specification. For more billing information about the product, see [Billing overview](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price).

* **Trigger conditions and validation mechanisms**

   * Scale\-up trigger condition: When the configured scale\-up time is reached, if the current instance specification is lower than the specified target specification, the system will automatically perform a scale\-up. If the current specification is greater than or equal to the target specification, no action will be taken.

   * Scale\-down (recovery) trigger condition: When the configured recovery time is reached, if the current instance specification exactly matches the scale\-up target specification recorded in the rule, the system will automatically perform a scale\-down. If the current specification does not match the target specification, no action will be taken.

   * Date validity check: Scheduled rules are triggered only when the specified date actually exists. If the configured date does not exist within the current cycle, the system will skip this cycle and will not postpone the execution. For example, if a rule is set to the 29th of each month, it will not be triggered in February of a non\-leap year. The system will continue to evaluate the rule in the next valid cycle.

   * Specification consistency check: When the recovery time is reached, if the current instance specification does not match the target specification set for scheduled scaling (e.g., if it was manually changed during the period), the system will not perform the recovery operation.

* **Business impact and risk warnings**

   * Transient connection interruptions: During scaling, database connections may experience brief interruptions. It is recommended to perform this operation during off\-peak hours and configure an automatic reconnection mechanism on the application side.

   * Interruption of DDL tasks: The scaling operation will interrupt ongoing OnlineDDL tasks. Please schedule the operation with caution.

* **Exception handling and rule circuit breaker mechanism**

   * Execution failure: If the scheduling fails to take effect due to insufficient underlying resources, unavailability of the target specification, or abnormal instance status, the system will automatically retry based on the scheduling policy.

   * Automatic rule closure (circuit breaker): If retries still fail, or the instance specification no longer meets the rule's expectations (e.g., due to manual configuration changes causing conflicts), the system will automatically close the rule and stop subsequent scheduling.

   * Manual intervention: After the rule is closed, handle the exception based on the failure reason in the "AutoOps event," then manually re\-enable or reconfigure the rule.


<span id="1PEls8W0"></span>
## Advantages


* Prepare resources in advance to avoid delayed responses:


Complete scaling up before traffic peaks to prevent service delays or failures caused by instance cold starts or application warm\-ups.


* Controllable and predictable costs

   * Resources scale according to plan, facilitating budget management and cost accounting.

   * Scale down during off\-peak hours to avoid resource waste.

* Simplified operation and maintenance logic

   * For businesses with strong cyclical patterns and clear trends, complex monitoring metrics are unnecessary.

   * Reduce frequent scaling caused by metric fluctuations, also known as oscillation issues.


<span id="xMDWIRUN"></span>
## Applicable scenarios

Scheduled scaling is suitable for business scenarios with predictable load patterns and known timeframes, as follows:


* Business systems with fixed working hours: For example, internal corporate systems like OA or HR platforms, which are used from 09:00 to 18:00 on weekdays and can be scaled down to minimal capacity at night.

* Education or exam platforms: Daily activities like classes or exams occur during fixed time slots, with traffic concentrated in specific periods, while weekends or holidays see almost no activity.

* E\-commerce mega promotion or flash sale event: Scale up 5\-10 minutes before the event starts, and scale down immediately after the event ends.

* Batch data processing tasks: Batch processing jobs are executed daily at 2:00 AM. Computing nodes can be scheduled to start, and resources are released upon task completion.

* Live streaming or media platforms: For example, for programs like Xinwen Lianbo airing at 7 PM daily, pre\-scaling is recommended to handle the concentrated viewer influx.

* Development and testing environments: Enable during workdays and automatically shut down after hours or on weekends to reduce costs.


Scheduled scaling achieves efficient resource allocation with minimal operational overhead, ensuring optimal performance while significantly lowering cloud service expenses.

<span id="JysvOAjO"></span>
## Enable scheduled scaling


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, select **Configure AutoOps rules** \> **Compute scaling**.

6. In the **Configure AutoOps rules \- Compute scaling** panel, configure the following parameters.



|**Parameter** ||**Description** |
|---|---|---|
|**Scaling method** ||This topic takes **scheduled scaling** as an example. |
|**Feature switch** ||Click **Enable**. |
|**Target specification** ||Set the target scale\-up specifications for the primary node and read\-only nodes as needed. The scale\-up specifications for the primary node and read\-only nodes can be configured independently. |
|**Recurrence interval**<br><br> |**Execute only once** |* **Repetition cycle**: Select **Execute run once** from the drop\-down list to perform the scaling once without repetition.<br><br>* **Adjustment start time**: Select the start time for scaling up as needed and click **OK**. The scaling start time cannot be earlier than the current time.<br><br>* **Time to revert to the original specification**: Set the time to revert to the original specification as needed, then click **OK**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The interval between the adjustment start time and the time to revert to the original specification must be greater than or equal to 1 hour.</div><br> |
||**By day** |* **Repetition cycle**: Select By day from the drop\-down list to repeat scaling operations **daily**. If the scaling operation is not completed within the previous cycle, it will be automatically skipped, and the system will re\-evaluate whether to perform scaling in the next cycle.<br><br>* **Effective time**: Select the effective start and end dates as needed.<br><br>* **Adjustment start time**: Select the start time for scaling up as needed and click **OK**.<br><br>* **Time to revert to the original specification**: Set the time to revert to the original specification as needed, then click **OK**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The interval between the adjustment start time and the time to revert to the original specification must be greater than or equal to 1 hour.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The interval between the adjustment start time and the previous time to revert to the original specification must be greater than or equal to 1 hour.</div><br> |
||**Week** |* **Repetition cycle**: Select By day from the drop\-down list to repeat scaling operations **weekly**. If the scaling operation is not completed within the previous cycle, it will be automatically skipped, and the system will re\-evaluate whether to perform scaling in the next cycle.<br><br>* **Effective time**: Select the effective start and end dates as needed.<br><br>* **Adjustment start time**: Select the start time for scaling up as needed and click **OK**.<br><br>* **Time to revert to the original specification**: Set the time to revert to the original specification as needed, then click **OK**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The interval between the adjustment start time and the time to revert to the original specification must be greater than or equal to 1 hour.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The interval between the adjustment start time and the previous time to revert to the original specification must be greater than or equal to 1 hour.</div><br> |
||**Monthly** |* **Repetition cycle**: Select By day from the drop\-down list to repeat scaling operations **monthly**. If the scaling operation is not completed within the previous cycle, it will be automatically skipped, and the system will re\-evaluate whether to perform scaling in the next cycle.<br><br>* **Effective time**: Select the effective start and end dates as needed.<br><br>* **Adjustment start time**: Select the start time for scaling up as needed and click **OK**.<br><br>* **Time to revert to the original specification**: Set the time to revert to the original specification as needed, then click **OK**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The interval between the adjustment start time and the time to revert to the original specification must be greater than or equal to 1 hour.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The interval between the adjustment start time and the previous time to revert to the original specification must be greater than or equal to 1 hour.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the corresponding day does not exist in the current month (e.g., February 30), the operation will be skipped.</div><br> |



7. Click **OK**.


<span id="Ytq9aVdJ"></span>
## Modify scheduled scaling


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, select **Configure AutoOps rules** \> **Compute scaling**.

6. In the **Configure AutoOps rules \- Compute scaling** panel, configure the following parameters.



|**Parameter** ||**Description** |
|---|---|---|
|**Target specification** ||Set the target scale\-up specifications for the primary node and read\-only nodes as needed. The scale\-up specifications for the primary node and read\-only nodes can be configured independently. |
|**Recurrence interval**<br><br> |**Execute only once** |* **Repetition cycle**: Select **Execute run once** from the drop\-down list to perform the scaling once without repetition.<br><br>* **Adjustment start time**: Select the start time for scaling up as needed and click **OK**. The scaling start time cannot be earlier than the current time.<br><br>* **Time to revert to the original specification**: Set the time to revert to the original specification as needed, then click **OK**.<br><br><br>The interval between the adjustment start time and the time to revert to the original specification must be greater than or equal to 1 hour. |
||**By day** |* **Repetition cycle**: Select By day from the drop\-down list to repeat scaling operations **daily**. If the scaling operation is not completed within the previous cycle, it will be automatically skipped, and the system will re\-evaluate whether to perform scaling in the next cycle.<br><br>* **Effective time**: Select the effective start and end dates as needed.<br><br>* **Adjustment start time**: Select the start time for scaling up as needed and click **OK**.<br><br>* **Time to revert to the original specification**: Set the time to revert to the original specification as needed, then click **OK**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The interval between the adjustment start time and the time to revert to the original specification must be greater than or equal to 1 hour.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The interval between the adjustment start time and the previous time to revert to the original specification must be greater than or equal to 1 hour.</div><br> |
||**Week** |* **Repetition cycle**: Select By day from the drop\-down list to repeat scaling operations **weekly**. If the scaling operation is not completed within the previous cycle, it will be automatically skipped, and the system will re\-evaluate whether to perform scaling in the next cycle.<br><br>* **Effective time**: Select the effective start and end dates as needed.<br><br>* **Adjustment start time**: Select the start time for scaling up as needed and click **OK**.<br><br>* **Time to revert to the original specification**: Set the time to revert to the original specification as needed, then click **OK**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The interval between the adjustment start time and the time to revert to the original specification must be greater than or equal to 1 hour.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The interval between the adjustment start time and the previous time to revert to the original specification must be greater than or equal to 1 hour.</div><br> |
||**Monthly** |* **Repetition cycle**: Select By day from the drop\-down list to repeat scaling operations **monthly**. If the scaling operation is not completed within the previous cycle, it will be automatically skipped, and the system will re\-evaluate whether to perform scaling in the next cycle.<br><br>* **Effective time**: Select the effective start and end dates as needed.<br><br>* **Adjustment start time**: Select the start time for scaling up as needed and click **OK**.<br><br>* **Time to revert to the original specification**: Set the time to revert to the original specification as needed, then click **OK**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The interval between the adjustment start time and the time to revert to the original specification must be greater than or equal to 1 hour.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The interval between the adjustment start time and the previous time to revert to the original specification must be greater than or equal to 1 hour.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the corresponding day does not exist in the current month (e.g., February 30), the operation will be skipped.</div><br> |



7. Click **OK**.


<span id="xuCAlhJY"></span>
## Disable scheduled scaling


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, select **Configure AutoOps rules** \> **Compute scaling**.

6. On the **Configure AutoOps rules \- Compute scaling** panel, click **Close** after **Function switch**.

7. Click **OK**.


<span id="uDJXm7XQ"></span>
## View scheduled scaling events

You can view scaling up events within the last 30 days at most.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the Automated O&M Events subtab of the **AutoOps** tab, set the time range for the query events as needed. The target events to view include **Event ID**, **Event status**, **Trigger value**, **Trigger condition**, **Rule type**, **Before/After adjustment**, **Trigger time** and **Last update time**.


Before/After triggering indicates the node specifications before and after scheduled scaling up is triggered.

<span id="R0xa3Ilg"></span>
## FAQ

Q: I have configured scheduled scaling. Why did the rule become invalid after I manually changed the instance specification?

A: Scheduled scaling requires the instance specification to remain consistent with the configured specification at the time of triggering. After a manual specification change causes the instance specification to differ, the rule will be deemed inconsistent and will not take effect. You need to reconfigure the scheduled scaling rule.
