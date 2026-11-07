---
title: "Creating scheduled scaling rules"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Creating-a-scheduled-scaling-policy"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Scaling Rules" tab.

4. Click Create Scaling Rules to go to the creation page. Refer to the table below to configure the parameters.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Rule Name |The name of the scaling rule. |as\-rule01 |
   |Rule Type |The "Scheduled task" option is provided, which indicates executing an adjustment at a specified time. |Scheduled task |
   |Trigger time |Select a trigger time for the adjustment. You can choose a specific time for a given date (year, month, day), accurate to the minute. If no specific time point is selected, the current time point is used by default.<br><br><br>* You can click the "Select date" and "Select time" buttons to switch the selection page. After the time is selected, click the "Confirm" button to complete the configuration.<br><br>* The specified trigger time cannot be earlier than the current time. |2023\-05\-30 14:00 |
   |Adjustment |Specifies the adjustment to be executed when the trigger time of the rule arrives. You can adjust the capacity/number of instances in the group. The adjustment amount can be specified as an exact value or a percentage.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The specified number must be within the maximum and minimum capacity range or the minimum and maximum instance count range. If the specified adjustment number exceeds the limits, it is automatically adjusted for the scaling group. For detailed description, refer to <a href="https://docs.byteplus.com/en/docs/as/Overview-of-scaling-policys">Scaling rule overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the current capacity of the scaling group is calculated as a percentage, any non\-integer result is rounded up to the next whole number. For example, 12.7 is rounded up to 13, and 0.67 is rounded up to 1.</div><br> |Add instance, count: 1 |
   |Cooldown Time |The interval from the successful execution of an adjustment job based on the scaling rule (which is when the last instance completes the adjustment) to the next adjustment job becoming executable. During this period, services running on newly created instances can be initialized. For details, refer to [Cooldown time](https://docs.byteplus.com/en/docs/as/Cooldown-period).<br><br><br>* If the cooldown time of the scaling rule conflicts with that of the scaling group, the cooldown time of the scaling rule takes precedence.<br><br>* If the scaling rule has no cooldown time configured, the cooldown time of the scaling group is used by default. |300s |
   |Status After Creation |Specify whether the scaling rule is enabled immediately upon creation.<br><br>If the scaling rule is disabled upon creation, you can enable it later by referring to [Enabling scaling rules](https://docs.byteplus.com/en/docs/as/Enabling-a-scaling-policy). |Enable |
   

6. Click "Confirm" to complete the operation.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

After the scaling rule is triggered, you can view the scaling result details via the [scaling log](https://docs.byteplus.com/en/docs/as/Viewing-scaling-activities), including the conditions that triggered scaling, adjustment type, start/stop time, and execution result.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateScalingPolicy](https://docs.byteplus.com/en/docs/as/CreateScalingPolicy)
