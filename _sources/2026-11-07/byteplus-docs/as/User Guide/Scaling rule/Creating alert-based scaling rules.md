---
title: "Creating alert-based scaling rules"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Creating-an-alarm-scaling-policy"
---

<span id="nvP8wIDX"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Scaling Rules" tab.

4. Click Create Scaling Rules to go to the creation page. Refer to the table below to configure the arguments.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Rule Name |The name of the scaling rule. |as\-rule01 |
   |Rule Type |The "Alarm task" option is provided, which indicates triggering adjustments based on monitoring metrics. |Alarm task |
   |Monitoring metric |Specifies trigger conditions and thresholds for one or multiple monitoring metrics.<br><br><br>* Trigger conditions:<br><br>   * Metric aggregation: Specifies whether alerts and Auto Scaling adjustments are triggered when all or any metric thresholds are reached.<br><br>   * Monitoring period: Specifies the continuous duration from when the specified monitoring metric reaches the threshold to when an alert and adjustment are triggered. The time period is calculated in cycles. The Cloud Monitor service collects monitoring metrics every **1 minute**. When the monitoring metric data reaches the threshold for several consecutive cycles, an alert is triggered, and the adjustment is executed.<br><br>* Metrics: Up to 5 metrics can be added. For supported monitoring metrics, refer to [Monitoring metric introduction](https://docs.byteplus.com/en/docs/as/Metrics).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A single monitoring metric can be selected only once per alert\-based rule and cannot be selected multiple times.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To retrieve Agent monitoring metrics, you need to install the Agent plugin and complete authorization on the instance first. Otherwise, the monitoring metrics cannot be retrieved. For installation instructions, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Overview-1">ECS monitoring overview</a>.</div><br> |* Trigger conditions: When both of the following thresholds are reached for one cycle (1 cycle = 1 min), an alert is triggered, and the adjustment is executed.<br><br>* Metrics:<br><br>   * Average out\-of\-band CPU utilization \> 80%. This indicates that the average CPU usage of all instances in the scaling group exceeds 80%.<br><br>   * Minimum out\-of\-band CPU utilization \> 80%. This indicates that the instance with the lowest CPU usage in the scaling group has a CPU usage exceeding 80%. |
   |Adjustment |Specifies the adjustment to be executed when the rule is triggered. You can adjust scaling group capacity or the number of instances in the group. The adjustment amount can be specified as an exact value or a percentage.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The specified number must be within the maximum and minimum capacity range or the minimum and maximum instance count range. If the specified adjustment number exceeds the limits, it is automatically adjusted for the scaling group. For detailed description, refer to <a href="https://docs.byteplus.com/en/docs/as/Overview-of-scaling-policys">Scaling rule overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the current capacity of the scaling group is calculated as a percentage, any non\-integer result is rounded up to the next whole number. For example, 12.7 is rounded up to 13, and 0.67 is rounded up to 1.</div><br> |Increase capacity, 1 |
   |Cooldown Time |The interval from the successful execution of an adjustment job based on the scaling rule (which is when the last instance completes the adjustment) to the next adjustment job becoming executable. During this period, services running on newly created instances can be initialized. For details, refer to [Cooldown time](https://docs.byteplus.com/en/docs/as/Cooldown-period).<br><br><br>* If the cooldown time of the scaling rule conflicts with that of the scaling group, the cooldown time of the scaling rule takes precedence.<br><br>* If the scaling rule has no cooldown time configured, the cooldown time of the scaling group is used by default. |300s |
   |Effective time |Set the effective time range of the alarm task.<br><br><br>* It is effective at all times by default.<br><br>* To take effect at a specific time, please use the [Cron expression](https://docs.byteplus.com/en/docs/as/Cron-expressions) configuration, suitable for scenarios such as disabling scale\-in during peak business hours. |\-\- |
   |Status After Creation |Specifies whether the scaling rule is enabled immediately upon creation.<br><br>If the scaling rule is disabled upon creation, you can enable it later by referring to [Enabling scaling rules](https://docs.byteplus.com/en/docs/as/Enabling-a-scaling-policy). |Enable |
   

5. Click the "Confirm" button to complete the operation.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

After the scaling rule is triggered, you can view the scaling result details via the [scaling log](https://docs.byteplus.com/en/docs/as/Viewing-scaling-activities), including the conditions that triggered scaling, adjustment type, start/stop time, and execution result.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateScalingPolicy](https://docs.byteplus.com/en/docs/as/CreateScalingPolicy)
