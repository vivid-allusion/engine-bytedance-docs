---
title: "QoS Policy overview"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/QoS_policy_overview"
---

The Quality of Service (QoS) Policy is a network traffic congestion management mechanism that provides different forwarding quality guarantees according to business priorities during network congestion. In the outbound direction (i.e., from a VPC to a data center), you can define different priorities for different Direct Connect (DC) Connections through the QoS policy. This ensures that high\-priority services receive the required bandwidth first, achieving smooth operation of critical services.

<span id=".5Z-65pys5qaC5b-1"></span>
## Terms


|Name |Description |
|---|---|
|QoS |QoS is Quality of Service. |
|Traffic queue |Queuing is the logic in the cache that orders packets. When the rate of traffic exceeds the interface bandwidth or the bandwidth set for that traffic, packets temporarily remain as a queue in the cache, and traffic queues can schedule on outbound DC Connection traffic and perform bandwidth limit based on the queue.<br><br>Traffic queues are divided into high queues and normal queues according to different priorities. |
|High queue |The traffic queue whose priority is **High** in the QoS policy of DC Connection. In the network congestion scenario, bandwidth is allocated for high queues first. |
|Normal queue |The traffic queue whose priority is **Normal** in the QoS policy of DC Connection. Multiple normal queues under the same QoS policy can share unused bandwidth to avoid bandwidth waste.<br><br><br>* In the network congestion scenario where high queues exist, the remaining bandwidth is allocated to normal queues after allocating for high queues. The allocation is performed in bandwidth proportion.<br><br>* In the network congestion scenario without high queues, bandwidth is proportionally allocated for each normal queue. |
|Default queue |After successfully creating a QoS policy, the system automatically adds a default queue to the policy, called Default queue.<br><br><br>* The default queue does not occupy your queue quota of the QoS policy.<br><br>* The default queue automatically uses the bandwidth left after other queues are allocated.<br><br>* The default queue contains only one traffic rule, which only allows editing Remark DSCP of the rule. The default queue cannot be deleted. |
|Traffic rule |A traffic rule is an identifier used in the network to recognize and classify data. The QoS policy for a DC Connection allows you to define traffic rules based on the six\-tuple. The six\-tuple consists of:<br><br><br>* Protocol type: The protocol type in the traffic packet.<br><br>* Source port: The source port in the traffic packet.<br><br>* Source CIDR: The CIDR block of a source address in the traffic packet.<br><br>* Destination CIDR: The CIDR block of a destination address in the traffic packet.<br><br>* Destination port: The destination port in the traffic packet.<br><br>* DSCP: Differentiated Services Code Point. |
|DSCP |Differentiated Services Code Point. DSCP occupies the 6 most significant bits of the Type of Service (ToS) field in the IP header to encode packet priority. DSCP uses 6 bits in the IP packet header to represent 64 different values (0\-63), which distinguish different service priorities. |
|Retagged DSCP |Remark DSCP means that packets matching the classification will have their DSCP values reset after the traffic passes through the DC Connection. |


<span id=".5Yqf6IO96K-05piO"></span>
## Capabilities

For the Direct Connect QoS policy feature, create a QoS policy and add traffic queues and rules first. Then, attach the created QoS policy to a Dedicated Line in the same region. Upon successful attachment, the traffic queues within the QoS policy automatically apply to the DC Connection, while the traffic rules apply to the DC Gateway associated through a Virtual Interface using this DC Connection.

When **Outbound** (from a VPC to a data center) traffic enters the DC Gateway with attached traffic rules, the related traffic will be classified according to the configured rules. The classified traffic then enters the DC Connection, and flows to different queues based on the respective matching rules. The traffic will be scheduled based on the queue priority to ensure bandwidth allocation for high\-priority traffic first.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The QoS policy only supports attaching Dedicated Lines, but not Shared Lines, Virtual Interfaces, or DC Gateways.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Since the QoS policy only supports Dedicated Lines, all references to "DC Connection" in next QoS Policy\-related description imply Dedicated Lines unless specified otherwise.   </div>
   

* In the Shared Line scenario, the tenant account can only share a DC Connection and cannot attach a QoS policy. QoS policy can be properly applied to other Dedicated Lines under the account.

* In the Shared Line scenario, for line operator accounts, **QoS policy supports only DSCP marking and the rate limiting of QoS Policy is unavailable**.

* In the Shared Virtual Interface scenario, the DC Connections associated with a Shared Virtual Interface cannot use QoS policies. QoS policy can be properly applied to other DC Connections not associated with Shared Virtual Interfaces under the account.

* Each Dedicated Line supports attaching only **1** QoS policy. Each QoS policy supports creating up to **1** High priority traffic queue (non\-upgradable) and **2** Normal priority traffic queues (upgradable)  **(High)**   **(Normal)** . For more usage limits on DC QoS policy configurations, see [Limits](https://docs.byteplus.com/en/docs/directconnect/Limits).


<span id=".5L2_55So6K-05piO"></span>
## Notes


* The bandwidth allocation sequence for traffic queues within the same QoS policy is: **High queue \> Normal queue \> Default queue**. That is, when cloud service traffic enters a DC Connection via the DC Gateway, bandwidth is allocated to high queues first. The remaining bandwidth is allocated to normal queues then. Finally, default queues automatically use the leftover bandwidth.

* If the bandwidth of the DC Connection is less than the Port Spec, the queue scheduling of QoS policy does not take effect. Only Remark DSCP is available.

* All Virtual Interfaces created using the QoS policy\-attached DC Connection cannot enable bandwidth limit. If any virtual interfaces with bandwidth limit enabled exist, the QoS policy of the DC Connection will become invalid.

* If multiple Virtual Interfaces are created using the same DC Gateway and multiple DC Connections, we recommend attaching the same QoS policy for all DC Connections.

   If only partial DC Connections are attached with the same QoS policy, the DC Connections not attached to that QoS policy will be scheduled based on the default QoS policy. When experiencing a DC Connection bandwidth congestion, additional bandwidth limit may apply. If Remark DSCP is set for the QoS policy attached to partial DC Connections, the DSCP of unattached DC Connections will also be remarked.


<span id=".5LiT57q_6L-e5o6lUW9T562W55Wl5LiO5Lit6L2s6Lev55Sx5ZmoUW9T562W55Wl55qE6IGU5Yqo"></span>
## Interaction between DC QoS policy and TR QoS policy

When traffic from a VPC passes through a Transit Router (TR), the traffic will be marked by the TR. After marking, the traffic enters the DC Gateway on the DC side and is queued for scheduling into an appropriate DC Connection based on the associated matching rules. Then the traffic travels through the DC Connection to an on\-premises data center.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For relatively complex marking scenarios, we recommend you to configure Remark DSCP in the QoS policy on the TR side. Remark DSCP configuration is not required on the DC side.</div>
