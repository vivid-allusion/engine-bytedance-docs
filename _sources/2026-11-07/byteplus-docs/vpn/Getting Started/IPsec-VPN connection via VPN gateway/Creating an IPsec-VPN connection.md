---
title: "Creating an IPsec-VPN connection"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection"
---

This topic describes how to quickly create an available IPsec\-VPN connection. This configuration example only provides required parameters. For more parameters and descriptions, see [Creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1).

<span id=".5pON5L2c5YmN5o-Q"></span>
## Prerequisites

The VPN gateway and customer gateway have been created. For details, see [Creating a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway) and [Creating a customer gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the VPN Connection console](https://console.byteplus.com/vpn/vpnConnect).

2. In the top menu bar, select the target project and region.

3. Click **Create VPN Connection** to enter the Create VPN connection page.

4. Configure the IPsec\-VPN connection based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Regions |Select the region where the IPsec\-VPN connection is located. |China (Beijing) |
   |Name |Name of the IPsec\-VPN connection. |IPsecVPN\-test |
   |Affiliated Project |The project to which the IPsec\-VPN connection belongs. |project\-1 |
   |**Associate resources** |||
   |Attach type |Select the resource type associated with the new IPsec\-VPN connection.<br><br><br>* VPN gateway: Associate the IPsec\-VPN connection with a VPN gateway.<br><br>* TR: Associate the IPsec\-VPN connection to a Transit Router (TR).<br><br>* Associate to TR later: Associate the IPsec\-VPN connection with a TR later. |VPN gateway |
   |VPN gateway |Select the VPN gateway created in the previous phase. |VPNGW\-test |
   |**Connection information** |||
   |Routing mode |Select a routing mode. |Destination Routing Mode |
   |Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration. |Yes |
   |Routing propagation mode |Select a routing propagation mode. |Static routes |
   |Customer gateway |Select the customer gateway created in the previous phase. |CGW\-test |
   |Pre\-shared key |Type the key used for IKE negotiation between VPN devices on both sides.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Identical Pre\-Shared Keys must be configured for both local and peer ends of the IPsec\-VPN connection. Otherwise, the connection cannot be initiated.</div><br> |test@123 |
   |Confirm key |Type the Pre\-Shared Key again. |test@123 |
   

5. Click **Create** to complete the configuration.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* [Configure routing](https://docs.byteplus.com/en/docs/vpn/Configuring-routes)

* [Test connectivity](https://docs.byteplus.com/en/docs/vpn/Testing-connectivity)
