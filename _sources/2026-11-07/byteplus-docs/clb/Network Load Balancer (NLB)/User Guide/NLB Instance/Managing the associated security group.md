---
title: "Managing the associated security group"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Managing-attached-security-groups"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

After successfully creating a Network Load Balancer (NLB) instance, you can modify its attached security group as needed and control the outbound and inbound traffic of the NLB instance through security group rules.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The security group to be attached must allow client access traffic and traffic for system probes checking availability of NLB's private IP address, otherwise, the network connectivity will be blocked. For detailed configuration steps, please see Configuring an instance security group.</div>


<span id=".5pON5L2c6K-05piO"></span>
## Action description


* Each NLB instance can attach up to 5 security groups, including the system\-default entrusted security group.

* Entrusted security groups are automatically associated by the system, and do not support disassociating and modifying security group rules.

* Modifying associated security groups or adding/deleting/editing security group rules may impact the outbound and inbound traffic of the NLB. Please proceed with caution.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures

<span id=".5pu05pS55YWz6IGU5a6J5YWo57uE"></span>
### Change attached security groups


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the target NLB instance name and choose the security group tab.

4. Click Change on the right side of the attached security group to reselect the security group to attach.

5. Click **Confirm** to complete the action.


<span id=".566h55CG5a6J5YWo57uE6KeE5YiZ"></span>
### Manage security group rule


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the target NLB instance name and choose the security group tab.

4. Click Edit rule on the right side of the target security group to add, modify, or delete security group rules as needed.

   For detailed introduction of related parameters, please see Adding a security group rule.

5. Click Confirm or Delete to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ModifyNetworkLoadBalancerSecurityGroups](https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerSecurityGroups)
