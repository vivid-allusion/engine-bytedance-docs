---
title: "Editing the modification protection"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CLB-instances-07"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

To avoid accidental modification or deletion of the Classic Load Balancer (CLB) instance configuration, enable Modification Protection for the instance.

<span id=".5pON5L2c6K-05piO"></span>
## Action description


* Edit modification protection is a hot configuration operation; you do not need to suspend the existing instance service, and changes take effect immediately.

* After enabling modification protection on a CLB instance, only modification protection settings and instance name changes are allowed; all other actions are blocked.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. On the right side of the target CLB instance list, choose ··· \> Edit Modification Protection.

4. In the Modification Protection zone:

   * Enable: Turn on the Modification Protection switch.

   * Disable: Turn off the Modification Protection switch. In the pop\-up confirmation dialog box, click Confirm to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ModifyLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyLoadBalancerAttributes)
