---
title: "Elastic scaling"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Elastic_scaling"
---

When using a Volcano Engine E\-MapReduce (EMR) cluster, if resource usage frequently experiences peaks and valleys, you can use the cluster's elastic scaling feature to automatically expand temporary computing capacity during peak periods, helping you handle business computing surges. After the business peak passes, automatic scale\-in is performed to reduce your computing resource usage costs. This document introduces the core capabilities of elastic scaling and how to use its features.

<span id="2e530776"></span>
# context

<span id="_2-应用场景"></span>
## **use cases**

In the following scenarios, using the EMR elastic scaling feature can help reduce costs and improve execution efficiency.


* The business computing load curve has obvious peaks and valleys.

* When you are very familiar with your business, you can plan the cluster's computing capacity within fixed time periods to meet business needs while also saving costs.

* To ensure that critical jobs are completed on time, it is necessary to add nodes based on certain load metrics during specific time periods.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Whether elastic scaling succeeds depends on factors such as resource inventory and cluster operating status.</div>


<span id="851b4458"></span>
## Concept definitions


* **Elastic scaling**:

   Elastic scaling (Auto Scaling) is a management service that automatically adjusts cluster computing resources based on your business needs and policies.

* **Sampling interval**

   The collection of load metric values is generally performed by a metric monitoring service (such as prometheus) on the cluster side at a fixed frequency. The time interval between two consecutive samples is called the sampling interval, which is fixed at 30 seconds.

* **Polling interval**

   The control side performs simple polling of the metric values collected from each cluster. The time interval between two consecutive polls is called the polling interval, which is fixed at 5 minutes. Based on the sampling interval above, it is easy to calculate that there are 10 values for a given load metric in each polling query.


<span id="_4-核心能力"></span>
## **Core capabilities**


|**Core capabilities** |**Note** |
|---|---|
|Supports multiple scaling scenarios |* Elastic expansion automatically adjusts elastic computing resources based on your business needs, seamlessly increasing ECS instances during peak demand.<br><br>* Elastic contraction automatically adjusts elastic computing resources based on your business needs, reducing ECS instances when demand decreases to save costs. |
|Supports multiple scaling rules |* Scheduled scaling rules configure scheduled tasks to add or remove ECS instances at a fixed time, suitable for scenarios with sudden and clearly defined business needs.<br><br>* Periodic scaling rules configure recurring tasks to add or remove ECS instances at scheduled intervals, suitable for stable business expectations.<br><br>* Load rules automatically add or remove ECS instances based on YARN metrics, such as the number of running tasks and available memory. Suitable for advanced EMR users, enabling optimal utilization of computing resources and reducing costs.<br><br>* Compound scaling rules combine time intervals and load rules. Within recurring time periods, ECS instances are automatically added or removed based on YARN metrics. These rules are suitable for advanced users with clear business expectations, enabling optimal utilization of computing resources while maximally meeting business needs. |


<span id="032e75ea"></span>
## Scaling rules


|**Rule types** |**Use cases** |**Core configuration parameters** |**Constraint validation items** |
|---|---|---|---|
|Scheduled rules |Rapidly expand resources before foreseeable, one\-time business peaks. |* Trigger condition: a fixed point in the future (time precision options include year/month/day/hour/minute, with seconds defaulting to 0).<br><br>* Example: fixed time point = 2026\-02\-27 21:12 |* Cannot be used in conjunction with other conditions.<br><br>* The fixed time point must be later than the current time plus 5 minutes (the default value is current time plus 5 minutes). |
|Periodic rules |For businesses with regular cyclical patterns. |* Recurring period: day.<br><br>* Trigger condition: a specific time within a day (hour/minute, with seconds defaulting to 0).<br><br>* Example: daily = 03:04. |* Cannot be used in conjunction with other conditions.<br><br>* Cannot be combined with other daily cycle conditions using 'or' logic. |
|||* Recurring period: week.<br><br>* Trigger condition: a specific time (hour/minute, with seconds defaulting to 0) on one or more days from Monday to Sunday.<br><br>* Example: every Tuesday and Thursday = 03:04 |* Cannot be used in conjunction with other conditions.<br><br>* Cannot be combined with other daily cycle conditions using 'or' logic. |
|||* Recurring period: month.<br><br>* Trigger condition: a specific time (precision up to hour/minute, with seconds defaulting to 0) on one or more days each month.<br><br>* Example: the 1st and 15th of each month at 03:04. |* Cannot be used in conjunction with other conditions.<br><br>* “Last day of the month” is automatically determined based on the number of days in the month.<br><br>* If the selected date does not exist in the current month (such as February 30), it is automatically adjusted to the last day of the month. |
|Load rules |Refined management by combining load conditions and specific time periods. For example, dynamic scaling based on YARN load is enabled only during daytime business peak hours on weekdays. |* YARN metrics: Select one or more YARN metrics as triggers, such as `AppsPending` (number of queued tasks), `AvailableMemoryPrecentage` (percentage of available memory), and more.<br><br>* Supports automatic triggering of elastic scaling based on YARN queue\-level resource metrics. The default is root, and queues under root are supported, such as root.default and root.production.<br><br>* Metric conditions: When the metric is `>`, `>=`, `=`, `<=`, or `<` a certain threshold<br><br>* Frequency: Occurs more than X times within the past statistical period. Statistical period: XX minutes/hours.<br><br>* Trigger condition: The YARN metric meets the metric condition at the specified frequency and is not within the cooldown period.<br><br>* Example: Within 30 minutes, the number of available YARN cores exceeds 50 more than 5 times; after each rule takes effect, there is a 30\-minute cooldown. |* Must be combined with the time interval rule.<br><br>* When the YARN service is abnormal or stopped, all load rules based on YARN metrics will automatically become invalid.<br><br>* The statistical period for frequency must be greater than 5 minutes and less than 1 hour.<br><br>* Add a load scaling rule. By default, a time interval scaling rule is also added. Default value: daily & interval. |
|Time interval ||* Repeat cycle: daily.<br><br>* Time period: A specific interval within a day (hour/minute, second defaults to 0).<br><br>* Example: 03:00–5:00 every day. |* Must be combined with the load rule.<br><br>* The time interval must be greater than 5 minutes.<br><br>* The time interval must be greater than the load statistical period. |
|||* Repeat cycle: weekly.<br><br>* Time period: A specific interval (hour/minute, second defaults to 0) on one or several days (weekdays) from Monday to Sunday.<br><br>* Example: 03:00–5:00 on Tuesday and Thursday every week. ||
|||* Repeat cycle: monthly.<br><br>* Time period: A specific interval (hour/minute, second defaults to 0) on one or several days each month.<br><br>* Example: 03:00–5:00 on the 1st and 15th of each month. ||


<span id="cd34155c"></span>
# prerequisites


* Currently, elastic scaling only supports the **Pay\-As\-You\-Go** billing type. Supported cluster types and versions are as follows:

   
   |**Cluster type** |**Version requirements** |
   |---|---|
   |Hadoop |> = EMR\-2.0.1 |
   |Starrocks |> = EMR\-3.5 |
   

* In the cluster instance settings, you must first add a Task instance. See [Create a cluster (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456) for details.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When creating a cluster, you must first add a Task node instance in the cluster instance settings. See <a href="https://docs.byteplus.com/docs/E-MapReduce/105456">Create a cluster (version 3.18.0 and earlier)</a> for details.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If an existing cluster does not have a Pay\-As\-You\-Go Task node group, you can add one via <strong>Node Management \> Add Node Group</strong> and then perform elastic scaling. For details, see <a href="https://docs.byteplus.com/docs/E-MapReduce/105443">Node group management</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also add a Task node scaling group by clicking <strong>Add Node Group</strong> in the middle of the elastic scaling tab page.   </div>
   


<span id="jump1"></span>
# Enable elastic scaling


1. Log in to the ([E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?)).

2. From the left navigation bar, go to the **Resource Management \> on ECS \> Cluster Details \> Elastic Scaling** tab.

3. If the cluster has eligible Task node groups, you can view the list of all available elastic scaling node groups for the cluster in the **Available Elastic Scaling Node Groups** section. You can perform the following actions:

   * In the rightmost **Actions** column, click the **Enable** or **Disable** button to control the status of the node group's elastic scaling feature.

   * In the **Elastic Scaling Range** column, the limit range for the number of node group instances is displayed. Click the **Edit** button to set the maximum and minimum number of instances for elastic scaling. The minimum and maximum instance settings only apply to elastic scaling and do not constrain manual scaling in or out. Their purposes are as follows:

      * Purpose of the maximum instance setting: When the scaling\-out rule takes effect, if the number of instances after scaling out exceeds the upper limit, the scaling\-out action will be denied to ensure that the number of instances in the scaling group does not exceed the maximum instance limit.

      * Purpose of the minimum instance setting: When the scaling\-in rule takes effect, if the number of instances after scaling in falls below the lower limit, the scaling\-in action will be denied to ensure that the number of instances in the scaling group does not fall below the minimum instance limit.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When you enable the auto\-scaling feature for a node group for the first time, if you do not set the scaling range, the system will set the scaling range of the node group to the default values: the default minimum number of instances is 0, and the default maximum number of instances is 30.      </div>
      

<span id="_6-2-管理弹性伸缩规则"></span>
# Add elastic scaling rules

<span id="_6-2-1-使用限制"></span>
## **Limits**


1. Each cluster can add up to 20 scaling rules.

2. Currently, only scaling rules based on certain YARN metrics for load type configuration are supported.

3. If the cluster's YARN service is stopped or abnormal, rules based on load metrics will become invalid.


<span id="_6-2-2-注意事项"></span>
## **important notes**


1. Elastic scaling rules belong to the cluster. To enable eligible node groups to use elastic scaling, you must enable the elastic scaling feature for the corresponding node group. For details, see [Enable elastic scaling](https://docs.byteplus.com/docs/E-MapReduce/105442#jump1).

2. After a rule is triggered, all node groups associated with the rule will automatically scale out or scale in according to the strategy preset when the rule was associated. If no rule is set, or if a rule is set but not associated with any node group, the elastic scaling feature will not be triggered.

3. Scaling actions are performed separately for each node group (with the same node configuration), and different node groups do not affect each other.


<span id="jump2"></span>
## Add scaling rule

In the **Elastic Scaling Rules** section, on the **Scaling Rules** tab (displayed by default), click the **Add Scaling Rule** button on the right to add a new scaling rule.

The detailed field descriptions are as follows:

<span id="171cbf7f"></span>
### Configure the rule name


|**Rule item** |**Description** |**Example value** |
|---|---|---|
|Rule name |Name of the scaling rule. Value:<br><br><br>* Must start with a Chinese character or a letter.<br><br>* Can only contain Chinese characters, letters, numbers, underscores, and hyphens.<br><br>* Length limit: 1–128 characters.<br><br>* Special characters are not supported. |test\-policy |


<span id="6d1ec3da"></span>
### Configure the trigger condition


|**Rule item** |**Description** |**Example value** |
|---|---|---|
|Fixed time point |* Cannot be set earlier than the current time.<br><br>* For sub\-rules with fixed time points (separated by "or"), you cannot add trigger metrics to set other sub\-items (separated by "and"). If you do, the system will ignore all sub\-items except the fixed time point. |2023\-02\-10 14:54:14 |
|Daily + interval |Indicates triggering within a specific time period each day |08:00 \- 18:00 |
|Daily + equals |Indicates triggering at a specific time point each day |09:00 |
|Weekly |Indicates triggering on certain days of the week; multiple selections are supported |Monday, Friday |
|Monthly + interval |Indicates triggering on a continuous range of dates each month |10th–22nd |
|Monthly + equals |Indicates triggering on a specific day each month; supports selecting the last day or the first day |Last day |
|Numeric type |When a metric exceeds the threshold, and the number of occurrences within a certain time period exceeds the set value, the rule is triggered. The sampling interval for metrics is 30 seconds.<br><br>For currently supported metrics, see the table [Configure the list of load metrics](https://docs.byteplus.com/docs/E-MapReduce/105442#df405e0b). |Yarn available cores:<br><br>Less than 30 cores, more than 10 occurrences within 30 minutes |


<span id="aa7f6c32"></span>
### Configure the retry interval


|**Rule item** |**Description** |**Example value** |
|---|---|---|
|Retry time |Retry time applies only to time\-triggered scaling rules. When a rule reaches its specified trigger time but cannot be executed immediately due to cooldown, ongoing scaling operations, insufficient resources, or other reasons, EMR will automatically retry once every 30 seconds within the configured retry period until the conditions are met and the scaling action is performed, or the retry period is exceeded and the execution is abandoned. Configuration range: 30–3600 seconds, default value: 360 seconds. |360 seconds |


<span id="df405e0b"></span>
### Configure the **list of load metrics**


|**Condition type** |**Data source** |**Metric code** |**Native metric** |**Metric name** |**Unit** |
|---|---|---|---|---|---|
|Value |YARN |AvailableVCores |availableVirtualCores |Yarn available cores |core |
|Value |YARN |AvailableMemory |availableMB |Yarn available memory |GB |
|Value |YARN |AppsRunning |appsRunning |Yarn running tasks |number |
|Value |YARN |AppsPending |appsPending |Yarn queued tasks |number |
|Value |YARN |MemoryAvailablePrecentage |availableMB/totalMB |Yarn available memory ratio |% |
|Value |YARN |VCoresAvailablePrecentage |availableVirtualCores/totalVirtualCores |Yarn available cores ratio |% |
|Value |YARN |AppsPendingRatio |appsPending/（appsSubmitted + appsPending + appsRunning） |Yarn queued task ratio |% |
|Value |YARN |AppsKilled |appsKilled |Yarn killed tasks |number |
|Value |YARN |AppsFailed |appsFailed |Yarn failed tasks |number |
|Value |YARN |AppsCompleted |appsCompleted |Yarn completed tasks |number |
|Value |YARN |AppsSubmitted |appsSubmitted |Yarn submitted tasks |number |


After entering the rule name and trigger condition, click the **OK** button to complete the addition of the scaling rule.

<span id="_6-2-4-管理伸缩规则"></span>
## Manage scaling rules

After a scaling rule is added successfully, you can perform the following management operations on the scaling rule.

<span id="9925d6c2"></span>
### Edit and delete rules

Click the **Actions** column and click the **Edit** or **Delete** button to edit or delete the scaling rule.

If a rule has already been bound to a node group and the node group has elastic scaling enabled, the rule will be in the active state. Active rules cannot be edited or deleted; the corresponding buttons will be grayed out. When hovering the mouse over the edit or delete button, a tooltip will display the reason why the operation is not allowed.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Editing a rule takes effect in real time and will be reflected in the next polling interval. All node groups associated with the rule will be affected.</div>


* <div data-tips="true" data-tips-type="warning">When deleting a rule, if the rule is already associated with a node group, the association will be removed synchronously. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">If a rule is already bound to a node group and the node group has enabled elastic scaling, the rule is active. Active rules cannot be edited or deleted.</div>



<span id="fa6ccae9"></span>
### Query rules


* You can enter the rule name in the search box to perform a fuzzy search for scaling rules.

* In the **Associated Node Group** column, click the **Filter** funnel button on the right to filter rules. You can query the rules associated with the corresponding node group.


<span id="193b7bdb"></span>
# Set the cooldown time

When a scaling rule triggers a scaling action for a node group (or multiple node groups), any scaling actions triggered by scaling rules for that node group will be rejected for a period after the scaling operation is completed. This period is called the cooldown period and is intended to prevent scenarios where node groups scale rapidly and frequently under certain conditions, which may lead to cluster instability.


* **Scope:**  All rules that have been added to the current cluster.

* **Setting range**: 1–180 minutes.

* **Default value**: 5 minutes.

* **Procedure**: In the **scaling rule** tab, click the **edit** icon to the right of **general settings** to set the cooldown period.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This cooldown period applies only to elastic scaling rules and does not affect manual actions. That is, during the cooldown period, manual scaling functions are not affected.   </div>
   

<span id="_6-3-关联伸缩规则"></span>
# Associate scaling rule

<span id="b68579e4"></span>
## Enable association with elastic scaling rules

In the **available elastic scaling node group** section, in the **operation** column on the right, click the button to the left of **associate rule** to enable association with elastic scaling rules for the node group.

<span id="db4a45c2"></span>
## Bind scaling rule

On the **associate rule** page, click the **bind** button in the operation column to bind the rule to the current node group.

The following items must be configured when binding:


* Scaling behavior

   
   |**Parameter** |**Note** |
   |---|---|
   |Number of new instances |Increase by number of instances |
   |Percentage of new instances |When the rule is triggered, the number of new instances is calculated based on the percentage of instances. The result is rounded up. If the current number of instances is 0, it is treated as 1.<br><br>For example: If the number of nodes when the rule is triggered is 10 and the percentage of new instances is set to 20%, then 2 instances will be added. |
   |Number of instances to reduce |Reduce by number of instances |
   |Percentage of instances to reduce |When the rule is triggered, the number of instances to reduce is calculated based on the percentage of instances. The result is rounded down.<br><br>For example: When the number of nodes triggered by the rule is 10 and the percentage for reducing instances is set to 20%, the number of instances will be reduced by 2. |
   

* Automatically add resource pool tags

   
   |**Status** |**Note** |**prerequisites** |
   |---|---|---|
   |Enable |After enabling automatic addition of resource pool tags, you can select the target resource pool tag. The system will automatically associate the resource pool tag with the nodes that are elastically scaled out. |Enable resource pool management. For details, see [YARN resource pool management](https://docs.byteplus.com/docs/undefined/6a18fa8b9a082404cc2e439b) |
   |Disable |Nodes that are elastically scaled out will not be associated with resource pool tags. |Not applicable |
   


After binding the rule, you can adjust the scaling behavior by clicking the **edit** icon button in the **scaling behavior** column.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The maximum number of instances that can be adjusted in a single operation must not exceed 30.</div>


<span id="a13a59c6"></span>
## View associated rules

Click the **associate rule** button to enter the **associate rule** page, where you can view all rules that have been added to the current cluster.

On the **associate rule** page, you can view all rules that have been added to the current cluster.

If there are many rules, you can check "**Show only associated rules**" or enter the **rule name** in the search box on the right for quick retrieval.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If there are no rules under the cluster, you can click the <strong>Add Rule</strong> button to quickly navigate to the Add Rule page and add scaling rules. For details, see <a href="https://docs.byteplus.com/docs/E-MapReduce/105442#jump2">Add scaling rule</a>.</div>


<span id="_6-4-查看伸缩记录"></span>
# View scaling records

Click the **history** button on the right side of the scaling rules tab to view the cluster's elastic scaling records. In the history records, you can perform the following actions:


1. You can quickly filter historical records by selecting **Trigger conditions met**. This option is selected by default.

2. Enter **the rule name** in the search box to filter the triggering and execution status of rules you are interested in. Fuzzy search is supported.

3. Enter the start and end time in the time search box to query records. The default time range is the past day.

4. You can also filter records using the **scaling status** column's **filter button (funnel icon)**  on the right. The specific status descriptions are shown in the table below:

   
   |**Status** |**Description** |
   |---|---|
   |In progress |The elastic scaling activity is in progress. |
   |All successful |According to the scaling rules and binding information, all nodes involved in scaling are added to or removed from the corresponding node group. |
   |Partially successful |This only occurs during scaling out. Due to the impact of ECS or cloud disk inventory, only some nodes are successfully scaled out. |
   |All failed |According to the scaling rules, no nodes are added to or removed from the cluster. |
   |Rejected |If the number of instances after running the scaling rule is greater than the maximum number of instances or less than the minimum number of instances, or if the previous scaling activity of the node group has not yet ended when the rule is triggered, the rule execution will be rejected. |
   |Exception |This only occurs during scaling in. When services such as ECS, cloud disk, or billing module are abnormal, the component has already been taken down, but the node has not been removed. At this time, the status of the scaling group will be locked in scaling in status, and node operations cannot be performed. Please contact us as soon as possible for processing to avoid losses. |
   

5. Click the **Trigger conditions met** column's **View** button to review how load\-based rules were triggered along with historical metric values.
