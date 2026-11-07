---
title: "Storage space expansion management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Storage_expansion_management_pg"
---

Database Workshop (DBW) provides the automatic scaling up feature, which can help you respond quickly and perform scaling up operations when your business grows rapidly, so as to ensure that your system can run stably and meet the ever\-increasing business needs. This article describes how to enable, view, modify, and close automatic scaling up rules.

<span id="GvzspGQO"></span>
## Prerequisites


* An RDS for PostgreSQL instance has been created. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This feature is not supported when the instance status is creating, recovering, importing, error, deleted, terminated, waiting for payment, billing suspension in progress, billing restoring, billing reclaiming or reconstructing.   </div>
   

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-control), and [Applying for operation permissions (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/Create_operation_permission_ticket).


<span id="u5Wqdi4x"></span>
## Precautions


* Currently, only automatic scaling up of instance storage space is supported. After a rule is triggered, automatic scaling up is usually completed in about 10 minutes. After automatic scaling up is complete, DBW will not perform automatic scaling down according to business scenarios. Therefore, if scaling down is needed, you must perform the operation manually. For details, see [Change configuration](https://docs.byteplus.com/en/docs/RDS_for_PG/standard_instance_specification_modification).

* Each expansion step is Min (maximum available storage space, twice the current storage space); if the instance's current storage space is 500 GB and the maximum available storage space is 800 GB, then the expansion will be to 800 GB.

* Automatic disk expansion cannot guarantee successful expansion in all scenarios due to physical limitations of local SSDs, insufficient host storage space, insufficient account balance, and other reasons. If expansion fails, the system will suspend the automatic scaling up task.

* Performing configuration change operations on the instance may prevent the instance from performing automatic scaling up. For example, in an automatic capacity expansion configuration, the maximum capacity can be expanded to 1500 GB. However, if you change the storage space of the instance to 1600 GB, the automatic capacity expansion rule will not be triggered. You can modify the automatic expansion rules to trigger them normally; if you do not need this function, you can disable it yourself.

* If the automatic expansion fails, the system will suspend subsequent expansion tasks until the cause of the failure is detected and resolved.

* During automatic scaling up, most operations related to databases, accounts, and networks cannot be performed.

* Automatic scaling up does not cause changes to the instance ID and connection address.

* RDS for PostgreSQL instances now support storage space exceeding 3000 GB. However, this capacity level is currently a whitelisted feature. To use larger storage specifications, [Submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

   If your instance has automatic scaling up enabled, after applying for this feature, be sure to manually increase the upper limit of the scaling rule. Otherwise, the rule's upper limit will remain at the default 3000 GB, and the instance will be unable to scale to the newly requested storage space.

* Before using the AutoOps function, make sure that there is sufficient balance in the account to support changing the instance configuration. For more billing information about the product, see [Billing overview](https://docs.byteplus.com/en/docs/RDS_for_PG/price_overview).


<span id="C5BBqoai"></span>
## Enable automatic scaling up rules


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for PostgreSQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Configure AutoOps rules** under **Storage expansion**.

6. On the **Configure AutoOps rules** panel, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Automatic expansion** |Select **Enable auto scaling** to enable the automatic scaling up function. |
   |**Scaling up type** |Currently, only selecting **Storage space** is supported, and modification is not supported. |
   |**Available storage space** |* Available storage space percentage threshold: Set the available storage space percentage threshold as required. The unit is percentage, and the value range is 10% ~ 50%. The scale\-up upper limit configuration range is 20 GB ~ 12000 GB.<br><br>* Available storage space threshold: Set the maximum storage space threshold for scaling up the instance as needed. When the available storage space percentage of the instance is less than or equal to the set threshold, the instance will start scaling up. The lower limit of the instance storage space threshold is the instance's current used storage space + 20 GB, and the upper limit is the upper limit of the storage space value range corresponding to the instance primary node specification, in GB. For more information about the range of storage space values that can be selected for different specifications, see [Product specifications](https://docs.byteplus.com/en/docs/RDS_for_PG/product_specifications).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Storage capacity over 3000 GB is currently an allowlisted feature, available only in the China (Beijing), China (Shanghai), and China (Guangzhou) regions. To use it, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to contact technical support to apply for usage.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For example, if you set the threshold for the available storage space percentage to <strong>50%</strong>, and the available instance storage space to <strong>600 GB</strong>, then when the available storage space percentage of the instance is less than or equal to 50%, the instance will start scaling up and can be changed to a maximum of 600 GB.</div><br> |
   

7. Click **OK**.


<span id="fQ1AnMxw"></span>
## View the triggered scaling up event

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can view scaling up events within the last 30 days at most.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for PostgreSQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, set the time range for the query events as needed. The target events to view include **Event ID**, **Event status**, **Trigger value**, **Trigger condition**, **Rule type**, **Before/After adjustment**, **Trigger time** and **Last update time**.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before/After adjustment represents the storage space before and after triggering automatic scaling up.</div>


<span id="LNaV0ylk"></span>
## Modify auto scaling rules


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for PostgreSQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Configure AutoOps rules** under **Storage expansion**.

6. On the **Configure AutoOps rules** panel, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Automatic expansion** |Select **Enable auto scaling** to enable the automatic scaling up function. |
   |**Scaling up type** |Currently, only selecting **Storage space** is supported, and modification is not supported. |
   |**Available storage space** |* Available storage space percentage threshold: Set the available storage space percentage threshold as required. The unit is percentage, and the value range is 10% ~ 50%. The scale\-up upper limit configuration range is 20 GB ~ 12000 GB.<br><br>* Available storage space threshold: Set the maximum storage space threshold for scaling up the instance as needed. When the available storage space percentage of the instance is less than or equal to the set threshold, the instance will start scaling up. The lower limit of the instance storage space threshold is the instance's current used storage space + 20 GB, and the upper limit is the upper limit of the storage space value range corresponding to the instance primary node specification, in GB. For more information about the range of storage space values that can be selected for different specifications, see [Product specifications](https://docs.byteplus.com/en/docs/RDS_for_PG/product_specifications).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">For example, if you set the threshold for the available storage space percentage to <strong>50%</strong>, and the available instance storage space to <strong>600 GB</strong>, then when the available storage space percentage of the instance is less than or equal to 50%, the instance will start scaling up and can be changed to a maximum of 600 GB.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Storage capacity over 3000 GB is currently an allowlisted feature, available only in the China (Beijing), China (Shanghai), and China (Guangzhou) regions. To use it, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to contact technical support to apply for usage.</div><br> |
   

7. Click **OK**.


<span id="kMnEdOXv"></span>
## Disable auto scaling rules


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for PostgreSQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Configure AutoOps rules** under **Storage expansion**.

6. In the **Configure AutoOps rules** control panel, clear **Enable auto scaling**.

7. Click **OK**.


<span id="vNk1Q8iA"></span>
## FAQs


|**Error** |**reason** |**Solution** |
|---|---|---|
|Pre\-check failed: Exceeds the maximum storage space that you configured, and the system will not be able to complete the automatic scaling up normally. |The instance specifications are greater than the configured auto\-scaling available storage space threshold. |You can adjust the available storage space threshold for automatic scaling up as appropriate. If there are any anomalies, relevant prompts will appear after you confirm the change. You can make corresponding modifications based on the specific prompts. For detailed operations, see [Modifying scaling up rules](https://docs.byteplus.com/en/docs/DBW/Storage_expansion_management_pg#LNaV0ylk). |
|Pre\-check failed: The host where the node is located has insufficient storage space, and the system will not be able to complete automatic scaling up normally. |The disk does not meet the local scaling up rules. |We suggest that you change the storage space of the target instance. After the change is complete, the system will select a host with more remaining storage space. If the error persists, we suggest that you readjust the instance's storage space. For details, see [Change configuration](https://docs.byteplus.com/en/docs/RDS_for_PG/standard_instance_specification_modification).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After scaling the instance, you can check for any exceptions on the Auto Scaling page. If there are any exceptions, hover your mouse over the event status to view the specific cause of the error and make corrections based on the prompts. For detailed operations, see Viewing triggered scaling up event.</div><br> |
|Pre\-check failed: Insufficient account balance. The system will not be able to automatically scale up. |Insufficient account balance |You need to recharge the current account to ensure sufficient account resources.   |
|Pre\-check failed: The expansion conditions are not met, and the system can not complete automatic scaling up normally. |The instance may be in the process of modifying. |If the instance status is not running or changing, the system will automatically record the expansion failure event during the automatic expansion process. If the instance is running, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff for troubleshooting and identifying the specific issue. |
