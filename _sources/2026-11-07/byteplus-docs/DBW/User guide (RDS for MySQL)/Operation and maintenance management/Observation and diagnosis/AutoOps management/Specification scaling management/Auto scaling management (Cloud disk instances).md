---
title: "Auto scaling management (Cloud disk instances)"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/auto-scaling-management-cloud-disk-instances"
---

DBW provides an automatic specification scaling management feature for RDS for MySQL (Cloud Disk) instances. Based on the instance CPU threshold and its duration, this feature dynamically adjusts the instance specification. This reduces the frequency of manual configuration changes, optimizing usage costs while ensuring performance. This topic describes how to manage automatic scaling for cloud disk instances in the DBW console.

<span id="5hYGzzAW"></span>
## Prerequisites


* An RDS for MySQL cloud disk instance has been created. For detailed operations, see [Create a cloud disk instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1?lang=zh).

* The target instance has security control enabled, and the current account has the operation and maintenance read\-only or read/write permissions of the target instance. For more information, refer to [Enabling instance security control (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql), and [Applying for operation permissions (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket).


<span id="64elzPIx"></span>
## Billing

Enable auto scaling feature itself incurs no additional fees. After a specification change is triggered by a rule, the instance fees will be recalculated based on the new specification and the current billing method of the instance. For more billing information, refer to [Billing items and prices of RDS for MySQL](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price).

<span id="nTSkY4Vg"></span>
## Precautions


* **Usage and mutual exclusion rules: ** 

   * Applicable Instances: This feature is only available for instances with High performance cloud disk, Cloud ESSD FlexPL, or Cloud ESSD PL0 storage types. For detailed information on instance specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications?lang=zh).

   * Policy mutual exclusion: Automatic scaling and scheduled scaling cannot be configured simultaneously for the same instance. For more information about scheduled scaling, see [Scheduled scaling management (Cloud disk edition)](https://docs.byteplus.com/en/docs/DBW/scheduled-scaling-management-cloud-disk-instances?lang=zh).

   * This feature is in beta. To use it, [Submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

* **Business impact and risk warnings:** 

   * Risk of transient connection interruptions: During the scaling process, the instance may experience brief disconnections (1 to 3 times) or enter a second\-level read\-only state. It is recommended to configure automatic retry and reconnection mechanisms for your application to ensure business continuity.

   * Interruption of DDL tasks: The scaling operation will interrupt ongoing OnlineDDL tasks. Please schedule the operation with caution. For more information about OnlineDDL, see [Create a Lock-Free DDL Ticket (OnlineDDL)](https://docs.byteplus.com/en/docs/DBW/creating-a-lock-free-structural-change-ticket-onlineddl-ticket-for-mysql?lang=zh).

   * Risk of execution failure: After an automatic scaling rule is triggered, the task may fail or not take effect if the instance state does not support the change, underlying resources are insufficient, the target specification is unavailable, or safety conditions (such as memory) are not met during scale\-down. The final success depends on the actual execution result of the task. Please monitor the instance status and automatic O&M events in a timely manner.

   * Unidirectional policy description: If only automatic scale\-up or automatic scale\-down is enabled for an instance, the instance will not automatically revert to its original specification after the corresponding operation is completed.

* **Configuration and specification limits:** 

   * Account balance requirement: Before using the automatic O&M feature, ensure that your account has sufficient balance to support instance specification changes. For more billing information, see [Billing overview](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price).

   * Specification upgrade constraints: The CPU core count of the selected new specification must be greater than the current specification, and the memory size must be greater than or equal to the current specification.

   * Read\-only node change restrictions: When an instance has multiple read\-only nodes, the system will validate whether a change is triggered according to the following rules:

      * Scale\-out limit: If the current specification of a read\-only node is ≥ the set maximum scalable specification, scale\-out is not triggered.

      * Scale\-in limit: If the current specification of a read\-only node is ≤ the set minimum scalable specification, scale\-in is not triggered.

      * Configuration conflict validation: Ensure the maximum scalable specification is higher than the minimum scalable specification. Otherwise, the configuration may not be saved or the rules may not function properly.

* **Relationship between primary instance and read\-only instances:** 

   * Independent policies: The auto\-scaling configurations and specification limits for primary/standby nodes and read\-only nodes are independent and do not affect each other.

   * Synchronization with primary/standby switchover: After a primary/standby switchover, the system continues to determine whether a specification adjustment is needed based on the post\-switchover node role, current specification, and auto\-scaling rules.

   * Independent judgment for read\-only nodes: Read\-only nodes are unaffected by primary/standby switchovers. The system independently determines whether to trigger scale\-out or scale\-in based on the read\-only node's current specification, monitoring metrics, and rule configuration.


<span id="ablV4qpm"></span>
## Advantages


* **High Availability and Business Continuity Assurance**

   * Automatic response to sudden load: When CPU usage exceeds the preset threshold (e.g., 90%), the system automatically scales out to a higher specification to avoid service degradation or interruption.

   * Automatic adaptation for primary\-standby switchover: If a primary instance triggers a primary\-standby switchover after scaling out, the new primary instance continues to automatically adjust its specification based on load, ensuring performance consistency in high\-availability architectures.

* **Cost Optimization and Improved Resource Utilization**

   * Pay\-as\-you\-go to avoid idle waste: Automatically retract specifications during business troughs, keeping resource consumption at the lowest level, especially suitable for businesses with clear peaks and valleys (e.g., e\-commerce promotions, game server launches).

   * Supports cost\-saving shutdown mode: Retains cloud disk data and suspends computing resources during scaling in; allows rapid recovery during scaling out, significantly reducing scaling time and the cost of repeated instance creation.

* **Enhanced Operational Efficiency and Automation Capabilities**

   * Fully automated closed\-loop management reduces manual intervention risks: The entire process from "monitoring → scaling out → retracting" is automated, requiring no manual intervention, making it particularly suitable for complex environments with multiple instances and services.

   * Multi\-dimensional observability: Provides capabilities such as scaling activity logs, monitoring metrics, and anomaly detection, facilitating quick root cause analysis and improving troubleshooting efficiency.

* **Architectural Flexibility and Scalability Support**

   * Supports independent scaling of nodes: You can set policies for the primary node and read\-only nodes separately to meet the evolving needs of complex architectures such as read/write separation and sharding.


<span id="vYjo66j2"></span>
## Enable auto scaling

Currently supports enabling only automatic scaling up, only automatic scaling down, or both automatic scaling up and down.


<Tabs>
<Tab zoneid="ol6eSezDq5" title="Only enable automatic expansion">
<TabTitle>Only enable automatic expansion</TabTitle>

If automatic scaling up is enabled for an instance but automatic scaling down is not, the instance will not perform scaling down after scaling up when the conditions are met.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, select **Configure AutoOps rules** \> **Compute scaling**.

6. On the **Configure AutoOps rules \- Compute scaling** panel, configure the **Auto scaling** parameters to enable only auto scaling up.



|**Parameter** |**Description** |
|---|---|
|**Scaling method** |This article uses **Auto scaling** as an example. Automatic and manual scaling cannot be configured simultaneously. |
|**Feature switch** |This example uses **Only enable automatic scaling up** as a case. |
|**Master and standby node expansion configuration** |Click **Enable** and configure the parameters for master and standby node scaling out as follows:<br><br><br>* **Judgment indicator**: Average CPU usage.<br><br>* **Effective condition**: The indicator remains above the set percentage threshold throughout the specified duration.<br><br>* **Execution action**: Scale up step by step according to the specification list until the maximum specification you set is reached.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For example: If you set the average CPU usage to 90%, the duration to 30 minutes, and the instance specification to 4 cores 16 GiB, then if the instance's average CPU usage remains at or above 90% for 30 minutes, the specification of the master and standby nodes will scale up step by step until reaching 4 cores 16 GiB.</div><br> |
|**Read\-only node scaling configuration** |Click **Enable**, then configure the read\-only node scaling parameters as follows:<br><br><br>* **Judgment indicator**: Average CPU usage.<br><br>* **Effective condition**: When a read\-only node's indicator remains above the set percentage threshold throughout the specified duration.<br><br>* **Execution action**: Scale up step by step according to the specification list until the maximum specification you set is reached.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Scaling is triggered for a read\-only node if any read\-only node in the instance meets the condition.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the set maximum scaling specification is less than the current maximum read\-only node specification of the instance, this rule does not take effect.</div><br> |
|**Read\-only node exemption configuration** |Select the target nodes from the list to which the automatic scaling up rules do not apply, keeping their specifications fixed.<br><br>This parameter is available when you enable the read\-only node scaling configuration. |



7. Click **OK**.


</Tab>
<Tab zoneid="Y2pufDMO92" title="Only enable automatic scaling">
<TabTitle>Only enable automatic scaling</TabTitle>

If the instance has not enabled auto scaling, even if auto scaling down rules are configured, the instance will not perform any scaling down operations. Therefore, before enabling auto scaling down, you must enable auto scaling configuration.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Configure AutoOps rules**.

6. On the **Configure AutoOps rules \- Compute scaling** panel, configure parameters to **Only enable automatic scaling** for auto scaling.



|**Parameter** |**Description** |
|---|---|
|**Scaling method** |This article uses **Auto scaling** as an example. Automatic and manual scaling cannot be configured simultaneously. |
|**Feature switch** |This example uses **Only enable automatic scaling down** as a case. |
|**Primary and standby node scaling configuration** |Click **Enable**, then configure the parameters for master and standby node scaling down as follows:<br><br><br>* **Judgment indicator**: Average CPU usage.<br><br>* **Effective condition**: The indicator remains below the set percentage threshold for the specified duration.<br><br>* **Execution action**: Scale down step by step according to the specification list until the minimum specification you set is reached.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">For example, if you set the average CPU usage threshold to 30%, the duration to 30 minutes, and the instance specification to 4 cores 16 GiB, then if the instance's average CPU usage remains at 30% or below for 30 minutes, the specification of the master and standby nodes will be gradually reduced until it reaches 4 cores 16 GiB.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The minimum specification you configure cannot be smaller than the instance's own specification.</div><br> |
|**Read\-only node scaling configuration** |Click **Enable**, then configure the parameters for scaling down the read\-only nodes as follows:<br><br><br>* **Judgment indicator**: Average CPU usage.<br><br>* **Effective condition**: When a read\-only node's indicator remains below the set percentage threshold throughout the specified duration.<br><br>* **Execution action**: Scale down step by step according to the specification list until the minimum specification you set is reached.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Scaling is triggered for a read\-only node if any read\-only node in the instance meets the condition.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If a read\-only node's minimum scaling specification is less than the current minimum scaling specification, that read\-only node will not trigger a change.</div><br> |
|**Read\-only node exemption configuration** |Select the target nodes from the list to which the automatic scaling down rules do not apply, keeping their specifications fixed. |



7. Click **OK**.


</Tab>
<Tab zoneid="ycZhgKRNjA" title="Enable Automatic scale-up and scale-down">
<TabTitle>Enable Automatic scale-up and scale-down</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Configure AutoOps rules**.

6. In the **Configure AutoOps rules \- Compute scaling** panel, configure **Auto scaling** and enable the automatic scaling up and automatic scaling down parameters.



|**Parameter** |**Description** |
|---|---|
|**Scaling method** |This article uses **Auto scaling** as an example. Automatic and manual scaling cannot be configured simultaneously. |
|**Feature switch** |This example uses **Only enable automatic scaling down** as a case. |
|**Master and standby node expansion configuration** |Click **Enable**, then configure the parameter information for master and standby node scaling as follows:<br><br><br>* **Judgment indicator**: Average CPU usage.<br><br>* **Effective condition**: The indicator remains above the set percentage threshold throughout the specified duration.<br><br>* **Execution action**: Scale up step by step according to the specification list until the maximum specification you set is reached.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For example: If you set the average CPU usage to 90%, the duration to 30 minutes, and the instance specification to 4 cores 16 GiB, then if the instance's average CPU usage remains at or above 90% for 30 minutes, the specification of the master and standby nodes will scale up step by step until reaching 4 cores 16 GiB.</div><br> |
|**Read\-only node scaling configuration** |Click **Enable**, then configure the read\-only node scaling parameters as follows:<br><br><br>* **Judgment indicator**: Average CPU usage.<br><br>* **Effective condition**: When a read\-only node's indicator remains above the set percentage threshold throughout the specified duration.<br><br>* **Execution action**: Scale up step by step according to the specification list until the maximum specification you set is reached.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Scaling is triggered for a read\-only node if any read\-only node in the instance meets the condition.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the set maximum scaling specification is less than the current maximum read\-only node specification of the instance, this rule does not take effect.</div><br> |
|**Primary and standby node scaling configuration** |Click **Enable**, then configure the parameters for master and standby node scaling down as follows:<br><br><br>* **Judgment indicator**: Average CPU usage.<br><br>* **Effective condition**: The indicator remains below the set percentage threshold for the specified duration.<br><br>* **Execution action**: Scale down step by step according to the specification list until the minimum specification you set is reached.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">For example, if you set the average CPU usage threshold to 30%, the duration to 30 minutes, and the instance specification to 4 cores 16 GiB, then if the instance's average CPU usage remains at 30% or below for 30 minutes, the specification of the master and standby nodes will be gradually reduced until it reaches 4 cores 16 GiB.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The minimum specification you configure cannot be smaller than the instance's own specification.</div><br> |
|**Read\-only node scaling configuration** |Click **Enable**, then configure the parameters for scaling down the read\-only nodes as follows:<br><br><br>* **Judgment indicator**: Average CPU usage.<br><br>* **Effective condition**: When a read\-only node's indicator remains below the set percentage threshold throughout the specified duration.<br><br>* **Execution action**: Scale down step by step according to the specification list until the minimum specification you set is reached.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Scaling is triggered for a read\-only node if any read\-only node in the instance meets the condition.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If a read\-only node's minimum scaling specification is less than the current minimum scaling specification, that read\-only node will not trigger a change.</div><br> |
|**Read\-only node exemption configuration** |Select the target nodes from the list to which the automatic scaling down rules do not apply, keeping their specifications fixed. |



7. Click **OK**.


</Tab>
</Tabs>


<span id="G2JWQSoI"></span>
## Modify auto scaling


<Tabs>
<Tab zoneid="xiWhfFCy7N" title="Modify automatic scale-up only">
<TabTitle>Modify automatic scale-up only</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Configure AutoOps rules**.

6. In the **Configure AutoOps rules \- Compute scaling** panel, configure **Auto scaling** and enable the automatic scaling up and automatic scaling down parameters.



|**Parameter** |**Description** |
|---|---|
|**Scaling method** |This article uses **Auto scaling** as an example. Automatic and manual scaling cannot be configured simultaneously. |
|**Feature switch** |This example uses **Only enable automatic scaling down** as a case. |
|**Master and standby node expansion configuration** |The parameter information for modifying the expansion of master and standby nodes is as follows:<br><br><br>* **Judgment indicator**: Average CPU usage.<br><br>* **Effective condition**: The indicator remains above the set percentage threshold throughout the specified duration.<br><br>* **Execution action**: Scale up step by step according to the specification list until the maximum specification you set is reached.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For example: If you set the average CPU usage to 90%, the duration to 30 minutes, and the instance specification to 4 cores 16 GiB, then if the instance's average CPU usage remains at or above 90% for 30 minutes, the specification of the master and standby nodes will scale up step by step until reaching 4 cores 16 GiB.</div><br> |
|**Read\-only node scaling configuration** |The parameter information for modifying the expansion of read\-only nodes is as follows:<br><br><br>* **Judgment indicator**: Average CPU usage.<br><br>* **Effective condition**: When a read\-only node's indicator remains above the set percentage threshold throughout the specified duration.<br><br>* **Execution action**: Scale up step by step according to the specification list until the maximum specification you set is reached.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Scaling is triggered for a read\-only node if any read\-only node in the instance meets the condition.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the set maximum scaling specification is less than the current maximum read\-only node specification of the instance, this rule does not take effect.</div><br> |
|**Primary and standby node scaling configuration** |Click **Enable**, then configure the parameters for master and standby node scaling down as follows:<br><br><br>* **Judgment indicator**: Average CPU usage.<br><br>* **Effective condition**: The indicator remains below the set percentage threshold for the specified duration.<br><br>* **Execution action**: Scale down step by step according to the specification list until the minimum specification you set is reached.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">For example, if you set the average CPU usage threshold to 30%, the duration to 30 minutes, and the instance specification to 4 cores 16 GiB, then if the instance's average CPU usage remains at 30% or below for 30 minutes, the specification of the master and standby nodes will be gradually reduced until it reaches 4 cores 16 GiB.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The minimum specification you configure cannot be smaller than the instance's own specification.</div><br> |
|**Read\-only node scaling configuration** |Click **Enable**, then configure the parameters for scaling down the read\-only nodes as follows:<br><br><br>* **Judgment indicator**: Average CPU usage.<br><br>* **Effective condition**: When a read\-only node's indicator remains below the set percentage threshold throughout the specified duration.<br><br>* **Execution action**: Scale down step by step according to the specification list until the minimum specification you set is reached.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Scaling is triggered for a read\-only node if any read\-only node in the instance meets the condition.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If a read\-only node's minimum scaling specification is less than the current minimum scaling specification, that read\-only node will not trigger a change.</div><br> |
|**Read\-only node exemption configuration** |Select the target nodes from the list to which the automatic scaling down rules do not apply, keeping their specifications fixed. |



7. Click **OK**.


</Tab>
<Tab zoneid="POsFC2xXka" title="Modify automatic scale-down only">
<TabTitle>Modify automatic scale-down only</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Configure AutoOps rules**.

6. On the **Configure AutoOps rules \- Compute scaling** panel, configure parameters to **Only enable automatic scaling** for auto scaling.



|**Parameter** |**Description** |
|---|---|
|**Scaling method** |This article uses **Auto scaling** as an example. |
|**Feature switch** |This example uses **Only enable automatic scaling down** as a case. |
|**Primary and standby node scaling configuration** |The modified parameters for scaling down the primary and standby nodes are as follows:<br><br><br>* **Judgment indicator**: Average CPU usage.<br><br>* **Effective condition**: The indicator remains below the set percentage threshold for the specified duration.<br><br>* **Execution action**: Scale down step by step according to the specification list until the minimum specification you set is reached.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">For example, if you set the average CPU usage threshold to 30%, the duration to 30 minutes, and the instance specification to 4 cores 16 GiB, then if the instance's average CPU usage remains at 30% or below for 30 minutes, the specification of the master and standby nodes will be gradually reduced until it reaches 4 cores 16 GiB.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The minimum specification you configure cannot be smaller than the instance's own specification.</div><br> |
|**Read\-only node scaling configuration** |The parameter information for modifying the scaling of read\-only nodes is as follows:<br><br><br>* **Judgment indicator**: Average CPU usage.<br><br>* **Effective condition**: When a read\-only node's indicator remains below the set percentage threshold throughout the specified duration.<br><br>* **Execution action**: Scale down step by step according to the specification list until the minimum specification you set is reached.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Scaling is triggered for a read\-only node if any read\-only node in the instance meets the condition.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If a read\-only node's minimum scaling specification is less than the current minimum scaling specification, that read\-only node will not trigger a change.</div><br> |
|**Read\-only node exemption configuration** |Select the target nodes from the list to which the automatic scaling down rules do not apply, keeping their specifications fixed. |



7. Click **OK**.


</Tab>
<Tab zoneid="P2Wg2Y6Qko" title="Modify auto scaling">
<TabTitle>Modify auto scaling</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Configure AutoOps rules**.

6. In the **Configure AutoOps rules \- Compute scaling** panel, configure **Auto scaling** and enable the automatic scaling up and automatic scaling down parameters.



|**Parameter** |**Description** |
|---|---|
|**Scaling method** |This article uses **Auto scaling** as an example. |
|**Feature switch** |This example uses **Only enable automatic scaling down** as a case. |
|**Master and standby node expansion configuration** |The parameter information for modifying the expansion of master and standby nodes is as follows:<br><br><br>* **Judgment indicator**: Average CPU usage.<br><br>* **Effective condition**: The indicator remains above the set percentage threshold throughout the specified duration.<br><br>* **Execution action**: Scale up step by step according to the specification list until the maximum specification you set is reached.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For example: If you set the average CPU usage to 90%, the duration to 30 minutes, and the instance specification to 4 cores 16 GiB, then if the instance's average CPU usage remains at or above 90% for 30 minutes, the specification of the master and standby nodes will scale up step by step until reaching 4 cores 16 GiB.</div><br> |
|**Read\-only node scaling configuration** |The parameter information for modifying the expansion of read\-only nodes is as follows:<br><br><br>* **Judgment indicator**: Average CPU usage.<br><br>* **Effective condition**: When a read\-only node's indicator remains above the set percentage threshold throughout the specified duration.<br><br>* **Execution action**: Scale up step by step according to the specification list until the maximum specification you set is reached.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Scaling is triggered for a read\-only node if any read\-only node in the instance meets the condition.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the set maximum scaling specification is less than the current maximum read\-only node specification of the instance, this rule does not take effect.</div><br> |
|**Primary and standby node scaling configuration** |The modified parameters for scaling down the primary and standby nodes are as follows:<br><br><br>* **Judgment indicator**: Average CPU usage.<br><br>* **Effective condition**: The indicator remains below the set percentage threshold for the specified duration.<br><br>* **Execution action**: Scale down step by step according to the specification list until the minimum specification you set is reached.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">For example, if you set the average CPU usage threshold to 30%, the duration to 30 minutes, and the instance specification to 4 cores 16 GiB, then if the instance's average CPU usage remains at 30% or below for 30 minutes, the specification of the master and standby nodes will be gradually reduced until it reaches 4 cores 16 GiB.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The minimum specification you configure cannot be smaller than the instance's own specification.</div><br> |
|**Read\-only node scaling configuration** |The parameter information for modifying the scaling of read\-only nodes is as follows:<br><br><br>* **Judgment indicator**: Average CPU usage.<br><br>* **Effective condition**: When a read\-only node's indicator remains below the set percentage threshold throughout the specified duration.<br><br>* **Execution action**: Scale down step by step according to the specification list until the minimum specification you set is reached.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Scaling is triggered for a read\-only node if any read\-only node in the instance meets the condition.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If a read\-only node's minimum scaling specification is less than the current minimum scaling specification, that read\-only node will not trigger a change.</div><br> |
|**Read\-only node exemption configuration** |Select the target nodes from the list to which the automatic scaling down rules do not apply, keeping their specifications fixed. |



7. Click **OK**.


</Tab>
</Tabs>


<span id="CUOKiKWv"></span>
## Disable auto scaling


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Configure AutoOps rules**.

6. In the **Configure AutoOps rules \- Compute scaling** panel, configure the following parameters.

   * Disable all scaling rules: You can directly click **Disable** on the ** Automatic O&M rules \> Specification scaling** control panel.

   * Disable automatic scale\-up only: On the **Automatic O&M rules \> Specification sScaling** control panel, click **Only enable automatic expansion**, and disable the scale\-up configuration for primary/secondary nodes or read\-only nodes as needed.

      You can disable either the scale\-up configuration for primary/secondary nodes or the scale\-up configuration for read\-only nodes, but not both.

   * Disable automatic scale\-down only: On the **Automatic O&M rules \> Specification scaling** control panel, click **Only enable automatic scaling**, and disable the scale\-down configuration for primary/secondary nodes or read\-only nodes as needed.

   You can disable either the scale\-down configuration for primary/secondary nodes or the scale\-down configuration for read\-only nodes, but not both.

   * Disable simultaneous auto scale\-out and auto scale\-in: In the **Automatic O&M Rules \> Specification Scaling** Control Panel, click **Enable Auto Scale\-Out and Auto Scale\-In Simultaneously**, and then disable the **scale\-out** and **scale\-in** configurations for **primary/secondary nodes** and **read\-only nodes** as needed.

   When disabling this feature, you must retain at least one scale\-up rule and one scale\-down rule.

7. Click **OK**.


<span id="IM3MtaKc"></span>
## View scheduled scaling events

You can view scaling up events within the last 30 days at most.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the AutoOps event tab under the **AutoOps** tab, set the time frame for querying events as needed. The target events you can view include **Event ID**, **Event status**, **Trigger value**, **Trigger condition**, **Rule type**, **Before/After adjustment**, **Trigger time**, and **Last update time**


Before/After triggering indicates the node specifications before and after automatic scaling up is triggered.

<span id="4d2Wi4Hv"></span>
## FAQ

**Q: Why is auto scaling not triggered even when threshold conditions are met?** 

A: Auto scaling not being triggered is usually caused by the following reasons:


* State restrictions: The instance is currently in a state that does not support configuration changes (e.g., restarting, upgrading, or under maintenance).

* Resource limitations: Insufficient underlying available resources prevent the configuration change from completing.

* Scale\-down condition validation: Triggering automatic scale\-down depends not only on CPU thresholds and duration but also on comprehensive safety checks, such as memory usage. If any condition is not met, the system will pause execution. It is recommended to check the specific trigger conditions and resource/state restrictions by reviewing instance monitoring metrics and the execution records of the current task.


**Q: Will scaling affect business connections?** 

A: Possibly. During scaling, the instance may experience brief disconnections (1–3 times) or enter a second\-level read\-only state. To ensure business continuity, it is strongly recommended to configure an automatic reconnection mechanism for your application or schedule operations during off\-peak hours.

**Q: Can scaling be performed while the instance is executing OnlineDDL?** 

A: It is not recommended to perform both simultaneously. Scaling operations will interrupt ongoing OnlineDDL tasks. Before performing configuration changes (including automatic and manual), confirm whether the instance has any running OnlineDDL tasks and try to schedule the operation in an appropriate maintenance window.
