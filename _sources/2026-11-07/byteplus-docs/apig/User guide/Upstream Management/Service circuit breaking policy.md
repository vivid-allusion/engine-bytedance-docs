---
title: "Service circuit breaking policy"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Circuit_breaking_policy"
---

Upstream supports configuration of service circuit breaking policy to isolate faults and ensure the overall availability of backend services. This article explains how to configure the service circuit breaking policy.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Upstream created. Refer to [Upstream Management](https://docs.byteplus.com/en/docs/apig/Upstream_Management) for details.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [APIG console](https://console.byteplus.com/veapig).

3. After selecting the target instance in **Instance Management**, click **Upstream list**.

3. On the Upstream list page, click the target Upstream name to enter the Upstream overview page.

4. In the circuit breaking region, click **Enable**, check **Enable circuit breaking** in the popup, and configure the service circuit breaking policy.

   
   |Parameter |Description |
   |---|---|
   |Threshold setting |Set the circuit breaking threshold based on actual conditions. The two parameters are **consecutive failure count** and **calculation cycle**.<br><br>For example, "5 consecutive failures, calculation cycle 10 s" means that if a backend node experiences 5 consecutive failures within 10 seconds, at the start of the next calculation cycle of 10 seconds, the node will be removed from the load balancing pool. |
   |Circuit breaking time |Set minimum pop\-up time.<br><br><br>* The minimum pop\-up time is ≤ 300 s; the single circuit breaking time is equal to the minimum pop\-up time multiplied by the number of consecutive circuit breaks; the maximum single circuit breaking time does not exceed 300 s.<br><br>* If the minimum pop\-up time is greater than 300 s, the single circuit breaking time will be set to your configured minimum pop\-up time.<br><br>   For example: in the scenario of 5 consecutive failures and a calculation cycle of 10 seconds.<br><br>* Minimum removal time 30 s: If a backend node fails 5 times consecutively within 10 seconds, the node will be removed from the load for the first time, with a circuit breaking time of 30 ✖️ 1 s; after the node recovers, if it fails 5 times consecutively within 10 seconds again, the node will be removed from the load for the second time, with a circuit breaking time of 30 ✖️ 2 s. This process repeats, and the node's maximum single circuit breaking time will not exceed 300 s.<br><br>* The minimum pop\-up time is 500 seconds: the circuit breaking time for each event is 500 seconds. If triggered again later, the circuit breaking time remains 500 seconds and does not accumulate. |
   |Maximum circuit breaking ratio |Set the maximum allowed proportion of nodes whose load can be evicted. |
   |Minimum available ratio |Set the minimum proportion of healthy nodes among all nodes. When the proportion of healthy nodes falls below this value, global load balancing will be performed, regardless of node health.<br><br>For example: when there are a total of 10 nodes, the maximum circuit breaking ratio is 20%, and the minimum available ratio is 60%:<br><br><br>* A maximum of 2 nodes can be subject to circuit breaking, and at least 6 healthy nodes must be maintained. That is, there are always 8 to 10 nodes participating in load balancing.<br><br>* The first 2 nodes can undergo circuit breaking normally, and subsequent unhealthy nodes will no longer undergo circuit breaking, ensuring that at least 8 nodes are maintained in the load balancer.<br><br>* When the fifth unhealthy node appears, the minimum available ratio threshold is triggered, and load balancing across 10 nodes will begin.<br><br>* The priority for the minimum available ratio to take effect is higher than that for the maximum circuit breaking ratio.<br><br>* It is recommended that the sum of the maximum circuit breaking ratio and the minimum available ratio be less than 100%, to avoid conflicts between the two parameter configurations. |
   

5. Click **Confirm**.
