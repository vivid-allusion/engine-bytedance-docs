---
title: "Enabling IPv6 Internet bandwidth"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_internet_bandwidth"
---

IPv6 addresses without enabled IPv6 Internet bandwidth cannot communicate with the Internet. This topic describes how to enable Internet bandwidth for IPv6 addresses, allowing them to communicate with the Internet

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have associated an IPv6 gateway with a Virtual Private Cloud (VPC) to which the IPv6 address belongs. If not, see [Create an IPv6 gateway instance](https://docs.byteplus.com/en/docs/IPv6/Creating_an_IPv6_gateway_instance).

* Cloud resources using IPv6 addresses are in normal status and are attached to [the VPC or subnet with IPv6 enabled](https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_for_private_networks).

* The route table associated with the subnet of the IPv6 address must contain a route entry with the Destination CIDR Block setting as ::/0 and the Next Hop setting as IPv6 gateway. If no such route entry, see [Add route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry).


<span id=".57qm5p2f6ZmQ5Yi2"></span>
## Limits


* Private dual\-stack Application Load Balancer (ALB) instances do not support enabling IPv6 Internet bandwidth, while public dual\-stack ALB instances automatically have IPv6 Internet bandwidth enabled upon creation.

* You can enable up to 20 IPv6 Internet bandwidths in a single region under a single account. To increase the quota, go to [Quota Center](https://console-stable.volcanicengine.com/quota/) to apply.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [IPv6 Gateway console](https://console.byteplus.com/eip/ipv6s).

2. In the top menu bar, select your target region.

3. In the IPv6 Gateway instances list, click the name of target instance to enter the details page.

4. On the IPv6 Internet bandwidth tab, click **Enable Internet bandwidth** to the right of target IPv6 address.

5. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Billing method |Select a billing method for IPv6 Internet bandwidth. Currently, it only supports Pay\-as\-you\-go. |Pay\-as\-you\-go |
   |Metering method |Select a metering method for IPv6 Internet bandwidth, supporting [Pay-by-bandwidth](https://docs.byteplus.com/en/docs/IPv6/Pay-as-you-go#.5oyJ5bim5a695LiK6ZmQ6K6h6LS5) and [Pay-by-data-transfer](https://docs.byteplus.com/en/docs/IPv6/Pay-as-you-go#.5oyJ5a6e6ZmF5rWB6YeP6K6h6LS5). |Pay\-by\-data\-transfer |
   |ISP |Select the ISP for the IPv6 Internet bandwidth. Currently, it supports BGP (multi\-ISP) and static preferential single\-ISP (China Mobile, China Unicom, or China Telecom).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>The static preferential single\-ISP</strong> is in the beta stage. If you need a trial, please contact your account manager.</div><br> |BGP (multi\-ISP) |
   |Bandwidth cap |Set the bandwidth cap for IPv6 internet bandwidth, measured in Mbps. For specific scope, see [Bandwidth limits](https://docs.byteplus.com/en/docs/IPv6/Limits#.5bim5a696ZmQ5Yi2). |1 Mbps |
   |Bandwidth Package |Check to add to [Bandwidth Package](https://docs.byteplus.com/en/docs/bandwidthpackage/What-is-Bandwidth-Package).<br><br><br>* If left unchecked, you can [add the EIP to a Bandwidth Package](https://docs.byteplus.com/en/docs/IPv6/Manage_Shared_Bandwidth_Package#.5Yqg5YWl5YWx5Lqr5bim5a695YyF) as needed in the next step.<br><br>* If checked, select the Bandwidth Package with the same ISP as the IPv6 Internet bandwidth in the current region. After being added to the Bandwidth Package, the IPv6 Internet bandwidth invalidates the metering method and bandwidth cap set as above, and shares the bandwidth of the Bandwidth Package. If you remove the IPv6 Internet bandwidth from the Bandwidth Package, its metering method and bandwidth cap set as above restore valid. |Not selected |
   |Tags |Add one or more custom tags to the IPv6 Internet bandwidth as needed. A tag consists of a tag key\-value object and is used for categorizing and searching resources. For more information, see [Tag management](https://docs.byteplus.com/en/docs/IPv6/Managing_tags).<br><br>Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e69956428611ee87141a75073bce3c8a.png) </span> icon, input tag key and tag value, and add tags to the IPv6 Internet bandwidth instance. |* Tag key: ipv6\-key<br><br>* Tag value: ipv6\-v1 |
   |Agreement |Follow the console guidance to review and accept the legal terms. |\- |
   

6. Click **Apply** to complete the action.

   > Support selecting multiple IPv6 addresses with the network type of **private network** and with the same ISP to enable IPv6 Internet bandwidth in bulk.   
   

<span id=".55u45YWz5paH5qGj"></span>
## What to do next


* [Add to a Bandwidth Package](https://docs.byteplus.com/en/docs/IPv6/Manage_Shared_Bandwidth_Package#.5Yqg5YWl5YWx5Lqr5bim5a695YyF): Add multiple IPv6 Internet bandwidths in the same region to a Bandwidth Package, sharing one Internet bandwidth and reducing costs.

* [Create an Egress Only rule](https://docs.byteplus.com/en/docs/IPv6/Create_only_active_outgoing_rules): After enabling IPv6 Internet bandwidth for the IPv6 address of the Elastic Compute Service (ECS) or secondary network interface, if you do not want the IPv6 address to be accessed by IPv6 terminals on the internet, you can create an Egress Only rule to deny IPv6 terminals on the internet to access the ECS or secondary network interface.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[AllocateIpv6AddressBandwidth](https://docs.byteplus.com/en/docs/IPv6/AllocateIpv6AddressBandwidth): Enable IPv6 Internet bandwidth for the specified IPv6 address.
