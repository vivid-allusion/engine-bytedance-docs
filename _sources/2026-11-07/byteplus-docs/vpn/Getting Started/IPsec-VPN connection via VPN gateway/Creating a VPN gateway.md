---
title: "Creating a VPN gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway"
---

This topic describes how to quickly create an available VPN gateway. This configuration example only provides required parameters. For more parameters and descriptions, see [Creating a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway-2).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway). 

2. In the top menu bar, select the target project and region.

3. Click **Create VPN Gateway** to enter the Create VPN Gateway page.

4. Configure Basic information for the VPN gateway based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Billing method |The billing method for the VPN gateway. |Subscription |
   |Regions |Select the region where the VPN gateway resides. The VPN gateway must reside in the same region as VPC1. |China (Beijing) |
   |Name |Name of the VPN gateway. |VPNGW\-test |
   |Tunnel mode |The tunnel mode of the VPN gateway.<br><br><br>* **Single tunnel**: Only one encrypted tunnel. Tunnel failure may cause network interruption.<br><br>* **Dual tunnels**: Two encrypted tunnels in primary\-secondary mode. If the primary tunnel fails, traffic can be switched to the secondary tunnel for normal transmission. Deploy two encrypted tunnels in different availability zones, enabling disaster recovery at the availability zone level.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The dual\-tunnel mode is in the beta stage. If you need a trial, please contact your account manager.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When creating a dual\-tunnel VPN gateway for the first time, please complete cross\-service authorization according to the guidance.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When creating a dual\-tunnel VPN gateway in a region that only supports single availability zone deployment for VPN Connect, you must configure both tunnels within the same zone.   </div><br>    |Single tunnel |
   |IP address type |The IP address type for the connection between the VPN gateway and the client. A single\-tunnel mode VPN gateway only supports the IPv4 address type. |IPv4 |
   |Protocol type |The protocol type used within the VPN gateway tunnels. All tunnels associated with the VPN gateway will use the same protocol type. A single\-tunnel mode VPN gateway only supports the IPv4 address type. |IPv4 |
   

5. Configure Network information for the VPN gateway based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Bandwidth |Set the bandwidth cap for the VPN gateway.<br><br>This value is the bandwidth shared for all VPN Connects created on this VPN gateway. That is, the total bandwidth of VPN Connects cannot exceed the bandwidth of the VPN gateway. |5Mbps |
   |VPC |The Virtual Private Cloud (VPC) where the VPN gateway resides. |VPC1\|10.0.0.0/24 |
   |Subnet |Select the subnet where the VPN gateway resides.<br><br>Reserve IPv4 addresses in the subnet as deploying the VPN gateway will occupy three IPv4 addresses of the subnet. |subnet1\|10.0.0.0/24 |
   |BGP ASN |Set the Autonomous System Number (ASN) for the VPN gateway. Configuring BGP ASN for a VPN gateway is only required for an IPsec\-VPN connection in dynamic routing mode. This example uses static routing, so BGP ASN configuration is not required. |\-\- |
   

6. Configure Feature information for the VPN gateway based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |IPsec\-VPN connection |Enable IPsec\-VPN connectivity as needed. After enabling, you can use the IPsec\-VPN feature. |Check |
   |SSL\-VPN connection |Enable SSL\-VPN connectivity as needed. After enabling, you can use the SSL\-VPN feature.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">带宽规格为3Gbps的VPN网关SSL\-VPN cannot be enabled for VPN gateways with a Bandwidth of 3 Gbps and dual\-tunnel VPN gateways.</div><br> |Disabled |
   

7. Configure more information for the VPN gateway based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Duration |Select the ​​validity period​​ for which the VPN gateway is subscribed. |1 month |
   |Automatic renewal |Enable automatic renewal as needed. |Disabled |
   |Affiliated Project |The project to which the new VPN gateway belongs. |default |
   

8. After the configuration is completed, click **Confirm order**.

9. After confirming that the **configuration information** is correct, follow the console guidance to review and accept the legal terms and then click **Buy now**.

10. After confirming that the order information is correct, proceed with payment according to the guidance. 

   After the VPN gateway is created, the system assigns an egress IP address: 180.XX.XX.43. It is displayed in the **IP Address** column of the VPN gateway list.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* [Create a customer gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway)

* [Create an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection)

* [Configure routing](https://docs.byteplus.com/en/docs/vpn/Configuring-routes)

* [Test connectivity](https://docs.byteplus.com/en/docs/vpn/Testing-connectivity)
