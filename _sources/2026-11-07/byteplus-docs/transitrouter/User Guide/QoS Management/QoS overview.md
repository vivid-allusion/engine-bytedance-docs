---
title: "QoS overview"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Qos-overview"
---

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

Transit Router (TR) provides Quality of Service (QoS) management through two functional modules: traffic marking policies and traffic queue policies. Traffic marking policies classify and tag traffic, while traffic queue policies handle traffic scheduling. You can use either module independently or combine both to optimize bandwidth utilization and ensure the performance of critical business traffic.


|Feature module |Description |Application scenarios |
|---|---|---|
|Traffic marking policy |It classifies and marks traffic entering the inter\-region attachment using different marking entries. |QoS management optimizes network resource allocation and guarantees the quality of critical services.<br><br><br>* Use only the traffic marking policy​ on the TR if you only need to mark DSCP values for different traffic flows to influence QoS behavior on downstream network devices.<br><br>* Use only the traffic queue policy​ on the TR if the traffic entering the TR is already classified and marked.<br><br>* Use both the traffic marking policy​ and traffic queue policy on the TR if the traffic entering the TR is not pre\-classified. |
|Traffic queue policy |It forwards traffic to queues with different bandwidth allocations based on the DSCP value of the traffic. This implements bandwidth allocation and rate limiting for different services, ensuring that bandwidth for one service is not preempted by another and guaranteeing bandwidth for critical business traffic. ||


<span id=".5Z-65pys5qaC5b-1"></span>
## Terms


|Name |Description |
|---|---|
|QoS |QoS is Quality of Service. |
|DSCP |A mechanism for classifying and marking business traffic. It uses 6 bits in the IP packet header, representing 64 distinct values (0\-63) to differentiate service priorities. |
|Retagged DSCP |The DSCP value that the TR sets for traffic after the traffic passes through and is processed by a TR traffic marking policy. |


<span id=".5Y6f55CG5LuL57uN"></span>
## Principles

As shown in the figure below, if you combine traffic marking and traffic queue policies on an inter\-region attachment, the outbound traffic path is as follows:


1. Traffic first passes through the traffic marking policy, where it is classified by matching marking entries and assigned a DSCP value.

2. The traffic then enters the traffic queue policy. Based on its DSCP value, traffic is scheduled into different queues with varying bandwidth allocations.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e28b36efb7994131ad783ae9c6932049) </span>

<span id=".5rWB5qCH6K6w562W55Wl"></span>
### Traffic marking policy

A traffic marking policy can contain multiple marking entries. It matches business traffic using a 6\-tuple (protocol type, source CIDR, source port, destination CIDR, destination port, and DSCP value). For details on the 6\-tuple, see [Creating a traffic marking policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-qos-marking-policy).

Once a traffic marking policy is enabled on an inter\-region attachment, the matching principles for outbound traffic are as follows:


* Match business traffic against entries in the traffic marking policy from the highest to lowest priority.

   * Match found: The system marks the traffic with the retagged DSCP configured for this marking entry.

   * No match: If the traffic does not match any entry in the policy, its DSCP value remains unchanged.

* Stop matching after the first successful entry. Traffic will not be evaluated against subsequent entries.

* Leave all 6\-tuple fields in an entry unset to match all outbound traffic on the inter\-region attachment.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_51c1846c1ed8dde407ad744cb88b534f.png) </span>

<span id=".5rWB6Zif5YiX562W55Wl"></span>
### Traffic queue policy

A traffic queue policy can contain multiple queues with different priorities. It ensures traffic forwarding for high\-priority queues first. You can assign different bandwidth limits to different queues. Each queue enforces its own bandwidth limit independently, preventing queues from contending with each other.


* Match traffic to a queue based on its DSCP value. Forward matched traffic through its assigned queue.

* Forward traffic that has no DSCP value​ or fails to match any custom queue​ through the default queue.

* The sum of the bandwidth for all queues in a single policy must not exceed​ the bandwidth cap of the inter\-region attachment.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

See [Limits](https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-04).

<span id=".6YWN572u5rWB56iL"></span>
## Configuration procedures

To configure business QoS management through TR, follow these steps:


1. Configure traffic classification and marking

   1. [Create traffic marking policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-qos-marking-policy): Create a traffic marking policy and add marking entries as needed.

   2. [Enable traffic marking for an inter-region attachment](https://docs.byteplus.com/en/docs/transitrouter/Configuring-a-qos-marking-policy-for-inter-region-attachment): Enable the traffic marking feature on the inter\-region attachment and specify the traffic marking policy.

2. Configure traffic scheduling

   1. [Create traffic queue policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-qos-queue-policy): Create a traffic queue policy and set bandwidth for its queues as needed.

   2. [Enable traffic queues for an inter-region attachment](https://docs.byteplus.com/en/docs/transitrouter/Configuring-a-qos-queue-policy-for-inter-region-attachment): Enable the traffic queue feature on the inter\-region attachment.
