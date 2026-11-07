---
title: "Creating a traffic queue policy"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Creating-a-qos-queue-policy"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

A traffic queue policy forwards traffic to queues with different bandwidth allocations based on the DSCP value of the traffic. This implements bandwidth allocation and rate limiting for different services, ensuring that bandwidth for one service is not preempted by another and guaranteeing bandwidth for critical business traffic.

<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* You can create up to 10 traffic queue policies for a single Transit Router (TR) instance by default.

* A traffic queue policy consists of 1 default queue and additionally supports up to 64 custom queues.​

* You can add up to 10 queues (excluding the default queue) when creating a new traffic queue policy.

* Currently, only inter\-region attachments support traffic queue policies.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the section below **Basic information**, select the **Traffic queue policy** tab.

4. Click **Create traffic queue policy** and complete the configuration based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Name |Type a name for the traffic queue policy. |queuepolicy01 |
   |**Traffic queue** |||
   |Queue name |Type a name for the traffic queue. |Video service traffic |
   |Match DSCP |The DSCP carried in packets entering the attachment. Value range: 0\-63.<br><br>Traffic matching this DSCP value is directed to the current queue. A single queue can match multiple DSCP values, separated by commas (,).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If a traffic marking policy is applied to this attachment and the traffic is marked, the value is the Retagged DSCP set for the traffic by the marking entry. Otherwise, the value retains the original DSCP of the traffic.</div><br><br><br> |1 |
   |Bandwidth  |The percentage of cross\-region bandwidth for a queue. <br><br>For example, if a high queue in this policy occupies 80% of the cross\-region bandwidth, and you set this parameter to 50 for a normal queue, the maximum bandwidth for that queue is 50%, (100% \- 80%) \* 50% = 10% of the total cross\-region bandwidth. Setting it to 0 means the queue cannot use any bandwidth, and its traffic will be dropped.<br><br>The sum of the bandwidth percentages for all queues in a single policy must not exceed 100%. |50% |
   

5. Click **OK** to complete the action.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

After creating the traffic queue policy, apply it to the inter\-region attachment to schedule traffic by queue. For details, see [Enable traffic queue](https://docs.byteplus.com/docs/transitrouter/Configuring-a-qos-queue-policy-for-inter-region-attachment#.5ZCv55So5rWB6Zif5YiX).

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[CreateTransitRouterTrafficQosQueuePolicy](https://docs.byteplus.com/docs/transitrouter/CreateTransitRouterTrafficQosQueuePolicy): Create a traffic queue policy.
