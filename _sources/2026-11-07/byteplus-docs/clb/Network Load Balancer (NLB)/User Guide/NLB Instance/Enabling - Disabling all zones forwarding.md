---
title: "Enabling/Disabling all zones forwarding"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Enabling-Disabling-all-zones-forwarding"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

When creating an Network Load Balancer (NLB) instance, you do not need to specify all zones forwarding. After the instance is created, the all zones forwarding feature is enabled by default, and you can modify it as needed.

<span id=".5pON5L2c6K-05piO"></span>
## Action description

After disabling all zones forwarding, the NLB instance can only forward access requests to backend servers within the same Availability Zone. For example, access requests from Availability Zone A can only be forwarded to backend servers in Availability Zone A for processing. For detailed information about all zones forwarding, see all zones forwarding.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the target NLB instance name.

4. In the instance attribute zone, enable/disable the all zones forwarding feature.

5. Click **OK** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ModifyNetworkLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerAttributes)
