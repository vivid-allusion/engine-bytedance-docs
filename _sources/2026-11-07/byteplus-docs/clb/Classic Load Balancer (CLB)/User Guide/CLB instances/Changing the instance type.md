---
title: "Changing the instance type"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CLB-instances-03"
---

Different [CLB instance types](https://docs.byteplus.com/en/docs/clb/Product-Overview-02) correspond to different performance levels (max connections, new connections per second, queries per second, bandwidth), which you can adjust based on your business needs.

This topic explains how to modify a CLB instance type.

Upgrade Specifications: Change to a higher\-performance specification. Use this when the current type's performance does not meet business requirements. Upgrade to enhance performance and satisfy business needs.

Downgrade Specifications: Change to a lower\-performance specification. Use this when the current type's performance greatly exceeds business needs and you want to reduce costs by downgrading. If the downgraded type's performance falls below business requirements, it will impact operations. Evaluate carefully before proceeding.

<span id=".5pON5L2c6K-05piO"></span>
## Action description


* The bandwidth of the changed specification cannot be less than the sum of all dedicated bandwidths of the current instance's listeners.

* Upgrading the specification will not affect business operation but will increase costs; downgrading the instance specification may affect running services. Proceed with caution.

* Changes take effect immediately.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

   * **Pay\-as\-you\-go:** 

      1. Click ··· \> Modify Instance Spec \> Modify instance configuration on the right side of the target CLB instance

      2. Re\-select the specification and click Submit to complete the action.

   * **Subscription:** 

      1. Re\-select the specification and click Confirm.

      2. Complete the operation after finishing the order payment according to the interface prompts.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ModifyLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyLoadBalancerAttributes)
