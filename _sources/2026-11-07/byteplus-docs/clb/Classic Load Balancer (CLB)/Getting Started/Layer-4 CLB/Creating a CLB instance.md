---
title: "Creating a CLB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Layer-4-CLB-02"
---

This topic introduces how to quickly create a public CLB instance.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. Click Create CLB.

3. Configure relevant parameters based on the table below.

   
   |Parameter ||Explanation |Example Value |
   |---|---|---|---|
   |Billing method ||Select a billing method for the CLB instance. The CLB instance supports pay\-as\-you\-go and subscription billing methods. |Pay\-as\-you\-go |
   |Regions ||Select the Region where the CLB instance resides. After you select a region, the created CLB instance can only serve resources within its selected region and cannot be migrated. |China (Beijing) |
   |Availability zone ||Select the master and slave availability zone of the CLB instance respectively. |* Primary: Availability Zone A<br><br>* Secondary: Availability Zone B |
   |Name ||Set the name of the CLB instance. |clb01 |
   |IP version ||Select the IP address type for the CLB instance’s private IP. |IPv4 |
   |Network type ||Select the network type of the CLB instance, which supports both public network and private network. |Public |
   |VPC ||Select the private network where the CLB instance belongs. |VPC01 |
   |Subnet ||Select the subnet to which the CLB instance belongs. |subnet01 \| 192.168.3.0/24 |
   |IPv4 address ||Select the allocation method for the CLB instance IPv4 address. |Automatic IP assignment |
   |Elastic IP Address |Security protection |Select the protection type for the EIP. |default |
   ||ISP |Select an ISP for the Elastic IP. Different types of ISPs vary in performance and billing standards. Only BGP (multi\-line) is supported by default. |BGP (multi\-line) |
   ||Metering method |Select the metering method for the EIP. Currently supports two billing methods: pay\-by\-bandwidth and billing by actual traffic. |Pay\-by\-bandwidth\-cap |
   ||Bandwidth cap |Maximum bandwidth of the EIP. Unit: Mbps. After creating a CLB instance, you can adjust the EIP bandwidth cap anytime as needed. |20Mbps |
   ||Bandwidth Package |Whether to join the share bandwidth package. |No |
   |Specification ||Different specifications correspond to different max connections, new connections per second, queries per second, and bandwidth. Select the appropriate specification based on your performance needs for different business scenarios. For specification details, refer to [Product specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02). |Small I |
   

4. Follow the console guidance to review and accept Legal.

5. Click **Submit order** to complete the action.
