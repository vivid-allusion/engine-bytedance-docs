---
title: "Creating target tracking scaling rules"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Creating-a-target-tracking-scaling-policy"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

A target tracking rule allows you to select a monitoring metric based on your operational experience and specify a target value for it. The platform automatically calculates the number of instances to add or remove during scaling, thereby keeping the specified metric close to the target value.

<span id=".5Yqf6IO95LyY5Yq_"></span>
## Advantages


* Reduced manual intervention: For a simple alert\-based rule, you need to focus on the expected target value, whereas for target tracking rules, you only need to focus on the target value of the target monitoring metric.

* When configuring an alert\-based rule, you can only specify a fixed scaling operation based on experience, causing limited scaling granularity. By contrast, target tracking rules deliver more precise and dynamic scaling granularity. The adjustment value can be calculated based on historical monitoring data and your expected target value. This feature minimizes the number of adjustments required for scaling activities, resulting in fast, precise, and dynamic scaling operations.


<span id="J25qPacH"></span>
## Usage notes


* You can create only one target tracking rule for each scaling group.

* After a target tracking rule is created successfully, the platform automatically creates a Cloud Monitor alert task. After the target tracking rule is deleted, the alert task is also deleted automatically. Trigger conditions for alert tasks are as follows:

   * When the metric value exceeds the target value, a scale\-out operation is triggered.

   * When the metric value is less than 80% of the target value, a scale\-in operation is triggered.

* The system keeps the monitoring metric value specified in the target tracking rule as close to your configured target value as possible. However, absolute precision is not guaranteed. When the monitoring metric value cannot exactly match the configured target value, the system prevents it from exceeding the target value as much as possible.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Scaling Rules" tab.

4. Click Create Scaling Rules to go to the creation page. Refer to the table below to configure the arguments.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Rule Name |The name of the scaling rule. |as\-rule01 |
   |Rule Type |The "Target tracking task" option is provided, which indicates executing adjustments based on the target value of a monitoring metric. |Target tracking task |
   |Monitoring metric/target value |Specifies a target value for the monitoring metric. When the [trigger condition](https://docs.byteplus.com/en/docs/as/Creating-a-target-tracking-scaling-policy#J25qPacH) of the target value is met, an alert is triggered, and the adjustment is executed to keep the Cloud Monitor metric value close to the target value.<br><br><br>* For supported monitoring metrics, refer to [Supported monitoring metrics](https://docs.byteplus.com/en/docs/as/Metrics).<br><br>* To retrieve Agent monitoring metrics, you need to install the Agent plugin and complete authorization on the instance first. Otherwise, the monitoring metrics cannot be retrieved. For installation instructions, refer to [ECS monitoring overview](https://docs.byteplus.com/en/docs/cloudmonitor/Overview-1). |Average out\-of\-band CPU utilization, 80%.<br><br>This indicates that the target average CPU usage of all instances in the scaling group is 80%. |
   |Cooldown Time |The interval from the successful execution of an adjustment job based on the scaling rule (which is when the last instance completes the adjustment) to the next adjustment job becoming executable. During this period, services running on newly created instances can be initialized.<br><br>For details, refer to [Cooldown time](https://docs.byteplus.com/en/docs/as/Cooldown-period).<br><br><br>* If the cooldown time of the scaling rule conflicts with that of the scaling group, the cooldown time of the scaling rule takes precedence.<br><br>* If the scaling rule has no cooldown time configured, the cooldown time of the scaling group is used by default. |300s |
   |Threshold for Scale\-out/Scale\-in Alerts |Select trigger conditions for the adjustments. Cloud Monitor collects monitoring metrics every minute. The rule is triggered when the [trigger conditions](https://docs.byteplus.com/en/docs/as/Creating-a-target-tracking-scaling-policy#J25qPacH) for the target value are met for a specified consecutive number of times. |3 |
   |Disable scale\-in |Specifies whether to disable the scale\-in operation triggered by the target tracking rule.<br><br><br>* If you select "True", alert tasks triggered by scaling rules for scale\-in operations are disabled. As a result, only scale\-out operations are performed, and scale\-in operations will not be executed. Afterwards, you can edit the [scaling rule](https://docs.byteplus.com/en/docs/as/Modifying-a-scaling-policy) to change this parameter. After this, alert tasks for scale\-in operations will be automatically enabled.<br><br>* After disabling this feature, you can use other methods to manage the scale\-in operations of the scaling group. For example, other metrics can also be monitored via [alert tasks](https://docs.byteplus.com/en/docs/as/Creating-an-alarm-scaling-policy) for scale\-in operations. |No |
   |Status After Creation |Specifies whether the scaling rule is enabled immediately upon creation.<br><br>If the scaling rule is disabled upon creation, you can enable it later by referring to [Enabling scaling rules](https://docs.byteplus.com/en/docs/as/Enabling-a-scaling-policy). |Enable |
   

6. Click the "Confirm" button to complete the operation.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

After the scaling rule is triggered, you can view the scaling result details via the [scaling log](https://docs.byteplus.com/en/docs/as/Viewing-scaling-activities), including the conditions that triggered scaling, adjustment type, start/stop time, and execution result.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateScalingPolicy](https://docs.byteplus.com/en/docs/as/CreateScalingPolicy1)
