---
title: "Enabling/Disabling modification protection"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Enabling-Disabling-modification-protection"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

The modification protection feature can prevent Network Load Balancer (NLB) instances and their associated resources from accidental actions. You can enable modification protection for NLB instances as needed.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Disabling modification protection may cause accidental modifications or deletions of NLB instances. Please proceed with caution.</div>


<span id=".5pON5L2c6K-05piO"></span>
## Action description


* After successfully creating the NLB instance, modification protection is disabled by default.

* Once modification protection is enabled for the NLB instance, only disabling modification protection is supported, and other actions are not allowed.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the target NLB instance name to enable or disable modification protection as needed.

   * Enable modification protection: In the instance attribute area, turn on the switch for the modification protection feature.

   * Disable modification protection: In the instance attribute area, turn off the switch for the modification protection feature, and then click Confirm to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ModifyNetworkLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerAttributes)
