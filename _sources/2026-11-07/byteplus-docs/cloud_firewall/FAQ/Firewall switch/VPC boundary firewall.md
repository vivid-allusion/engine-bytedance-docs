---
title: "VPC boundary firewall"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/VPC_boundary_firewall_faq"
---

<span id="55f6db8a"></span>
### What impact does turning on and off the VPC boundary firewall have on the business?


* **Automatic flow diversion**

   * Creating a VPC boundary firewall and deleting it after turning it off have no impact on the business.

   * Creating a diversion scenario and deleting it after turning it off have no impact on the business.

* **Manual flow diversion**

   * Creating a VPC boundary firewall and deleting it after turning it off have no impact on the business.

   * Creating a diversion scenario and deleting it after turning it off, the impact on the business depends on the custom flow diversion method.


<span id="f193f9bf"></span>
### Will there be a network interruption when the VPC firewall is bypassed? 

When the current VPC firewall is bypassed, all the routing tables associated with the network instances that have protection enabled will be switched to the system's default routing table, so whether there will be a network interruption depends on whether a default unrestricted route is configured in the system routing table. Please refer to the [VPC boundary firewall introduction](https://docs.byteplus.com/en/docs/cloud_firewall/Enabling-VPC-firewall) for the VPC firewall drainage principle.

<span id="1f59609b"></span>
### What is the routing table added in the TR transit router after creating the VPC firewall and the new drainage scenario? 

The cloud firewall realizes traffic detection between VPC instances through the custom routing function of the transit router. To avoid business interruption, do not modify or delete these routing configurations arbitrarily. Please refer to the [VPC boundary firewall introduction](https://docs.byteplus.com/en/docs/cloud_firewall/Enabling-VPC-firewall) for the VPC firewall drainage principle.

<span id="552aa461"></span>
### When creating a VPC firewall, how should the cloud firewall subnet and subnet information be filled out?


* The VPC firewall subnet segment is used for deploying firewall cluster instances, and the subnet segment filled in cannot conflict with the subnet segments of the VPC instances (dedicated line instances, VPN instances) that need protection to avoid routing conflicts that could lead to business interruptions.

* It is recommended to fill in a 28\-bit subnet for the VPC firewall subnet segment; the larger the traffic, the more IP bits the VPC firewall will require.


<span id="cb36aa67"></span>
### Does the VPC firewall support traffic protection between cross\-region VPC instances and cross\-account VPC instances?


* Automatic drainage mode is not supported.

* Manual traffic diversion mode is supported, and you need to manually configure the diversion scenario based on the network segments of cross\-account and cross\-region VPC instances that require protection. If you need help configuring the route table, you can [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001280), and cloud firewall experts will provide assistance and guidance.
