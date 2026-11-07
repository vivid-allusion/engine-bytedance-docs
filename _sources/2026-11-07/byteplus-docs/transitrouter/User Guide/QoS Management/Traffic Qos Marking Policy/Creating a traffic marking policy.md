---
title: "Creating a traffic marking policy"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Creating-a-qos-marking-policy"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

The traffic marking policy classifies outbound traffic from the TR attachment for easier distinction of different services.

<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* You can create up to 10 traffic marking policies for a single Transit Router (TR) instance by default.

* A traffic marking policy comprises at least one marking entry and, by default, supports a maximum of 100 entries.​ If the default quota is insufficient, [create a quota application](https://docs.byteplus.com/en/docs/6837/129542) to request a quota increase.

* You can add up to 10 marking entries when creating a new traffic marking policy.

* Currently, only inter\-region attachments support traffic marking policies.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. Select the **Basic information** tab, then choose the **Traffic marking policy** tab below.

4. Click **Create traffic marking policy** and configure the traffic marking policy as shown in the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Name |Enter the name of the traffic marking policy. |markpolicy01 |
   |**Traffic marking entries** |||
   |Name |Enter the name of the marking rule. |Video service traffic |
   |Priority |Enter the priority of the marking entry. Value range: 1–10000. Lower numbers indicate higher priority. |1 |
   |Protocol type |Select protocol type. Supports ICMP, ICMPv6, TCP, UDP, and GRE protocols. You can also select **ALL** to indicate any protocol.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Transit Router IPv6 feature is in beta. To select ICMPv6, first enable the Transit Router IPv6 feature.</div><br> |TCP |
   |Source CIDR |The CIDR block to which the source address of the traffic packet belongs.<br><br>If this field is not set, the system defaults it to `0.0.0.0/0` or `::/0`. That is, it matches any source IP addresses. When the protocol type is ICMPV6, it defaults to ::/0. For other protocols, it defaults to 0.0.0.0/0. |192.168.1.0/24 |
   |Source port range |Source port of the traffic packet. Supports input of a single port (e.g., 80) or a port range (e.g., 20\-23). Port range: 1\-65535.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The source port does not need to be configured when the protocol type is ICMP, ICMPv6, or GRE.</div><br> |80 |
   |Destination CIDR |The CIDR block to which the destination address of the traffic packet belongs.<br><br>If this field is not set, the system defaults it to `0.0.0.0/0` or `::/0`. That is, it matches any source IP addresses. When the protocol type is ICMPV6, it defaults to ::/0. For other protocols, it defaults to 0.0.0.0/0.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The IP type of the destination CIDR block and the source CIDR block must be consistent. For example, both should be IPv4 CIDR blocks, or both should be IPv6 CIDR blocks.</div><br> |172.16.1.0/24 |
   |Destination port range |Destination port for traffic packets. Supports single port input (e.g., 80) or port range (e.g., 20\-23). Port range: 1\-65535.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">No destination port configuration required when the protocol type is ICMP, ICMPV6, GRE, or ALL.</div><br> |80 |
   |DSCP |The original DSCP value carried by traffic before entering the Transit Router (TR) connection. Value range: 0\-63.<br><br>This marking entry matches traffic carrying the specified DSCP value. If not specified, it matches traffic with any DSCP value by default. |2 |
   |Retagged DSCP |The new DSCP value set for matching traffic to classify and mark traffic entering the TR connection. Value range: 0\-63.<br><br>Retagged DSCPs for different marking entries can be the same. |10 |
   

5. Click **OK** to complete the action.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

After creating the traffic marking policy, apply it to an inter\-region attachment to enable traffic classification marking. For details, see [Enable traffic marking policy](https://docs.byteplus.com/en/docs/transitrouter/Configuring-a-qos-marking-policy-for-inter-region-attachment#.5ZCv55So5rWB5qCH6K6w).

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[CreateTransitRouterTrafficQosMarkingPolicy](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterTrafficQosMarkingPolicy): Create a traffic marking policy.
