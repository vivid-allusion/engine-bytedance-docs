---
title: "Generating alert policies using templates"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Generating_alarm_strategies_with_alarm_templates"
---

You can save alert rules for commonly used cloud product metrics to an alert template, and save collections of alert targets to an object group. When the resource types of an alert template and an object group overlap, Cloud Monitor will automatically generate the corresponding alert policies.

<span id="ce786019"></span>
## Background

Only when the resource types of an alert template and an object group overlap will Cloud Monitor automatically generate an alert policy.

Since alert templates and object groups are independent of each other, the impact of editing a configured alert template or object group on existing alert policies is shown in the following table.


|Targets edited |Impact |
|---|---|
|Edit alert templates only. |The alert rules of generated alert policies will be synchronized with the updates. |
|Edit object groups only |The alert resources of generated alert policies will be synchronized with the updates. |
|Edit alert templates and object groups simultaneously |The alert rules and alert resources of generated alert policies will be synchronized with the updates. |


When you delete a configured alert template or object group, the impact on already generated alert policies is shown in the following table.


|Targets edited |Impact |
|---|---|
|Delete alert templates only |Generated alert policies will also be deleted. |
|Delete object groups only |The alert template needs to be unbound first. After unbinding, the generated alert policy will be deleted. |
|Delete alert templates and object groups simultaneously |Generated alert policies are deleted. |


<span id="1edc0e56"></span>
## Prerequisites

Alert contacts and contact groups have been created. For details, see [Creating contacts and contact groups](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group).

<span id="nNAjIE8C"></span>
## Procedure

<span id="43e62794"></span>
### Step 1: Create an alert template

An alert template is a template that saves alert rules for various cloud product metrics, so that you can quickly create alert policies.


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Alert Center** \> **Alert Template**.

3. Click **Create alert template**.

4. On the **Create alert template **  page, complete the following configuration, then click **Create**.

   
   |**Parameter** |**Descriptions** |**Sample value** |
   |---|---|---|
   |Name |Specify a custom name for the alert template to identify the alert template.<br><br><br>* The name must be 1 to 128 characters in length.<br><br>* The name cannot start with a digit, a hyphen (\-), or other special characters.<br><br>* The name can contain special characters. |Alerting templates |
   |Description |Specify a custom description for the alert template. |test |
   |Alert object |Configure the alert targets in the alert template.<br><br><br>* **Resource type**: From the drop\-down menu, select the cloud product type to be monitored.<br><br>* **Add dimension**: Click **Add dimension** to specify the resource dimensions for the cloud product being monitored.<br><br>   * **Dimension**: Specify the resource dimensions for the cloud product being monitored.<br><br>   * **Rule name**: Specify a custom name for the alert rule.<br><br>      * The name must be 1 to 64 characters in length.<br><br>      * The name cannot start with a digit, a hyphen (\-), or other special characters.<br><br>      * The name can contain special characters.<br><br>   * **Metric type**: Set the metric type for the alert. Available options include **Single\-metric **  or **Multi\-metric**.<br><br>   * **Trigger condition**: Set the metric, duration, statistical method, comparison operator, and threshold for the alert. If the monitored resource metric meets the trigger condition, the system will send an alert notification.<br><br>      * If the Metric type parameter is set to **Single metric**, only one trigger condition can be set.<br><br>      * If the Metric type parameter is set to **Multiple metrics**, one or more trigger conditions can be set.<br><br>      * **Duration: ** The duration can be set to 1 cycle, 3 cycles, 5 cycles, 10 cycles, 15 cycles, 30 cycles, 60 cycles, or 120 cycles.<br><br>      * **Comparison operator: ** The comparison operator can be set to \>, \>=, <, <=, !=, =, Compare to Last Period Increase, Compare to Last Period Decrease, Compare to Last Period Increase or Decrease, Compare to The Same Period of Yesterday Increase, Compare to The Same Period of Yesterday Decrease, Compare to The Same Period of Yesterday Increase or Decrease, Compare to The Same Period of Last Week Increase, Compare to The Same Period of Last Week Decrease, or Compare to The Same Period of Last Week Increase or Decrease.<br><br>      * **Alert level**: indicates the severity level of the alert. Valid values: **Critical**, **Warning**, **Notification**. You can select different thresholds for different alert levels under the same condition. |\- |
   |Mute For |After an alert policy is triggered, if the monitored resource continues to trigger alerts, the system will periodically send alert notifications. |5 minutes |
   |Notify mode |* **Rule**: If any resource in an alert rule continuously exceeds the threshold during a notification cycle, only one alert will be sent within that cycle.<br><br>* **Rule and resource**: If different resources in the alert rule continuously exceed the alert threshold during the alert sending cycle, alert notifications will be sent for each resource. If metrics do not recover after the alert sending cycle, Cloud Monitor will send alert notifications again. |Rule |
   |Alert recovery notification |An alert recovery notification is sent when the status of an alert policy returns to Normal. Cloud Monitor determines that an alert has been resolved. |Enable |
   |NoData alert |If a resource reports no data for N consecutive periods, a NoData alert will be triggered. |Enable |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">An alert template supports multiple cloud products and multiple dimensions.   </div>
   

<span id="ebdee4e7"></span>
### Step 2: Create an object group

An object group is a collection of alert targets. It can contain instances of multiple products across multiple regions, and is applied to alert templates to define the scope of alert resources.


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Object Group**.

3. On the **Object group list** page, click **Create object group**.

4. On the **Create object group** page, finish configuration and then click **Create**.



|**Parameter** |**Descriptions** |**Sample value** |
|---|---|---|
|Object group name |Object group name.<br><br><br>* The number of characters needs to be from 1 to 64.<br><br>* Only Chinese, English characters, and underscore `_` are supported. |group_demo |
|resource type |* **Resource type**: From the drop\-down menu, select the cloud product type to be monitored.<br><br>* **Selection method**: Configure the resource selection method. Supports **Manually select**, **Resource name**, **Project**, and **Label**.<br><br>* **Region**: Select the region of the monitored resource.<br><br>* **Select resource**: From the list of available instances on the left, select the target instances and move them to the selected instances area on the right. |\- |


<span id="508f0bac"></span>
### Step 3: Apply the alert template to the group

When the resource types of an alert template and an object group overlap, you can apply the template to the group. Cloud Monitor will then automatically generate the corresponding alert policies based on the intersecting resource types and dimensions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">An Object group can only be bound to one alert template.</div>



1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Alert center** \> **Alert policy**.

3. In the alert template list, find the target alert template and click **Apply to Group** in the **Actions** column on its right.

4. In the **Apply alert template to object group** pop\-up window, click **Add object group**.

5. Expand the added object group, select the created object group and notification channel, then click **Apply**.

6. In the alert policy list, view the alert policy name.

   When the resource types in an alert template and an object group overlap, Cloud Monitor automatically generates alert policies based on the common resource types and dimensions. The generated policies will be named in the format `{Alert Rule Name}&{Object Group Name}`, i.e., `RuleForEcs&Group` in this document.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Alert policies generated from an alert template do not support editing or deletion. They only support enabling and disabling.   </div>
