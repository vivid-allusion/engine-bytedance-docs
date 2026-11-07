---
title: "Creating a CLB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Layer-7-CLB-02"
---

This topic describes how to quickly configure a Layer\-7 public CLB instance.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The table below only covers the parameters required for this configuration; other parameters should remain at their default values. If you need to learn more about the parameters, see User Guide \> Create a CLB Instance.</div>



1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. Click Create CLB.

3. Configure relevant parameters based on the table below.

   
   |Parameter ||Explanation |Example Value |
   |---|---|---|---|
   |Billing method ||Select a billing method for the CLB instance. The CLB instance supports pay\-as\-you\-go and subscription billing methods. |Pay\-as\-you\-go |
   |Regions ||Select the Region where the CLB instance resides. After you select a region, the created CLB instance can only serve resources within its selected region and cannot be migrated. |China (Beijing) |
   |Availability zone ||Select the master and slave availability zone of the CLB instance respectively. |* Primary: Availability Zone A<br><br>* Secondary: Availability Zone B |
   |Name ||Set the name of the CLB instance. |clb01 |
   |IP version ||Select the private IP address type for the CLB instance. |IPv4 |
   |Network type ||Select the network type of the CLB instance, which supports both public network and private network. |Public |
   |VPC ||Select the private network where the CLB instance belongs. |VPC01 |
   |Subnet ||Select the subnet to which the CLB instance belongs. |subnet01 \| 192.168.3.0/24 |
   |IPv4 address ||Select the allocation method for the CLB instance's IPv4 address. |Automatic IP assignment |
   |Elastic IP Address |Security protection |Select the protection type for the EIP. |default |
   ||ISP |Select the ISP type for the public IP. Different types vary in performance and billing standards. The default only supports BGP (multi\-line). |BGP (multi\-line) |
   ||Metering method |Select the metering method for the EIP. Pay\-by\-bandwidth and Pay\-by\-data\-transfer are supported. |Pay\-by\-bandwidth\-cap |
   ||Bandwidth cap |Maximum bandwidth of the EIP. Unit: Mbps. After creating a CLB instance, you can adjust the EIP bandwidth cap anytime as needed. |20Mbps |
   ||Bandwidth Package |Join the bandwidth package. |No |
   |Specification ||Different specifications correspond to different max connections, new connections per second, queries per second, and bandwidth. Choose the appropriate specification based on your performance needs for various business scenarios. For specification details, see [Product specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02). |Small I |
   

4. Follow the console guidance to review and accept Legal.

5. Click **Submit order** to complete the action.
