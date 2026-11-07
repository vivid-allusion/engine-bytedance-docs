---
title: "Creating a QoS Policy"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Creating_a_QoS_Policy"
---

This topic introduces how to create a QoS policy and add traffic queues.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Direct Connect console](https://console.byteplus.com/dc/PhysicalConnection). In the left navigation pane, select **QoS Policy**.

2. Select region information in the top navigation bar and click **Create QoS Policy**.

3. Configure the QoS policy information according to the table below.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Each QoS policy must contain at least one flow queue. Each flow queue must contain at least one traffic rule.   </div>
   

   * **Basic information**

      
      |Parameter |Description |Example |
      |---|---|---|
      |Regions |Select the region where the QoS policy is located. QoS policy can only attach to dedicated DC Connection within the same Region. |China (Beijing) |
      |Name |Enter the name of the QoS policy. |QoS_policy01 |
      

   * **Traffic queue**

      
      |Parameter |Description |Example |
      |---|---|---|
      |Name |Enter the name of the current traffic queue. |Queue_01 |
      |Priority |Select the priority for the current traffic queue.<br><br><br>* **High queue**: A traffic queue with high priority. High\-priority queues receive bandwidth allocation first. Each QoS policy can only have one high\-priority flow queue.<br><br>* **Normal queue**: A traffic queue with normal priority. Normal\-priority queues share the remaining bandwidth (after high\-priority allocation) based on their configured bandwidth percentage limits. |Normal |
      |Bandwidth rate limiting |This parameter only needs to be configured when the priority is set to "Normal". Set the bandwidth limit percentage for the current traffic queue.<br><br><br>* Value range: An integer between 1 and 99.<br><br>* The rate limiting bandwidth of all normal traffic queues under the same QoS policy cannot exceed 99%. |20 |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Click <strong>+Add traffic queue</strong> to create multiple traffic queues simultaneously. You can create up to 3 traffic queues simultaneously.      </div>
      

   * **Traffic rule**

      
      |Parameter |Description |Example |
      |---|---|---|
      |Name |Enter the name of the current traffic rule. |Video service traffic |
      |Priority |Enter the priority of the current traffic rule.<br><br><br>* Value range: 1\-10000. A smaller number indicates higher priority.<br><br>* The priority values for traffic rules within the same QoS policy must be unique. |1 |
      |Protocol type |Select the protocol type for the current traffic rule. Supports ICMP, ICMPv6, TCP, UDP, GRE protocols. You can also select "ALL" to indicate any protocol.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Direct Connect IPv6 feature is in beta stage. The ICMPv6 protocol type will only be visible after the IPv6 function is enabled. If needed, please contact your account manager.</div><br> |TCP |
      |Source CIDR |The CIDR block to which the source address of the traffic packet belongs.<br><br><br>* If this field is not set, the system defaults it to `0.0.0.0/0` or `::/0`. That is, it matches any source IP addresses.<br><br>* When the protocol type is **ICMPV6**, it defaults to `::/0`. For other protocols, it defaults to `0.0.0.0/0`. |192.168.1.0/24 |
      |Source port |The source port of the traffic packet. Only a single port (e.g., 80) is supported. Port range: 1\-65535.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The source port does not need to be configured when the protocol type is ICMP, ICMPv6, or GRE.</div><br> |80 |
      |Destination CIDR |The CIDR block to which the destination address of the traffic packet belongs.<br><br><br>* If this field is not set, the system defaults it to `0.0.0.0/0` or `::/0`. That is, it matches any source IP addresses.<br><br>* When the protocol type is **ICMPV6**, it defaults to `::/0`. For other protocols, it defaults to `0.0.0.0/0`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The IP type of the destination CIDR block and the source CIDR block must be consistent. For example, both should be IPv4 CIDR blocks, or both should be IPv6 CIDR blocks.</div><br> |172.16.1.0/24 |
      |Destination port |The destination port of the traffic packet. Only a single port (e.g., 80) is supported. Port range: 1\-65535.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The source port does not need to be configured when the protocol type is ICMP, ICMPv6, or GRE.</div><br> |80 |
      |DSCP |The original DSCP value carried by traffic entering the DC gateway before. Value range: 0\-63.<br><br>The current traffic classification rule matches traffic carrying a specific DSCP value. If this value is not specified, it defaults to matching traffic carrying any DSCP value. |2 |
      |Retagged DSCP |The new DSCP value set for the traffic that matches the traffic rule is used to classify and mark the traffic entering DC gateway. Value range: 0\-63.<br><br><br>* The remarking DSCP values of different traffic rules can be the same.<br><br>* If the incoming service traffic originates from a Transit Router (TR) and a QoS policy is already configured on the TR side, it is recommended not to configure DSCP remarking in the Direct Connect QoS policy. If DSCP remarking is configured on both the TR side and the Direct Connect side, the Direct Connect side will ignore the original DSCP value (before TR remarking). It will only re\-mark the DSCP value that was already remarked by the TR, and forward the traffic to the on\-premises IDC based on this final remarked DSCP value. |10 |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Click <strong>+Add traffic marking entry</strong> below the queue to create multiple traffic rules simultaneously. You can add up to 5 traffic rules simultaneously.      </div>
      

4. After configuration, click **Accept**.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

After the QoS policy is created, you need to [Attach DC Connection](https://docs.byteplus.com/en/docs/directconnect/Attaching_and_detaching_DC_Connection) to QoS policy. The traffic of the DC Connection associated with the QoS policy will be allocated and scheduled according to the flow queue priority and flow classification rules in the QoS policy.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">A Virtual Interface created using a DC Connection associated with a QoS policy does not support enabling the bandwidth limit. If a Virtual Interface has bandwidth limit enabled, the QoS policy will become ineffective.</div>


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [CreateDirectConnectTrafficQosPolicy](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectTrafficQosPolicy): Create a QoS policy.

* [CreateDirectConnectTrafficQosQueue](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectTrafficQosQueue): Add a traffic queue to a QoS policy.

* [CreateDirectConnectTrafficQosRule](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectTrafficQosRule): Add a traffic rule to a traffic queue.
