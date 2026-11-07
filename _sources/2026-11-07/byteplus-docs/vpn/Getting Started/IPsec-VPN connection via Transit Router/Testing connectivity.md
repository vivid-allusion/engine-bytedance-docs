---
title: "Testing connectivity"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Test_connectivity"
---

This topic describes how to verify VPN connectivity after you complete all configurations.

<span id="VJp0w6Za"></span>
## Procedure


1. Log in to any Elastic Compute Service (ECS) within a subnet (named subnet1) of your Virtual Private Cloud (named VPC1). For procedure, see Logging on to a Linux instance.

2. In the ECS, execute the `ping` command to the IP address of any server in your on\-premises data center. The IP address is covered by the IPsec CIDR block.

3. A successful ping indicates that the VPN connection is established and in normal communication.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_890ffc3801ce5f6be8ee3341fd9e2f47.png) </span>
