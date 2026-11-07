---
title: "Modifying a forwarding rule"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Modifying-the-forwarding-rule"
---

<span id=".5pON5L2c6K-05piO"></span>
## Action description


* The domain name and URL of the forwarding rule cannot be modified.

* Default forwarding rules only support modifying backend server groups.

* Forwarding rules do not currently support attaching backend server groups of the IPv6 type.

* Modifying forwarding rules may affect running services. Proceed with caution.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click Edit Listener to the right of the target CLB instance.

4. Click Configure forwarding rule to the right of the target Layer 7 listener.

5. Click **Edit** to the right of the target forwarding rule to modify parameters related to forwarding actions. For parameter details, see [Adding a forwarding rule](https://docs.byteplus.com/en/docs/clb/Adding-a-forwarding-rule).

6. Click **OK** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ModifyRules](https://docs.byteplus.com/en/docs/clb/ModifyRules)
