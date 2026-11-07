---
title: "VPC NAT Gateway application scenarios"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Scenarios-VPC-NAT"
---

This topic introduces the application scenarios for VPC NAT Gateway.

## Resolve address conflicts

When multiple Virtual Private Clouds (VPCs) need connectivity but their subnet CIDR blocks overlap, connectivity cannot be achieved through Cloud Enterprise Network (CEN) or Transit Router (TR) alone. You can use the VPC NAT Gateway to resolve CIDR block address conflicts.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c54b66dcb38012e2747d2f2310b74564.png)

## Access via designated IP addresses

When a local data center interacts with cloud resources, you can use the VPC NAT Gateway to allow only designated cloud IP addresses to communicate with it. This helps simplify management and enhance security.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b1f12e424aff37279dc63c3027fb9cbc.png)
