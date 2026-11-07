---
title: "Storage space expansion management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/automatic-expansion-management"
---

Database Workshop (DBW) provides the automatic scaling up feature, which can help you respond quickly and perform scaling up operations when your business grows rapidly, so as to ensure that your system can run stably and meet the ever\-increasing business needs. This article describes how to enable, view, modify, and close automatic scaling up rules.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance for RDS for MySQL has been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This feature is not supported when the instance status is creating, recovering, importing, error, deleted, terminated, waiting for payment, billing suspension in progress, billing restoring, billing reclaiming or reconstructing.   </div>
   

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql), and [Applying for operation permissions (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Currently, only automatic in\-place scaling up of instance storage space is supported. After a rule is triggered, automatic scaling up is usually completed in about 5 minutes.

* Each expansion amount is Max(5 GB, 15% of the current storage space), rounded up to the nearest multiple of 5 GB. If the total instance space is <50 GB and the available space is <10%, the expansion amount is 10 GB.

* Automatic disk expansion cannot guarantee successful expansion in all scenarios due to physical limitations of local SSDs, insufficient host storage space, insufficient account balance, and other reasons. If the expansion fails, the system will suspend the automatic expansion task. At the same time, RDS for MySQL will report the instance storage automatic expansion failure event to CloudMonitor. You can configure event rules for such events to obtain event information as soon as possible and handle the problem in a timely manner. For more details about view events and configuring create event rules, see [View events](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_an_event) and [Create event rules](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Creating_event_policy).

* Performing configuration change operations on the instance may prevent the instance from performing automatic scaling up. For example, in an automatic capacity expansion configuration, the maximum capacity can be expanded to 1500 GB. However, if you change the storage space of the instance to 1600 GB, the automatic capacity expansion rule will not be triggered. You can modify the automatic expansion rules to trigger them normally; if you do not need this function, you can disable it yourself.

* If the automatic expansion fails, the system will suspend subsequent expansion tasks until the cause of the failure is detected and resolved.

* During automatic scaling up, most operations related to databases, accounts, and networks cannot be performed.

* Automatic scaling up does not cause changes to the instance ID and connection address.

* Before using the AutoOps function, make sure that there is sufficient balance in the account to support changing the instance configuration. For more billing information about the product, see [Billing overview](https://docs.byteplus.com/en/docs/RDS_for_MySQL/price_overview).

* To avoid frequently triggered storage expansions, the system sets a 5\-minute cooldown period. This represents the minimum time interval from the completion of one expansion to when the next expansion is allowed.


<span id=".5byA5ZCv6Ieq5Yqo5omp5a656KeE5YiZ"></span>
## Enable automatic scaling up rules


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Configure AutoOps rules**.

6. On the **Configure AutoOps rules** panel, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Automatic expansion** |Select **Enable auto scaling** to enable the automatic scaling up function. |
   |**Scaling up type** |Currently, only selecting **Storage space** is supported, and modification is not supported. |
   |**Available storage space** |* Storage space type: Specifies the node scope used as the basis for scaling judgment. Valid values:<br><br>   * **Available storage space on the primary node** (Default): Scaling is triggered based solely on the available storage space of the primary node.<br><br>   * **Available storage space on primary/standby nodes**: Monitors both the primary and standby nodes. Scaling is triggered if any node meets the expansion condition.<br><br>* Available storage space percentage threshold: The system initiates the scaling\-up process when the available storage space percentage of the selected node is less than or equal to this threshold.<br><br><br>Set the storage usage threshold for triggering automatic scaling, in percentage (%), with a range of 10% to 50%. The upper limit for storage capacity after scaling ranges from 180 GB to 3000 GB.<br><br><br>* Available storage space threshold (absolute value): When the available storage space percentage of the instance is less than or equal to the available storage space percentage threshold, scaling is triggered, up to the maximum value you set for the available storage space threshold.<br><br>   * Minimum value: Current instance storage capacity + 20 GB.<br><br>   * Maximum value: The maximum storage capacity supported by the primary node specification.<br><br><br>For details on the selectable storage space ranges for different specifications, refer to [Product Specifications](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications?lang=en).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For example, if you set the available storage space percentage threshold to <strong>40%</strong> and the available instance storage space to <strong>600 GB</strong>, the instance will start scaling up and can be changed to a maximum of 600 GB when its available storage space percentage is less than or equal to 40%.</div><br> |
   

7. Click **OK**.


<span id=".5p-l55yL6Kem5Y-R5omp5a655LqL5Lu2"></span>
## View the triggered scaling up event

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can view scaling up events within the last 30 days at most.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, set the time range for the query events as needed. The target events to view include **Event ID**, **Event status**, **Trigger value**, **Trigger condition**, **Rule type**, **Before/After adjustment**, and **Trigger time**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Before/After triggering indicates the node specifications before and after automatic scaling up is triggered.   </div>
   

<span id=".5L-u5pS56Ieq5Yqo5omp5a656KeE5YiZ"></span>
## Modify auto scaling rules


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Configure AutoOps rules**.

6. On the **Configure AutoOps rules** panel, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Automatic expansion** |Select **Enable auto scaling** to enable the automatic scaling up function. |
   |**Scaling up type** |Currently, only selecting **Storage space** is supported, and modification is not supported. |
   |**Available storage space** |* Storage space type: Specifies the node scope used as the basis for scaling judgment. Valid values:<br><br>   * **Available storage space on the primary node** (Default): Scaling is triggered based solely on the available storage space of the primary node.<br><br>   * **Available storage space on primary/standby nodes**: Monitors both the primary and standby nodes. Scaling is triggered if any node meets the expansion condition.<br><br>* Available storage space percentage threshold: The system initiates the scaling\-up process when the available storage space percentage of the selected node is less than or equal to this threshold.<br><br><br>Set the storage usage threshold for triggering automatic scaling, in percentage (%), with a range of 10% to 50%. The upper limit for storage capacity after scaling ranges from 180 GB to 3000 GB.<br><br><br>* Available storage space threshold (absolute value): When the available storage space percentage of the instance is less than or equal to the available storage space percentage threshold, scaling is triggered, up to the maximum value you set for the available storage space threshold.<br><br>   * Minimum value: Current instance storage capacity + 20 GB.<br><br>   * Maximum value: The maximum storage capacity supported by the primary node specification.<br><br><br>For details on the selectable storage space ranges for different specifications, refer to [Product Specifications](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications?lang=en).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For example, if you set the available storage space percentage threshold to <strong>40%</strong> and the available instance storage space to <strong>600 GB</strong>, the instance will start scaling up and can be changed to a maximum of 600 GB when its available storage space percentage is less than or equal to 40%.</div><br> |
   

7. Click **OK**.


<span id=".5YWz6Zet6Ieq5Yqo5omp5a656KeE5YiZ"></span>
## Disable auto scaling rules


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Configure AutoOps rules**.

6. In the **Configure AutoOps rules** control panel, clear **Enable auto scaling**.

7. Click **OK**.


<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQs


|**Error** |**reason** |**Solution** |
|---|---|---|
|Pre\-check failed: Exceeds the maximum storage space that you configured, and the system will not be able to complete the automatic scaling up normally. |The instance specifications are greater than the configured auto\-scaling available storage space threshold. |You can adjust the available storage space threshold for automatic scaling up as appropriate. If there are any anomalies, relevant prompts will appear after you confirm the change. You can make corresponding modifications based on the specific prompts. For detailed operations, see [Modifying scaling up rules](https://docs.byteplus.com/en/docs/DBW/automatic-expansion-management#.5L-u5pS56Ieq5Yqo5omp5a656KeE5YiZ). |
|Pre\-check failed: The host where the node is located has insufficient storage space, and the system will not be able to complete automatic scaling up normally. |The disk does not meet the local scaling up rules. |We suggest that you change the storage space of the target instance. After the change is complete, the system will select a host with more remaining storage space. If the error persists, we suggest that you readjust the instance's storage space. For details, see [Change configuration](https://docs.byteplus.com/en/docs/RDS_for_MySQL/standard_instance_specification_modification).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After scaling the instance, you can check for any exceptions on the Auto Scaling page. If there are any exceptions, hover your mouse over the event status to view the specific cause of the error and make corrections based on the prompts. For detailed operations, see <a href="https://docs.byteplus.com/en/docs/DBW/automatic-expansion-management#.5p-l55yL6Kem5Y-R5omp5a655LqL5Lu2">Viewing triggered scaling up event</a>.</div><br> |
|Pre\-check failed: Insufficient account balance. The system will not be able to automatically scale up. |Insufficient account balance |You need to recharge the current account to ensure sufficient account resources. For detailed operations, see [Recharge](https://docs.byteplus.com/en/docs/6269/100434). |
|Pre\-check failed: The expansion conditions are not met, and the system can not complete automatic scaling up normally. |The instance may be in the process of modifying. |If the instance status is not running or changing, the system will automatically record the expansion failure event during the automatic expansion process. If the instance is running, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff for troubleshooting and identifying the specific issue. |


&nbsp;
