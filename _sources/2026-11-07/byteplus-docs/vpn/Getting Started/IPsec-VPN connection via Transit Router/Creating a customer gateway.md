---
title: "Creating a customer gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Creating_a_Customer_Gateway"
---

This topic describes how to quickly create an available customer gateway. This configuration example only provides required parameters. For more parameters and descriptions, see [Creating a customer gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway1).

## Procedure

1. Log in to the [Customer Gateway console](https://console.byteplus.com/vpn/vpnClient).

2. In the top menu bar, select the target project and region.

3. Click **Create Customer Gateway** to enter the Create Customer Gateway page.

4. Configure the customer gateway based on the table below.

   |Parameters |Description |Sample value |
   |---|---|---|
   |Regions |Select the region where the customer gateway resides. The customer gateway must reside in the same region as the Transit Router  **(TR\-01)** . |China (Beijing) |
   |Name |Set the name for the customer gateway. |CGW\-test |
   |IP address type |Select the IP address type for the Customer Gateway. Both IPv4 and IPv6 addresses are supported. In IPv6 communication scenarios, please ensure that all link configurations support the IPv6 protocol type.<br><br>> **tip**<br><br><br>> The IPv6 address type for customer gateway is currently in Beta stage. If you need a trial, please contact your account manager.<br> |IPv4 |
   |IP Address |Type the static EIP address of the on\-premises data center's gateway. |110.XX.XX.64 |
   |BGP ASN |Set the ASN (Autonomous System Number) for the customer gateway. Configuring BGP ASN for a customer gateway is only required for an IPsec\-VPN connection in dynamic routing mode. This example uses static routing, so BGP ASN configuration is not required. |\- |
   |Affiliated Project |The project to which the new customer gateway belongs. |project\-1 |

5. Click **Create** to complete configuration.

## What to do next

* [Create an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating_a_Customer_Gateway)

* [Configure route](https://docs.byteplus.com/en/docs/vpn/Configure_routing)

* [Test connectivity](https://docs.byteplus.com/en/docs/vpn/Test_connectivity)
