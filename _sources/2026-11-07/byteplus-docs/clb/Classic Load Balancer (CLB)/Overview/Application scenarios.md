---
title: "Application scenarios"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Product-Overview-05"
---

Classic Load Balancer (CLB) services are mainly applicable to traffic distribution, guarantee of high service reliability, and disaster recovery across Availability Zone scenarios.

<span id=".5Lia5Yqh5rWB6YeP5YiG5Y-R"></span>
## Traffic distribution

For businesses with high access volume, the CLB scheduling algorithm can be configured to distribute traffic to different backend servers, preventing a single backend server from being overloaded and causing delays in business response.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_56a60aef6aee44246482b0a3b8446817.png) </span>

<span id=".5pyN5Yqh6auY5Y-v6Z2g5L-d6Zqc"></span>
## Guarantee of high service reliability

When some servers in the Server Group are unavailable, CLB can automatically shield the failed backend servers to avoid the impact of single\-point failures and ensure the normal operation of application systems.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fc85ff0af0f9a91245d57f495e8cc156.png) </span>

<span id=".6Leo5Y-v55So5Yy65a6554G-"></span>
## Cross\-AZ Disaster Recovery

Regions with deployed primary and backup Availability Zones support CLB’s disaster recovery across Availability Zone. Under normal circumstances, the CLB deployed in the primary Availability Zone forwards access traffic to the corresponding backend servers, while the CLB deployed in the backup Availability Zone does not carry traffic. When the primary Availability Zone fails, the access traffic will be forwarded by the CLB deployed in the backup Availability Zone to the corresponding backend servers, thereby ensuring the normal operation of the business.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_078184d37a9080cd220ec8011cf16e95.png) </span>

&nbsp;
