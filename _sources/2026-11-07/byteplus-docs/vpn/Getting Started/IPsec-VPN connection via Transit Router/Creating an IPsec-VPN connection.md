---
title: "Creating an IPsec-VPN connection"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Creating_an_IPsec-VPN_connection"
---

This topic describes how to quickly create an available IPsec\-VPN connection. This configuration example only provides required parameters. For more parameters and descriptions, see [Creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1).

<span id="o3IfDYhM"></span>
## Prerequisites


* You have created a customer gateway. For procedure, see [Creating a customer gateway](https://docs.byteplus.com/en/docs/vpn/Creating_a_Customer_Gateway).

* You have [created](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01) a Transit Router  **(TR\-01)**  and associated it with a Virtual Private Cloud (VPC1). For procedure, see [Creating a VPC attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpc).


<span id="o3IfDYhM"></span>
## Procedure


1. Log in to [the VPN Connection console](https://console.byteplus.com/vpn/vpnConnect). 

2. In the top menu bar, select the target project and region.

3. Click **Create VPN Connection** to enter the Create VPN connection page.

4. Configure the IPsec\-VPN connection based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Region |Select the region where the IPsec\-VPN connection is located. |China (Beijing) |
   |Name |Name of the IPsec\-VPN connection. |IPsecVPN\-test |
   |Affiliated Project |The project to which the IPsec\-VPN connection belongs. |project\-1 |
   |**Associate resources** |||
   |Attach type |Select the resource type of the new IPsec\-VPN connection associated.<br><br><br>* VPN gateway: Associate the IPsec\-VPN connection with a VPN gateway.<br><br>* TR: Associate the IPsec\-VPN connection to a Transit Router (TR).<br><br>* Associate to TR later: Associate the IPsec\-VPN connection with a TR later. |Transit Router |
   |Transit Router |Select **TR\-01** and its associated project. |All projects; **TR\-01** |
   |Availability zone |Select the availability zone to which the TR belongs. |Availability zone A |
   |**Connection information** |||
   |Routing mode |Select a routing mode. |Destination Routing Mode |
   |Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration. |Yes |
   |Routing propagation mode |Select a routing propagation mode. |Static routes |
   |Customer gateway |Select the customer gateway created in the previous phase. |CGW\-test |
   |Pre\-shared key |Type the key used for IKE negotiation between VPN devices on both sides.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Identical Pre\-Shared Keys must be configured for both local and peer ends of the IPsec\-VPN connection. Otherwise, the connection cannot be initiated.</div><br> |test@123 |
   |Confirm the key |Type the Pre\-Shared Key again. |test@123 |
   

5. Click **Create** to complete the configuration.


<span id="FMwUKPaA"></span>
## What to do next


* [Configure routing](https://docs.byteplus.com/en/docs/vpn/Configure_routing)

* [Test connectivity](https://docs.byteplus.com/en/docs/vpn/Test_connectivity)
