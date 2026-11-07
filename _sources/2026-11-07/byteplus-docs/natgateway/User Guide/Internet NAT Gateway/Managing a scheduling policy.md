---
title: "Managing a scheduling policy"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Managing_the_scheduling_policy"
---

A scheduling policy is a network traffic congestion management mechanism. In scenarios of network congestion, it provides different forwarding service quality guarantees based on the requirements of different priority services. After the Scheduling Policy is enabled, you can configure different priorities and corresponding bandwidth values for traffic queues of different purposes. This enables granular traffic management in multi\-service scenarios, ensuring that high\-priority services can preferentially obtain the required bandwidth.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The scheduling policy feature is available only for <strong>Pay\-by\-CU Internet NAT Gateways</strong>. </div>


* <div data-tips="true" data-tips-type="default">The NAT Gateway Scheduling Policy feature currently does not support simultaneous use with the IP Rate Limiting feature. If IP rate limiting rules are already configured on the Internet NAT Gateway,  <a href="https://docs.byteplus.com/en/docs/natgateway/Managing_IP_rate_limiting#atRnjQYg">delete</a> them before enabling the Scheduling Policy.</div>



<span id="C7Xrf3YZ"></span>
## Instructions


* A single Internet NAT Gateway instance supports the creation of up to 64 custom traffic queues.

* The supported upper limits for bandwidth vary depending on the billing method and specification of the Internet NAT Gateway instance. For details, see [Product performance](https://docs.byteplus.com/en/docs/natgateway/Specifications#.5YWs572RTkFU572R5YWz).

   * The guaranteed bandwidth and maximum bandwidth of the Internet NAT Gateway can reach the configured value only when the number of connections is sufficiently high. If the number of connections is too low, the configured bandwidth value cannot be reached.

* When the Scheduling Policy feature is enabled, the deletion of the Internet NAT Gateway is temporarily not supported. To delete an Internet NAT Gateway instance,  [disable scheduling policy](https://docs.byteplus.com/en/docs/natgateway/Managing_the_scheduling_policy#MAGQ27nu) first.

* Traffic queues are divided into two types: **Default Traffic Queue** and **Custom Traffic Queue**. The detailed description is as follows:

   
   |Queue type |Description |Supported action |
   |---|---|---|
   |Default traffic queue |After the Scheduling Policy is successfully enabled, the system will automatically configure a Default Traffic Queue (Guaranteed Bandwidth: 0%, Maximum Bandwidth: 100%) for the Internet NAT Gateway instance.<br><br><br>* When no custom traffic queues are created, the Default Traffic Queue ensures the normal forwarding of all traffic within the Internet NAT Gateway.<br><br>* The Default Traffic Queue does not affect the priority of custom traffic queues.<br><br>* The Default Traffic Queue does not count against your traffic queue quota. |Modify guaranteed bandwidth and maximum bandwidth |
   |Custom traffic queue |You can create custom traffic queues based on the Differentiated Services Code Point (DSCP) to differentiate the traffic priority. According to the different priorities you define, it ensures that high\-priority services can preferentially obtain the required bandwidth, enabling the stable operation of critical services.<br><br><br>* In idle network scenarios, bandwidth is allocated to each traffic queue based on their configured bandwidth ratios.<br><br>* In congested network scenarios, high\-priority traffic queues will occupy the bandwidth of lower\-priority queues. After satisfying the high\-priority queues, the remaining bandwidth is allocated to lower\-priority queues, also according to their bandwidth ratios.<br><br><br> |* Create and delete<br><br>* Modify DSCP match / guaranteed bandwidth / maximum bandwidth / priority |
   


<span id="egqIXhDf"></span>
## Enable scheduling policy


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the list of Internet NAT Gateways, click the name of the target Internet NAT Gateway.

4. Select the **Scheduling policy** tab.

5. Click **Enable scheduling policy** to complete the action.


<span id="L961SpVv"></span>
## Add a traffic queue

You can add up to 5 traffic queues in a single request.


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the list of Internet NAT Gateways, click the name of the target Internet NAT Gateway.

4. Select the **Scheduling policy** tab, then click **Add queue**.

5. Configure the relevant parameters according to the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Queue name |Traffic queue name. |NATwg\-Qos |
   |Match DSCP |Enter the DSCP extension field used to match traffic passing through the Internet NAT Gateway. This traffic will be forwarded by the NAT Gateway under the control of the rate limiting policy.<br><br><br>* Value range: 0\-63. To match multiple traffic flows, separate multiple DSCP values with commas (,).<br><br>* DSCP values assigned to traffic queues cannot be duplicated. |0 |
   |Rate limiting policy |Currently, only **Percentage** configuration is supported. When the metering method of NAT Gateway is Pay\-by\-CU, the instance's bandwidth cap possesses elastic capability. After configuring by percentage, the actual effective rate limit value will adjust dynamically with changes in the maximum bandwidth cap. |Percentage |
   |Guaranteed bandwidth (%) |Set the minimum guaranteed bandwidth for the traffic queue. The sum of the guaranteed bandwidth percentages for all traffic queues on an Internet NAT Gateway instance must not exceed 100%. |80 |
   |Maximum bandwidth (%) |Set the maximum bandwidth that the traffic queue is allowed to occupy. The default value is 100, indicating that the queue's traffic can occupy up to the instance's maximum bandwidth value. |100 |
   |Priority |Set the priority of the traffic queue. Priority range is 1\-10000, where the value 1 represents the highest precedence.​​ The priority levels for traffic queues cannot be duplicated. High\-priority traffic queues are allowed to preempt bandwidth from lower\-priority queues. |1 |
   

6. Click **Add** to complete the action.


<span id="D99zUyoE"></span>
## Edit a traffic queue


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the list of Internet NAT Gateways, click the name of the target Internet NAT Gateway.

4. Select the **Scheduling policy** tab.

5. Click **Edit** on the right side of the target traffic queue.

6. Edit the queue name, DSCP match, guaranteed bandwidth, maximum bandwidth, or priority.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The Default Traffic Queue only supports editing the guaranteed bandwidth and maximum bandwidth.   </div>
   

7. Click **Save** to complete the action.


<span id="RdtkQWf9"></span>
## Delete a traffic queue

You can delete custom traffic queues that no longer require rate limiting. The Default Traffic Queue cannot be deleted.


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the list of Internet NAT Gateways, click the name of the target Internet NAT Gateway.

4. Select the **Scheduling policy** tab.

5. Click **Delete** on the right of the target traffic queue.

6. Click **Delete** to complete the action.


<span id="MAGQ27nu"></span>
## Disable scheduling policy

Before disabling the Scheduling Policy, ensure that [all custom traffic queues have been deleted](https://docs.byteplus.com/en/docs/51/79161#RdtkQWf9).


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the list of Internet NAT Gateways, click the name of the target Internet NAT Gateway.

4. Select the **Scheduling policy** tab.

5. Click **Disable scheduling policy** to complete the action.
