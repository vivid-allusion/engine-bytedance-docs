---
title: "Adding to/Removing from a bandwidth package"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Adding-or-removing-an-EIP-to-or-from-the-Bandwidth-Package"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

By adding the Elastic IP (EIP) and IPv6 internet bandwidth associated with the Network Load Balancer (NLB) instance to a Bandwidth Package, internet bandwidth sharing can be achieved, which saves internet costs.

<span id=".5pON5L2c5q2l6aqk"></span>
## Add to Bandwidth Package

After the EIP or IPv6 Internet bandwidth is associated with a Bandwidth Package, they will share the bandwidth of the  Bandwidth Package. During peak business periods, multiple EIP or IPv6 Internet bandwidths might compete for bandwidth. Therefore, before adding the EIP or IPv6 Internet bandwidth of the NLB instance to a Bandwidth Package, please first [view CloudMonitor](https://docs.byteplus.com/en/docs/bandwidthpackage/Viewing-monitoring-data) to carefully assess the usage of the Bandwidth Package. Adjust the bandwidth of the Bandwidth Package as needed before adding to avoid business impacts from bandwidth competition.

<span id=".5Yqg5YWl5YWx5Lqr5bim5a695YyF"></span>
### Prerequisites


* To add the EIP of an NLB instance into a Bandwidth Package, the following conditions must be met simultaneously:

   * The billing method of the EIP is Pay\-as\-you\-go.

   * Both are in the same region.

   * Both have the same protection type.

   * Both have the same ISP.

   * Internet egress for both is the same.

* To add the IPv6 Internet bandwidth of the NLB instance to the Bandwidth Package, the following conditions must be met simultaneously:

   * The bandwidth package protocol is dual\-stack (IPv4 & IPv6).

   * Both are in the same region.

   * Both have the same ISP.

   * Internet egress for both is the same.


<span id="0rhZMHos"></span>
### Procedures


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click ··· \> Join the IPv4/IPv6 Shared Bandwidth Package on the right side of the target NLB instance, then select the Bandwidth Package.

4. Click **OK** to complete the action.


<span id=".56e75Ye65YWx5Lqr5bim5a695YyF"></span>
## Removed from Bandwidth Package

<span id="PPnPUm8Q"></span>
### Action description

After an EIP or IPv6 Internet bandwidth is removed from the Bandwidth Package, it will no longer use the bandwidth of the Bandwidth Package and will revert to its own maximum bandwidth. Therefore, before removing an EIP or IPv6 Internet bandwidth from the Bandwidth Package, check the details page of an[ EIP](https://console.byteplus.com/eip/eips) or [IPv6 Internet bandwidth](https://console.byteplus.com/eip/ipv6s) to verify whether its bandwidth meets the operational requirements of the current NLB instance. If not, adjust the bandwidth before removal to avoid business disruptions caused by insufficient bandwidth.

<span id="2PjnO9Rh"></span>
### Procedures


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click ··· \> Remove IPv4/IPv6 Shared Bandwidth Package on the right side of the target NLB instance.

4. Click **OK** to complete the action.


<span id=".5pON5L2c57uT5p6c"></span>
### Results


* The maximum bandwidth of the EIP or IPv6 Internet bandwidth is restored.

* The billing items (bandwidth fee and data transfer fee) for the EIP or IPv6 Internet bandwidth are restored, with billing starts immediately.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ModifyNetworkLoadBalancerBandwidthPackage](https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerBandwidthPackage)
