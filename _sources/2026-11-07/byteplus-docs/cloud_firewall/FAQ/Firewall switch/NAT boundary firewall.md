---
title: "NAT boundary firewall"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/NAT_boundary_firewall_faq"
---

<span id="b87454e4"></span>
### What is the impact of enabling and disabling the NAT boundary firewall on business?


* Creating a NAT boundary firewall: No impact on business.

* Configuring the diversion scenario: Due to the need to adjust routing configuration (switching the business subnet access destination `0.0.0.0/0` from the NAT gateway to the cloud firewall diversion node), there will be a brief business interruption during the operation. It is recommended to perform this operation during off\-peak business hours.

* Deleting the NAT boundary protection: You must manually switch business traffic first, otherwise it may cause business interruption.


<span id="516c0fdd"></span>
### Why does the NAT boundary firewall need to create a routing table? 

The NAT firewall needs to create a dedicated subnet and routing table for deploying the firewall traction node (gateway load balancing endpoint) to achieve traffic diversion between the business subnet and the NAT gateway. For the principle of NAT firewall traffic diversion, please refer to [NAT boundary firewall introduction](https://docs.byteplus.com/en/docs/cloud_firewall/Introduction_to_NAT_boundary_firewall).

<span id="e4107066"></span>
### When both the internet boundary and NAT boundary firewalls are enabled, how is the inbound and outbound internet traffic matched?


* Outbound traffic: Business subnet \-\> NAT boundary firewall \-\> NAT gateway \-\> Internet boundary firewall

* Inbound traffic: Internet boundary firewall \-\> NAT gateway \-\> NAT boundary firewall \-\> Business subnet


<span id="0b81c572"></span>
### When creating a NAT firewall, how should the cloud firewall subnet information be filled in? 

When creating a NAT firewall, it is necessary to add a subnet for deploying the NAT firewall traction node (gateway load balancing endpoint), and only a 29\-bit subnet is required.

<span id="aeed6adb"></span>
### Does the NAT boundary firewall support protection for DNAT traffic? 

Supports simultaneous protection for SNAT and DNAT traffic.
