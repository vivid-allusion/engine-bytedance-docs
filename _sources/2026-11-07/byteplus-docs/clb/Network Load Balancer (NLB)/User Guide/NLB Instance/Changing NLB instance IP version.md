---
title: "Changing NLB instance IP version"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Changing-NLB-instance-IP-version"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

NLB supports two types of IP versions: IPv4 and dual\-stack. You can flexibly modify the IP version type based on your business requirements.

<span id=".5pON5L2c6K-05piO"></span>
## Action description


|Change Actions |Prerequisites |Explanation After Change |
|---|---|---|
|Convert IPv4 to dual\-stack instance |* Ensure that you have enabled permission for the IPv6 feature of the NLB. If not enabled, contact your account manager.<br><br>* Ensure the subnet intended for assigning IPv6 addresses to the NLB instance already has an IPv6 CIDR block. If not available, refer to Enabling IPv6 for a Subnet. |* The system automatically allocates IPv6 addresses for each Availability Zone of the NLB and adds domain name resolution to the IPv6 addresses, while the IPv4 addresses remain unchanged.<br><br>* To enable IPv6 access to the internet for this instance, first modify the instance to a dual\-stack type, then follow the steps of Changing the IPv6 network type to internet. |
|Convert dual\-stack to IPv4 instance |Ensure that the IPv6 network type of the NLB instance is private network. If it is internet, first refer to Modify IPv6 network type to private network and then change to IPv4 instance. |The system automatically deletes all IPv6 addresses from the NLB instance and removes the domain name resolution entries of the IPv6 addresses, while the IPv4 addresses remain unchanged. |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click Convert on the right side of the target NLB instance.

   * IPv4 to dual\-stack: Click the Convert IP version to dual\-stack button.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If there is no IPv6 CIDR within the subnet, refer to Enabling IPv6 for a subnet.      </div>
      

   * Dual\-stack to IPv4: Click Convert IP version to IPv4 button.

4. Click **Migrate** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ModifyNetworkLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerAttributes)
