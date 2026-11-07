---
title: "Creating periodic scaling rules"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Creating-a-recurring-scaling-policy"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Trigger time of periodic scaling adjustments

The trigger time for periodic adjustments is determined by the execution time, recurrence cycle, and recurrence end time together.

When the execution time arrives, the first adjustment is triggered immediately. Then, the system triggers the adjustment repeatedly based on the specified recurrence cycle. When the recurrence end time arrives, triggering stops immediately.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The execution time needs to be no earlier than the current time and no later than the recurrence end time.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Scaling Rules" tab.

4. Click Create Scaling Rules to go to the creation page. Refer to the table below to configure the parameters.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Rule Name |The name of the scaling rule. |as\-rule01 |
   |Rule type |Select the "Periodic task" option. This indicates that the adjustment is executed repeatedly within a specified time period. |Periodic task |
   |Recurrence |Specifies that scaling actions repeat by day, week, or month. The [Cron expression](https://docs.byteplus.com/en/docs/as/Cron-expressions) feature is supported. |By day |
   |Select time/week/date/Cron expression |Select a time to repeatedly trigger scaling actions.<br><br><br>* If the recurrence cycle is set to "By month" and a date later than the 28th is selected, the scaling operation will not be executed for that month if the selected date does not exist.<br><br>* The exact time of repeated execution is the hour and minute specified in the execution time. If you use a Cron expression to specify the hour and minute, the Cron expression takes precedence. |Run every four days |
   |Time zone |Currently, only "UTC +08:00" (Beijing time) is supported. |UTC +08:00 |
   |Execution time |Select the time to start executing the scaling operation. You can choose a specific time for a given date (year, month, day), accurate to the minute.<br><br><br>* If no specific time point is selected, this parameter defaults to the current time point. |2023\-05\-30 14:00 |
   |Expired at |Select the time to end executing the scaling operation. You can choose a specific time for a given date (year, month, day), accurate to the minute.<br><br><br>* If no exact time is specified, the parameter defaults to the time one day/week/month from the current time, based on the selected recurrence cycle.<br><br>* Set to empty to indicate that this task will never stop. |2023\-06\-30 14:00 |
   |Adjustment |Specifies the adjustment to be executed when the rule is triggered. You can adjust the scaling group capacity/number of instances in the group. The adjustment amount can be specified as an exact value or a percentage.<br><br><br>* When the current capacity/number of instances of the scaling group is calculated as a percentage, any non\-integer result is rounded up to the next whole number. For example, 12.7 is rounded up to 13, and 0.67 is rounded up to 1.<br><br>* The specified number or percentage must be within the maximum and minimum instance capacity range or minimum and maximum instance count range. If the specified adjustment number or percentage exceeds the limits, it is automatically adjusted for the scaling group. For detailed description, refer to [Overview of scaling rules](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-policys). |Add instance, count: 1 |
   |Cooldown time |The interval from the successful execution of an adjustment job based on the scaling rule (which is when the last instance completes the adjustment) to the next adjustment job becoming executable. During this period, services running on newly created instances can be initialized.<br><br>For details, refer to [Cooldown time](https://docs.byteplus.com/en/docs/as/Cooldown-period).<br><br><br>* If the cooldown time of the scaling rule conflicts with that of the scaling group, the cooldown time of the scaling rule takes precedence.<br><br>* If the scaling rule has no cooldown time configured, the cooldown time of the scaling group is used by default. |300s |
   |Status After Creation |Specifies whether the scaling rule is enabled immediately upon creation.<br><br>If the scaling rule is disabled upon creation, you can enable it later by referring to [Enabling scaling rules](https://docs.byteplus.com/en/docs/as/Enabling-a-scaling-policy). |Enable |
   

6. Click "Confirm" to complete the operation.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

After the scaling rule is triggered, you can view the scaling result details via the [scaling log](https://docs.byteplus.com/en/docs/as/Viewing-scaling-activities), including the conditions that triggered scaling, adjustment type, start/stop time, and execution result.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateScalingPolicy](https://docs.byteplus.com/en/docs/as/CreateScalingPolicy)
