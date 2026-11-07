---
title: "Elastic scheduled scale-out (general-purpose)"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Elastic_scheduled_scale-out"
---

Vital Kubernetes Engine (VKE) provides the feature of elastic scheduled scale\-out for node pools that consist of Elastic Scheduled Instances (ESI), allowing a single increase in the number of nodes within the node pools by the specified count within a specific time period or periodic increase at a specified interval. This topic introduces the usage scenarios and configuration methods of this feature.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

ESI is a type of pay\-as\-you\-go instance provided by BytePlus IaaS that can be delivered according to a schedule. It is designed to ensure a stable supply of resources for elastic usage scenarios. After you finish the schedule configuration, instances can be automatically created as pay\-as\-you\-go type within the specified delivery time period, but are charged as ESI. For details, see [ESI overview](https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances_Overview).

The cluster resource scale\-out feature in VKE through ESI applies to the following scenarios:


* A predictable non\-persistent resource demand peak

   Business scenarios where a large number of visits are expected in a short time period. In such cases, allocate more resources to critical cluster businesses during specific time periods to maintain high performance. Examples include major e\-commerce promotions, live video streaming, holiday peak ticketing, and other similar scenarios.

* Regular business peaks

   The business peaks that are predicted to occur periodically (daily, weekly, or monthly). When business workload peaks in a cluster always occur within a specific time period, you can use the elastic scheduled scale\-out feature to scale out the cluster during that period. This ensures a stable resource supply and an optimal access experience. The peaks include the daily business peaks of online gaming, online education, big data analysis, and rendering businesses, and the monthly reconciliation peaks of financial services.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">New ECS nodes created by elastic scheduled scale\-out use the same <strong>instance type</strong> as configured for the node pool. For example, if the instance type for the node pool is set to <code>ecs.g3i.large</code>, the new ECS nodes will also use <code>ecs.g3i.large</code>.</div>


* <div data-tips="true" data-tips-type="tip">For details of the instance families supported by ESI, see <a href="https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances_Overview">ESI overview</a>.</div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A node pool has been created. For details, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* Elastic scheduled scale\-out and cluster autoscaler cannot both be enabled.

* ESI cannot be reclaimed automatically (except for those reclaimed due to account arrears) after they are successfully delivered and added to the node pool. You can use the following methods to reclaim the instances:

   * Disable or delete the scheduled scale\-out job, and then enable cluster autoscaling to realize dynamic node scale\-out or automatic node reclaim. For details, see [Cluster autoscaler](https://docs.byteplus.com/en/docs/vke/Creating-a-Cluster-Autoscaler).

   * On the [Elastic Compute Service console](https://console.byteplus.com/ecs/instance), manually delete the ESI.

* You can create at most 10 scaling rules per node pool.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".6YWN572u5a6a5pe25Lu75Yqh"></span>
### Configuring CronJobs

After you configure a CronJob, which is a one\-time scheduled scale\-out task, the system will scale out the node pool with ESI within the specified delivery time period. Procedure:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the cluster list page, click the target cluster.

4. In the left navigation bar, click **Nodes** \> **Node pool**.

5. In the node pool list, find the target node pool and click `...`****  \> **Scheduled scale\-out** to go to the **Scheduled scale\-out rule** tab.

6. Click **Create scheduled scale\-out rule** to configure the scheduled scale\-out specification settings.

   
   |Parameter |Description |
   |---|---|
   |Name |Provide a name for the elastic scheduled scale\-out rule. The rule name must be unique within the same node pool. |
   |Rule type |Select the type of elastic scheduled scale\-out rule. In this example, select **CronJob**. |
   |Scheduled type |Select the type of elastic scheduled instance. In this example, select **General purpose**. |
   |Number of scheduled instances |Specify the number of instances to be added in a one\-time job. Instances will be automatically delivered within the delivery time period.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">500 instances can be scheduled for a one\-off job at most.</div><br> |
   |Delivery time period |Select the time period for instance delivery. The period is a 10\-minute time slot within the day you specified. After you confirm the configuration, the instance will be delivered within that time period.<br><br>For example, if the current time is 17:42, the earliest available delivery window is 4 hours later, i.e., from 21:50 to 22:00, and the latest available delivery window is 8 hours later, i.e., from 01:40 to 01:50 (next day). |
   |Time to submit the scheduled order |Configure the time for submitting scheduled orders. Elastic scheduled instances can be scheduled 4 to 8 hours in advance. Therefore, this configuration can be set to 4 to 8 hours before the **Delivery time period**. You can specify a time from years all the way down to minutes. |
   |Best effort |Specify whether to enable the best effort feature for elastic scheduled scale\-out.<br><br><br>* Disable: (Default) The system creates one scheduled order based on the instance type and the number of scheduled instances configured in the node pool. If the corresponding instances are insufficient, the scheduled order will fail to be created.<br><br>* Enable: If the inventory of elastic scheduled instances cannot fully meet the requirements, the best effort mode is adopted.<br><br>   * The system attempts to create multiple scheduled orders to reach the required number of scheduled instances based on the scheduled instance type and availability zone (AZ) specified for the node pool.<br><br>   * If the total scheduled instances of the corresponding type in the corresponding availability zone still cannot meet the requirements,<br><br>      * When the inventory is greater than or equal to 1 and less than or equal to the number of scheduled instances, the system will create multiple scheduled orders based on the inventory.<br><br>      * When the inventory is less than 1, the scheduled order fails to be created due to insufficient inventory. |
   |Post\-creation state |Specify the status of the elastic scheduled scale\-out job. Valid values:<br><br><br>* **Enable**: Creates and enables the elastic scheduled scale\-out job.<br><br>* **Disable**: Creates the elastic scheduled scale\-out job without enabling it. |
   

7. Click **Confirm**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After you complete the initial elastic scheduled scale\-out configuration, you can modify the configuration by clicking <strong>Scheduled scale\-out</strong> again. The system applies the configuration changes as follows:   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the configuration modification time is earlier than the <strong>Time to submit the scheduled order</strong> set in the initial configuration, the initial scheduled order has not been created. Therefore, the node pool will ‌submit the scheduled order based on the latest parameters‌ (those from the last modification) and complete the scheduled delivery.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the configuration modification time is later than the <strong>Time to submit the scheduled order</strong> set in the initial configuration:   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you modify only parameters other than the <strong>Time to submit the scheduled order</strong> parameter: Because the scheduled order for the initial configuration has already been created, the new configuration will not impact the already submitted scheduled order. The new configuration applies only to the next scheduled order submission.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you modify the <strong>Time to submit the scheduled order</strong> parameter, the system will create a new scheduled order with your updated configuration, and the node pool will perform two scheduled deliveries.   </div>
   


<span id=".6YWN572u5ZGo5pyf5Lu75Yqh"></span>
### Configuring periodic jobs

After you configure a periodic job, the system will periodically scale out the node pool with ESI within the specified time period. Procedure:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the cluster list page, click the target cluster.

4. In the left navigation bar, click **Nodes** \> **Node pool**.

5. ****In the node pool list, find the target node pool and click `...`  \> **Scheduled scale\-out** to go to the **Scheduled scale\-out rule** tab.

6. Click **Create scheduled scale\-out rule** to configure the scheduled scale\-out specification settings.

   
   |Parameter |Description |
   |---|---|
   |Name |Provide a name for the elastic scheduled scale\-out rule. The rule name must be unique within the same node pool. |
   |Rule type |Select the type of elastic scheduled scale\-out rule. In this example, select **Periodic job**. |
   |Scheduled type |Select the type of elastic scheduled instance. In this example, select **General purpose**. |
   |Number of scheduled instances |Specify the number of instances to be added in a periodic job. Instances will be automatically delivered within the delivery time period.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">500 instances can be scheduled for a one\-off job at most.</div><br> |
   |First delivery period |Select the time period for the first delivery of the instance. The period is a 10\-minute time slot within the day you specified. After you confirm the configuration, the instance will be delivered within that time period.<br><br>For example, if the current time is 17:42, the earliest available delivery window is 4 hours later, i.e., from 21:50 to 22:00, and the latest available delivery window is 8 hours later, i.e., from 01:40 to 01:50 (next day). |
   |Time to submit the scheduled order for the first time |Configure the time for submitting the first scheduled order ESI can be scheduled 4 to 8 hours in advance. Therefore, this configuration can be set to 4 to 8 hours before the **Delivery time period**. You can specify a time from years all the way down to minutes. |
   |Best effort |Specify whether to enable the best effort feature for elastic scheduled scale\-out.<br><br><br>* Disable: (Default) The system creates one scheduled order based on the instance type and the number of scheduled instances configured in the node pool. If the corresponding instances are insufficient, the scheduled order will fail to be created.<br><br>* Enable: If the inventory of ESI cannot fully meet the requirements, the best effort mode is adopted.<br><br>   * The system attempts to create multiple scheduled orders to reach the required number of scheduled instances based on the scheduled instance type and AZ specified for the node pool.<br><br>   * If the total scheduled instances of the corresponding type in the corresponding AZ still cannot meet the requirements,<br><br>      * When the inventory is greater than or equal to 1 and less than or equal to the number of scheduled instances, the system will create multiple scheduled orders based on the inventory.<br><br>      * When the inventory is less than 1, a scheduled order fails to be created due to insufficient inventory. |
   |Repeat cycle |Select a repeat cycle for the elastic scheduled scale\-out job. Valid values:<br><br><br>* **By day**: The job is executed by day. For example, it runs every two days.<br><br>* **By week**: The job will be executed on the specified days each week. Valid values: **Monday**, **Tuesday**, **Wednesday**, **Thursday**, **Friday**, **Saturday**, and **Sunday**.<br><br>* **Monthly**: The job will be executed on the specified days each month. For example, the job is executed from the 1st to the 10th of each month.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you select <strong>Monthly</strong> and specify days beyond the 28th, the job will be ignored in a month that only has 28 days.</div><br> |
   |Time zone |Currently, only UTC+08:00 is supported, which is Beijing Time. |
   |Cycle end time |Select the end time of the periodic elastic scheduled scale\-out job. You can specify a time point on a day of a month of a year, which is accurate to minutes. |
   |Post\-creation state |Specify the status of the elastic scheduled scale\-out job. Valid values:<br><br><br>* **Enable**: Creates and enables the elastic scheduled scale\-out job.<br><br>* **Disable**: Creates the elastic scheduled scale\-out job without enabling it. |
   

7. Click **Confirm**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After you complete the initial elastic scheduled scale\-out configuration, you can modify the configuration by clicking <strong>Scheduled scale\-out</strong> again. The system applies the configuration changes as follows:   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the configuration modification time is earlier than the <strong>Time to submit the scheduled order for the first time</strong> set in the initial configuration, the initial scheduled order has not been created. Therefore, the node pool will ‌submit the scheduled order based on the latest parameters‌ (those from the last modification) and complete the scheduled delivery.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the configuration modification time is later than the <strong>Time to submit the scheduled order for the first time</strong> set in the initial configuration:   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you modify only parameters other than the <strong>Time to submit the scheduled order for the first time</strong> parameter: Because the scheduled order for the initial configuration has already been created, the new configuration will not impact the already submitted scheduled order. The new configuration applies only to the next scheduled order submission.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you modify the <strong>Time to submit the scheduled order for the first time</strong> parameter, the system will create a new scheduled order with your updated configuration, and the node pool will perform two scheduled deliveries.   </div>
   


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

<span id=".566h55CG5by55oCn6aKE57qm5omp5a655Lu75Yqh"></span>
### Manage elastic scheduled scale\-out jobs

In the node pool list, click the name of the target node pool to enter the node pool details page. On the node details page, click the **Scheduled scale\-out rule** tab to view the scheduled scale\-out job details.


* Click **Modify** to view or modify the elastic scheduled scale\-out job.

* Click **Delete** to delete the elastic scheduled scale\-out job.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You can modify the initial elastic scheduled scale\-out configuration. The system applies the configuration changes as follows:   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the configuration modification time is earlier than the <strong>Time to submit the scheduled order</strong> set in the initial configuration, the initial scheduled order has not been created. Therefore, the node pool will ‌submit the scheduled order based on the latest parameters‌ (those from the last modification) and complete the scheduled delivery.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the configuration modification time is later than the <strong>Time to submit the scheduled order</strong> set in the initial configuration:   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you modify only parameters other than the <strong>Time to submit the scheduled order</strong> parameter: Because the scheduled order for the initial configuration has already been created, the new configuration will not impact the already submitted scheduled order. The new configuration applies only to the next scheduled order submission.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you modify the <strong>Time to submit the scheduled order</strong> parameter, the system will create a new scheduled order with your updated configuration, and the node pool will perform two scheduled deliveries.   </div>
   


<span id=".5p-l55yL6IqC54K55rGg5Ly457yp6K-m5oOF"></span>
### Viewing the scaling details of the node pool

After an elastic scheduled scale\-out is performed on the node pool, you can view the scaling logs of the node pool, which contain detailed scaling information.


1. In the left navigation bar, click **Nodes** \> **Node pool**.

2. Click the name of the target node pool to enter the details page.

3. Click the **Scaling record** tab to view the detailed autoscaling records of this node pool. These records include scaling activity, status, number of changed instances, number of instances after change, and other information.

   You can filter the scaling records based on conditions and time. Multiple filter conditions can be configured, and the relationship between them is **AND**. You can use the following keywords:

   * **Scaling record ID**: Filter records by scaling record ID. You can find it in the **Scaling activity** column of the scaling records. For example, `s-42ccnt`.

   * **Node ID**: Filter records by node ID. You can find node IDs in the **Number of changed instances** column of the scaling records.

   * **Scaling type**: Filter records by scaling type. Supported options include **Scale in** and **Scale out**.


<span id="qvS6M3BZ"></span>
### Viewing the scheduled orders of nodes

After an elastic scheduled scale\-out is performed on a node pool, you can view the ID of the elastic scheduled order associated with each new node in the node list.


1. In the left navigation bar, select **Nodes** \> **Node**.

2. In the node list, find the target node and view the ID of the scheduled order that is associated with the newly added node in the **Elastic scheduled order ID** column.
