---
title: "Managing an IPv6 internet bandwidth"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Activating-or-Deleting-IPv6-Internet-bandwidth"
---

This topic explains how dual\-stack CLB instances manage IPv6 Internet bandwidth to flexibly switch their availability in the IPv6 Internet environment. Once enabled, the CLB instance can provide services to the Internet.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The dual\-stack CLB feature is in beta. Contact customer service support to request a trial.</div>


<span id=".5byA6YCaSVB2NuWFrOe9keW4puWuvQ=="></span>
## Enable IPv6 Internet bandwidth

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

Ensure you have applied for trial permission for the IPv6 gateway product. If not applied, contact customer service support.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click ··· \> Public \> Enable public IPv6 bandwidth on the right of the target CLB instance.

4. Configure relevant parameters based on the table below.

   
   |Parameter name |Description |Example |
   |---|---|---|
   |Billing method |Currently only support Pay\-as\-you\-go. |Pay\-as\-you\-go |
   |Metering method |Select the metering method for IPv6 Internet bandwidth.<br><br><br>* [Pay-by-data-transfer](https://docs.byteplus.com/en/docs/IPv6/Pay-as-you-go#.5oyJ5a6e6ZmF5rWB6YeP6K6h6LS5): after specifying the bandwidth cap, fees are based on the actual outbound Internet traffic used, regardless of usage duration.<br><br>* [Pay-by-bandwidth](https://docs.byteplus.com/en/docs/IPv6/Pay-as-you-go#.5oyJ5bim5a695LiK6ZmQ6K6h6LS5): after specifying the bandwidth cap, fees are based on usage duration, regardless of actual traffic. |Pay\-by\-data\-transfer |
   |ISP |Only supports BGP (multi\-ISP). |BGP (multi\-ISP) |
   |Bandwidth cap |Set the bandwidth cap for IPv6 internet bandwidth, measured in Mbps. For specific scope, see [Bandwidth limits](https://docs.byteplus.com/en/docs/IPv6/Limits#.5bim5a696ZmQ5Yi2). |10Mbps |
   |Bandwidth Package |Select to join the [bandwidth package](https://docs.byteplus.com/en/docs/bandwidthpackage/What-is-Bandwidth-Package) as needed.<br><br><br>* If left unchecked, you can [add the EIP to a Bandwidth Package](https://docs.byteplus.com/en/docs/eip/Adding-an-EIP-to-a-Bandwidth-Package) as needed in the next step.<br><br>* If selected, you can choose an IPv6 shared bandwidth package in the current region.<br><br>   After selecting a shared bandwidth package, the billing items traffic fee or bandwidth fee and bandwidth cap of the above billing method become invalid, and the IPv6 Internet bandwidth shares the bandwidth of the bandwidth package. If you remove the EIP from the Bandwidth Package, EIP's original billing method and maximum bandwidth restore valid. |No |
   |Agreement |Follow the console guidance to review and accept Legal. |Check |
   

5. Click **Apply** to complete the action.


<span id=".5Y-Y5pu0SVB2NuWFrOe9keW4puWuvemFjee9rg=="></span>
## Modify IPv6 Internet bandwidth configuration

<span id=".5pON5L2c6K-05piO"></span>
### Action description


* Reducing the EIP bandwidth cap may affect running services. Proceed with caution.

* Instances added to the Bandwidth Package can modify IPv6 Internet bandwidth configuration, but the changes only take effect after removal from the Bandwidth Package.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click ··· \> Public \> Modify IPv6 Internet bandwidth configuration on the right side of the target CLB instance.

4. Modify the IPv6 Internet billing method or set a new EIP bandwidth cap as needed. Billing will follow the new method or cap after modification. See [IPv6 gateway billing conversion](https://docs.byteplus.com/en/docs/IPv6/Billing_methods_change) for detailed constraints on billing method changes.

5. Click Confirm order.

6. Follow the console guidance to review and accept Legal.

7. Click **Submit** to complete the action.


<span id=".5Yig6ZmkSVB2NuWFrOe9keW4puWuvQ=="></span>
## Disable IPv6 Internet bandwidth

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

The IPv6 Internet bandwidth is not added to any Bandwidth Package. If added, [remove it from the Bandwidth Package](https://docs.byteplus.com/en/docs/clb/CLB-instances-08#.56e75Ye65YWx5Lqr5bim5a695YyF).

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click ··· \> Public \> Delete public IPv6 bandwidth on the right side of the target CLB instance.

4. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [AllocateIpv6AddressBandwidth](https://docs.byteplus.com/en/docs/IPv6/AllocateIpv6AddressBandwidth)

* [ModifyIpv6AddressBandwidth](https://docs.byteplus.com/en/docs/IPv6/ModifyIpv6AddressBandwidth)

* [ReleaseIpv6AddressBandwidth](https://docs.byteplus.com/en/docs/IPv6/ReleaseIpv6AddressBandwidth)


&nbsp;

&nbsp;
