---
title: "Procedure for creating a scaling task"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Building-a-scaling-task-process"
---

You can use the Auto Scaling service to perform multiple types of adjustments to meet the needs of different business scenarios. This topic describes the basic procedure for performing adjustments. Learn more about [adjustment types](https://docs.byteplus.com/en/docs/as/Adjustment-types).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After the following steps, confirm that the scaling group, scaling configuration, and scaling rules are all in the <strong>Active/Added</strong> status to ensure adjustments can be triggered normally.</div>



|Adjustment type |Business scenario |Procedure |
|---|---|---|
|Health Check |By monitoring the status and quantity of instances, this feature can automatically replace unhealthy instances or perform instance scale\-in/scale\-out to ensure stable daily operations. |Step 1: [Create scaling group](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group)<br><br>Step 2: [Create scaling configuration](https://docs.byteplus.com/en/docs/as/Managing_a_scaling_configuration) |
|Scheduled tasks |Instances are scaled in or out automatically at a specified time. This feature is applicable to business scenarios involving predictable or regular changes, such as holiday promotions or daily scheduled releases. |Step 1: [Create scaling group](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group)<br><br>Step 2: [Create scaling configuration](https://docs.byteplus.com/en/docs/as/Managing_a_scaling_configuration)<br><br>Step 3: [Create scheduled scaling rule](https://docs.byteplus.com/en/docs/as/Creating-a-scheduled-scaling-policy) |
|Periodic task |Tasks are executed automatically at fixed times on a daily, weekly, or monthly basis. This feature is applicable to long\-term regular business scenarios, such as monthly end\-of\-month settlements or daily scheduled ticket sales. |Step 1: [Create scaling group](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group)<br><br>Step 2: [Create scaling configuration](https://docs.byteplus.com/en/docs/as/Managing_a_scaling_configuration)<br><br>Step 3: [Create periodic scaling rule](https://docs.byteplus.com/en/docs/as/Creating-a-recurring-scaling-policy) |
|Alert task |By monitoring instance metrics, this feature detects whether the instance status meets expectations to achieve dynamic scaling. It is applicable to sudden or unpredictable business scenarios, such as breaking news. |Step 1: [Create scaling group](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group)<br><br>Step 2: [Create scaling configuration](https://docs.byteplus.com/en/docs/as/Managing_a_scaling_configuration)<br><br>Step 3: [Create alert-driven scaling rule](https://docs.byteplus.com/en/docs/as/Creating-an-alarm-scaling-policy) |
|Target tracking task |Based on your operational experience, you can select a monitoring metric and specify a target value for it. The platform automatically calculates the number of instances to add or remove during scaling, thereby keeping the specified metric close to the target value.<br><br>This feature is applicable to business scenarios prioritizing operational health. For example, maintain the average CPU usage of instances in the scaling group at or below 80%. |Step 1: [Create scaling group](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group)<br><br>Step 2: [Create scaling configuration](https://docs.byteplus.com/en/docs/as/Managing_a_scaling_configuration)<br><br>Step 3: [Create target tracking scaling rule](https://docs.byteplus.com/en/docs/as/Creating-a-target-tracking-scaling-policy) |
|Manual scaling |You can manually add, move out, or delete instances in the scaling group. This feature is applicable to scenarios where business changes are irregular and instances need to be added or removed at any time. |Step 1: [Create scaling group](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group)<br><br>Step 2: [Create scaling configuration](https://docs.byteplus.com/en/docs/as/Managing_a_scaling_configuration)<br><br>Step 3: [Add instance](https://docs.byteplus.com/en/docs/as/Adding-instances-manually)<br><br>Step 4: [Move out](https://docs.byteplus.com/en/docs/as/Removing-instances-automatically)/[delete](https://docs.byteplus.com/en/docs/as/Deleting-instances-manually) instance |


<span id=".5pON5L2c5q2l6aqk6K-05piO"></span>
## Procedure description


1. [Create scaling group](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group)

   A scaling group is used to manage a group of instances for the same business scenario. The configuration of a scaling group is defined, including the VPC to which the instances belong, the maximum and minimum number of instances, the cooldown time, and other information. About [cooldown time](https://docs.byteplus.com/en/docs/as/Cooldown-period).

2. [Create scaling configuration](https://docs.byteplus.com/en/docs/as/Managing_a_scaling_configuration)

   Scaling configuration is used to define the instance configurations for a scaling group, including those related to compute, memory, network, storage, and security. When the scaling group scales out, new instances are created based on the preset instance configuration. About [scaling configuration source overview](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources).

3. [Create scaling rule](https://docs.byteplus.com/en/docs/as/Managing_a_scaling_configuration)

   Scaling rules are used to define the conditions for adjustment jobs: the timing and method for triggering scaling\-out or scaling\-in operations. About [scaling rules](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-policys).

4. [Add instance](https://docs.byteplus.com/en/docs/as/Adding-instances-manually)

   You can add an existing instance to the scaling group to provide services with other instances in the group.

5. [Move out](https://docs.byteplus.com/en/docs/as/Removing-instances-automatically)/[delete](https://docs.byteplus.com/en/docs/as/Deleting-instances-manually) instance

   You can manually move out or delete an instance from the scaling group.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

We recommend configuring [scaling notifications](https://docs.byteplus.com/en/docs/as/Overview_of_notification_channels) for the scaling group. This allows you to learn the scaling status of instances in the group timely and manage scaling operations efficiently.
