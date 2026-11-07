---
title: "Public CLB to private CLB"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CLB-instances-04"
---

After converting a public CLB instance to a private CLB instance, the lifecycle of the private instance and the associated EIP are independent of each other. When deleting the private CLB instance, the EIP can still be attached to other resources for continued use.

This topic introduces how to convert a public CLB instance to a private CLB instance.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click ··· \> Modify Instance Spec \> Convert to private type on the right side of the target CLB instances list.

4. Click **Apply** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ModifyLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyLoadBalancerAttributes)
