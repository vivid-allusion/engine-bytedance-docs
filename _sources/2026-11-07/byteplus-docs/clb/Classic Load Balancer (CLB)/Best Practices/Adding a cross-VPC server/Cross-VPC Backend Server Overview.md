---
title: "Cross-VPC Backend Server Overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Cross-VPC-server-overview"
---

This topic explains how Classic Load Balancer (CLB) integrates with other network products to use ECSs or servers within an IDC across VPCs as backend servers for CLB.

<span id=".5qaC6L-w"></span>
## Overview

CLB supports cross\-VPC backend service capabilities, allowing you to add service resources from other VPCs in the cloud or servers from IDCs on\-premises as backend servers.

The cross\-VPC backend service capability helps you flexibly configure backend servers based on business needs and forward access traffic to servers both in the cloud and on\-premises through CLB.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The CLB's cross\-VPC backend feature is in Beta stage. If you need a trial, please contact your account manager.</div>


<span id=".6KeE5YiS5YeG5aSH"></span>
## Preparation

If you want to use CLB's cross\-VPC backend service capability, complete the following preparations first:


* The cross\-VPC backend feature is currently in Beta. You need to contact your customer service support to apply for trial permission.

* Plan your specific solution for using the cross\-VPC backend feature in advance. You can see [networking scenario](https://docs.byteplus.com/en/docs/clb/Cross-VPC-server-overview#.57uE572R5Zy65pmv).


<span id=".57uE572R5Zy65pmv"></span>
## Networking scenario

CLB adds cross\-VPC backend servers. The specific networking scenarios are shown in the following table.


|Cross\-VPC Backend Type |Scenario overview |Documentation |
|---|---|---|
|Cloud resource IP address |Add IP addresses of ECS instances in other VPCs on the cloud as backend servers |[Implement with Transit Router (TR) service](https://docs.byteplus.com/en/docs/clb/Combining-with-the-TR-service-to-use-an-ECS-instance-in-a-VPC-as-the-cross-VPC-server) |
|IP addresses inside the on\-premises IDC |Add IP addresses of servers in on\-premises IDC as backend servers |* [Implement with Transit Router (TR) service](https://docs.byteplus.com/en/docs/clb/Combining-with-the-TR-service-to-use-a-server-in-a-data-center-as-the-cross-VPC-server)<br><br>* [Implement with Cloud Enterprise Network (CEN) service](https://docs.byteplus.com/en/docs/clb/Achieve-the-server-of-the-data-center-as-the-backend-server-of-CLB-Instance-through-CEN) |


<span id=".6LSf6L295Z2H6KGh5Zue5rqQ5Zyw5Z2A"></span>
## CLB back\-to\-source address

When configuring the cross\-VPC backend feature, you need to set up CLB's back\-to\-source routing so the data returned by backend servers can be sent back to the client through CLB. The back\-to\-source addresses for each region are shown in the table below.


|Regions |CLB (Layer 4 Listener) ||CLB (Layer 7 Listener) |
|---|---|---|---|
||IPv4 |IPv6 |IPv4 |
|China (Guangzhou) |100.127.232.0/22 |fd00:64:0:1004::/64 |100.127.236.0/23 |
|China (Shanghai) |100.127.224.0/22<br><br>100.127.96.0/19 |fd00:64:0:1007::/64 |100.127.228.0/23 |
|China (Beijing） |100.127.216.0/22<br><br>100.127.64.0/19 |fd00:64:0:100a::/64 |100.127.220.0/23 |
|Asia Pacific (Johor) |100.127.204.0/23<br><br>100.127.128.0/20 |fd00:64:0:100d::/64 |100.127.206.0/24 |
