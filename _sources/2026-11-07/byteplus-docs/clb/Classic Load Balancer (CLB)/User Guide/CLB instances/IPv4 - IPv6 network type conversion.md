---
title: "IPv4/IPv6 network type conversion"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Changing-the-IP-address-version"
---

CLB supports switching between single\-stack IPv4 and dual\-stack IPv4&IPv6 freely, allowing you to adjust based on business needs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Dual\-stack IPv4&IPv6 is in beta. To apply for a trial, contact customer service support.</div>


<span id=".6L2s5Li65Y-M5qCISVB2NCZJUHY2"></span>
## Convert to dual\-stack IPv4&IPv6

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* The VPC and subnet where CLB resides have enabled IPv6. If not enabled, please see Enabling IPv6 feature for VPC and Enabling IPv6 feature for subnet.

* CLB is a private type. If CLB is public type, please refer to Converting public instance to private instance.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click ··· \> Manage instance configuration \> Convert to dualstack instance on the right side of the target CLB instance.

4. Select the allocation method for the CLB instance IPv6 address.

   * **Auto\-assign IP**: Automatically allocate an available IPv6 address from the subnet CIDR block where the CLB is located.

   * **Manual assignment**: Enter the last 16 digits of the IPv6 address in hexadecimal.

5. Click Save to complete the conversion.


After allocating an IPv6 address to the CLB, enable IPv6 internet bandwidth to communicate with the IPv6 internet if needed. For details, please see Activating IPv6 Internet bandwidth.

<span id=".6L2s5Li65Y2V5qCISVB2NA=="></span>
## Switch to single\-stack IPv4

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* The CLB's IPv6 address does not have IPv6 Internet bandwidth enabled. If activated, please see Deleting an IPv6 Internet bandwidth.

* The CLB does not have an IPv6 backend server group. If it exists, see [Deleting the backend server group](https://docs.byteplus.com/en/docs/clb/Deleting-the-server-group).


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click ··· \> Manage instance configuration \> Convert to IPv4 instance on the right side of the target CLB instance.

4. Click Save to complete the conversion.


After converting to single\-stack IPv4, the original IPv6 address is released, and the IPv6 address entries in listener\-related access control become invalid.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ModifyLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyLoadBalancerAttributes)
