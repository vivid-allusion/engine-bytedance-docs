---
title: "API release notes"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/API_release_notes"
---

This document introduces the API updates for the IPv6 gateway.

<span id="march-2025"></span>
## March 2025


|API |change record |associated function |
|---|---|---|
|* DescribeIpv6Gateways<br><br>* DescribeIpv6GatewayAttribute |Added return parameter: `RouteTableId`. |Query an IPv6 gateway instance |
|AllocateIpv6AddressBandwidth |* Modify the properties of the request parameter `IPv6Address` to an optional parameter.<br><br>* Added request parameter `AllocationIds. N`.<br><br>* Added return parameter `AllocationIds. N`.<br><br>* Added error code `InvalidEip. IPv6ISPMisMatch`. |Open IPv6 public network bandwidth |
|* DescribeIpv6AddressBandwidths<br><br>* DescribeIpv6AddressBandwidthAttributes |Added return parameter `IsBlocked`. |Query IPv6 public network bandwidth |
|ReleaseIpv6AddressBandwidth |* Modify the properties of the request parameter `IPv6Address` to an optional parameter.<br><br>* Added request parameter `AllocationIds. N`. |Free up IPv6 public network bandwidth |


<span id="january-2025"></span>
## January 2025


|API |Change History |Associated Features |
|---|---|---|
|All APIs |The APIs of IPv6 Gateway are released for the first time. |\- |
