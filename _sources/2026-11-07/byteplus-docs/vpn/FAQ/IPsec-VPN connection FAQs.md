---
title: "IPsec-VPN connection FAQs"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/IPsec-VPN-connection-FAQs"
---

* [What is an IPsec-VPN connection?](https://docs.byteplus.com/en/docs/52/5090#.5LuA5LmI5pivSVBzZWPov57mjqXvvJ8=)

* [Does the IPsec tunnel establish a connection automatically?](https://docs.byteplus.com/en/docs/52/5090#.SVBzZWPov57mjqXpmqfpgZPmmK_lkKbkvJroh6rliqjlu7rnq4vov57mjqXvvJ8=)

* [How long after the IPsec tunnel is established until VPN connectivity is available?](https://docs.byteplus.com/en/docs/52/5090#.SVBzZWPov57mjqXpgJrpgZPlu7rnq4vmiJDlip_lkI7ov5jpnIDopoHlpJrplb_ml7bpl7Tlj6_nlKhWUE7ov57mjqXlip_og73vvJ8=)

* [What are negotiation parameters for an IPsec-VPN connection?](https://docs.byteplus.com/en/docs/52/5090#.SVBzZWPov57mjqXnmoTljY_llYblj4LmlbDmnInlk6rkupvvvJ8=)

* [What should I be aware of when using an IPsec-VPN connection?](https://docs.byteplus.com/en/docs/52/5090#.5L2_55SoSVBzZWPov57mjqXmnInku4DkuYjms6jmhI_kuovpobnvvJ8=)

* [Do I need to configure VPN gateway routes for an IPsec-VPN connection?](https://docs.byteplus.com/en/docs/52/5090#.5L2_55SoSVBzZWPov57mjqXlv4XpobvphY3nva5WUE7nvZHlhbPot6_nlLHkuYjvvJ8=)

* [Why can't my on-premises data center access the ECS in the VPC even though the IPsec tunnel is established?](https://docs.byteplus.com/en/docs/52/5090#.5oiQ5Yqf5bu656uLSVBzZWPpgJrkv6HpmqfpgZPvvIzkuLrku4DkuYjmnKzlnLDmlbDmja7kuK3lv4Pku43ml6Dms5Xorr_pl67np4HmnInnvZHnu5zlhoXnmoTkupHmnI3liqHlmajvvJ8=)

* [How can I use the NAT traversal feature?](https://docs.byteplus.com/en/docs/52/5090#.5aaC5L2V5L2_55SoTkFU56m_6LaK5Yqf6IO977yf)

* [How do I enable the DPD feature?](https://docs.byteplus.com/en/docs/52/5090#.5aaC5L2V5byA5ZCvRFBE5Yqf6IO977yf)

* [What requirements must the peer VPN gateway meet for DPD to work?](https://docs.byteplus.com/en/docs/52/5090#.5L2_55SoRFBE5Yqf6IO977yM5a-556uvVlBO572R5YWz6ZyA6KaB5ruh6Laz5LuA5LmI5p2h5Lu277yf)

* [Can I configure two IPsec-VPN connections that are identical except for the Remote ID?](https://docs.byteplus.com/en/docs/52/5090#.5piv5ZCm5pSv5oyB6YWN572u5Lik5Liq6ZmkUmVtb3RlSUTkuI3lkIzlhbbku5bkv6Hmga_lnYfnm7jlkIznmoRJUHNlY-i_nuaOpe-8nw==)

* [Can I initiate an IPsec-VPN connection if the peer uses a non-fixed egress IP address?](https://docs.byteplus.com/en/docs/52/5090#.6Iul5a-556uv5Li66Z2e5Zu65a6a5Ye65Y-jSVDvvIzmmK_lkKbmlK_mjIHlj5HotbdJUHNlY-i_nuaOpe-8nw==)

* [How can I view the EIP of a TR IPsec-VPN connection?](https://docs.byteplus.com/en/docs/52/5090#.5aaC5L2V5p-l55yLVFLnsbvlnotJUHNlY-i_nuaOpeeahOWFrOe9kUlQ5Zyw5Z2A77yf)

* [After configuring health checks for an IPsec-VPN connection, how do I view the health check event information?](https://docs.byteplus.com/en/docs/52/5090#.SVBzZWPov57mjqXphY3nva7kuoblgaXlurfmo4Dmn6XlkI7vvIzlpoLkvZXmn6XnnIvlgaXlurfmo4Dmn6Xkuovku7bkv6Hmga_vvJ8=)

* [Why did my IPsec tunnel stop working after being connected for a period of time?](https://docs.byteplus.com/en/docs/52/5090#.5Li65LuA5LmISVBzZWPov57mjqXpmqfpgZPov57pgJrkuIDmrrXml7bpl7TlkI7lv73nhLbkuI3pgJrvvJ8=)

* [Can I view the TopN resources by traffic? How?](https://docs.byteplus.com/en/docs/52/5090#.5piv5ZCm5pSv5oyB5p-l55yL5rWB6YePVG9wTueahOi1hOa6kOS_oeaBr--8n-WmguS9leafpeeci--8nw==)

* [Which devices support integration with BytePlus VPN?](https://docs.byteplus.com/en/docs/52/5090#o70WK4I4)

* [In a multi-CIDR scenario, why are some CIDR blocks unreachable even though the IPsec-VPN connection status is "Phase 2 negotiation successful"?](https://docs.byteplus.com/en/docs/52/5090#weCxrGBw)

* [How can I achieve multi-CIDR connectivity if my on-premises gateway device does not support ikev2?](https://docs.byteplus.com/en/docs/52/5090#dO6JK6AW)


<span id=".5LuA5LmI5pivSVBzZWPov57mjqXvvJ8="></span>
## What is an IPsec\-VPN connection?

An IPsec\-VPN connection is a communication tunnel established between a customer gateway and a VPN gateway. It enables encrypted communication between your on\-premises network and a Virtual Private Cloud (VPC).

<span id=".SVBzZWPov57mjqXpmqfpgZPmmK_lkKbkvJroh6rliqjlu7rnq4vov57mjqXvvJ8="></span>
## Does the IPsec tunnel establish a connection automatically?

During IPsec\-VPN connection creation, you can control whether to establish the connection immediately by configuring **Negotiate Instantly**.


* When set to "Yes":​ The system actively initiates negotiation immediately after the IPsec\-VPN connection is created.

* When set to "No":​ The connection is not established immediately. The tunnel is triggered and established only when the peer (on\-premises data center or other VPC) actively initiates a Security Association (SA), executes a `Ping` command to access the VPC, or when data traffic passes through.


<span id=".SVBzZWPov57mjqXpgJrpgZPlu7rnq4vmiJDlip_lkI7ov5jpnIDopoHlpJrplb_ml7bpl7Tlj6_nlKhWUE7ov57mjqXlip_og73vvJ8="></span>
## How long after the IPsec tunnel is established until VPN connectivity is available?

The VPN connectivity is ready to use immediately. Once the IPsec tunnel is established, you can start using VPN for data transfer without any waiting time.

<span id=".SVBzZWPov57mjqXnmoTljY_llYblj4LmlbDmnInlk6rkupvvvJ8="></span>
## What are negotiation parameters for an IPsec\-VPN connection?


* IKE Config

   
   |Configuration item |Value |default |
   |---|---|---|
   |Version |Supports ikev1 and ikev2. |ikev2 |
   |Negotiation |Supports main and aggressive modes. This parameter only applies to ikev1. |main |
   |Authentication algorithm |Supports sha1, md5, sha256, sha384, and sha512. |sha1 |
   |Encryption algorithm |Supports aes, aes192, aes256, des, and 3des. |aes |
   |DH algorithm |Supports group1, group2, group5, and group14. |group2 |
   |Lifecycle |Valid range: 900 to 86400. Unit: seconds. |86400 |
   

* IPsec Config

   
   |Configuration item | |default |
   |---|---|---|
   |Authentication algorithm |Supports sha1, md5, sha256, sha384, and sha512. |sha1 |
   |Encryption algorithm |Supports aes, aes192, aes256, des, and 3des. |aes |
   |DH algorithm |Supports disable (not configure), group1, group2, group5, and group14. |group2 |
   |lifecycle |Valid range: 900 to 86400. Unit: seconds. |86400 |
   


<span id=".5L2_55SoSVBzZWPov57mjqXmnInku4DkuYjms6jmhI_kuovpobnvvJ8="></span>
## What should I be aware of when using an IPsec\-VPN connection?


1. Ensure that the encryption and authentication algorithms in the IKE and IPsec configurations are consistent on both ends of the IPsec\-VPN connection.

2. We recommend using ikev2 for the IKE protocol. If you must use ikev1, ensure that the IKE configuration lifetime is consistent on both ends.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you use ikev1 with inconsistent lifetime settings, the IPsec tunnel may fail to re\-establish after a connection break.   </div>
   

<span id=".5L2_55SoSVBzZWPov57mjqXlv4XpobvphY3nva5WUE7nvZHlhbPot6_nlLHkuYjvvJ8="></span>
## Do I need to configure VPN gateway routes for an IPsec\-VPN connection?

Yes, the configuration is required.

After creating an IPsec\-VPN connection, you must manually add VPN gateway route entries to enable network connectivity between the VPN gateway and your on\-premises data center or other VPC. For route configuration, see [Adding a VPN gateway route](https://docs.byteplus.com/en/docs/vpn/Adding-a-VPN-gateway-route).

<span id=".5oiQ5Yqf5bu656uLSVBzZWPpgJrkv6HpmqfpgZPvvIzkuLrku4DkuYjmnKzlnLDmlbDmja7kuK3lv4Pku43ml6Dms5Xorr_pl67np4HmnInnvZHnu5zlhoXnmoTkupHmnI3liqHlmajvvJ8="></span>
## Why can't my on\-premises data center access the ECS in the VPC even though the IPsec tunnel is established?

In this scenario, check the following configurations:


* Check the routing and Network Access Control List (ACL) in your on\-premises data center​ to ensure that traffic destined for the VPC is allowed to enter the IPsec tunnel.

* Check the security group of the target Elastic Compute Service (ECS) to confirm that the security group rules allow access from your on\-premises data center's private CIDR block.


For more information, see [IPsec-VPN connection troubleshooting](https://docs.byteplus.com/en/docs/vpn/Troubleshooting-and-solutions-for-IPsec-VPN-connection-issues).

<span id=".5aaC5L2V5L2_55SoTkFU56m_6LaK5Yqf6IO977yf"></span>
## How can I use the NAT traversal feature?

The NAT traversal feature is disabled by default. To enable it, you can turn on the NAT traversal switch when [creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1). You must also enable NAT traversal on the VPN gateway device in your on\-premises data center.

<span id=".5aaC5L2V5byA5ZCvRFBE5Yqf6IO977yf"></span>
## How do I enable the DPD feature?

The Dead Peer Detection (DPD) feature is enabled by default when creating an IPsec\-VPN connection. If you have manually disabled DPD and need to re\-enable it, go to the **Modify VPN connection**​ page and turn on the DPD​ switch.

<span id=".5L2_55SoRFBE5Yqf6IO977yM5a-556uvVlBO572R5YWz6ZyA6KaB5ruh6Laz5LuA5LmI5p2h5Lu277yf"></span>
## What requirements must the peer VPN gateway meet for DPD to work?

DPD itself does not require the peer VPN gateway to have full DPD capability, but it must be able to respond to DPD VendorID messages. If the peer VPN gateway cannot respond, DPD will continuously time out.

Therefore, before using DPD, ensure that your peer VPN gateway supports DPD VendorID response capability.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In this section, Local and Peer are used to refer to the two ends of VPN Connect.</div>



* <div data-tips="true" data-tips-type="tip">Local: The VPC side.</div>


* <div data-tips="true" data-tips-type="tip">Peer: The on\-premises data center or other VPC side.</div>



<span id=".5piv5ZCm5pSv5oyB6YWN572u5Lik5Liq6ZmkUmVtb3RlSUTkuI3lkIzlhbbku5bkv6Hmga_lnYfnm7jlkIznmoRJUHNlY-i_nuaOpe-8nw=="></span>
## Can I configure two IPsec\-VPN connections that are identical except for the Remote ID?


* ikev2: Yes, supported.

* ikev1: No, not supported. If you configure two ikev1 IPsec\-VPN connections that differ only in Remote ID but are otherwise identical, they will repeatedly disconnect and reconnect, rendering both tunnels unusable.


<span id=".6Iul5a-556uv5Li66Z2e5Zu65a6a5Ye65Y-jSVDvvIzmmK_lkKbmlK_mjIHlj5HotbdJUHNlY-i_nuaOpe-8nw=="></span>
## Can I initiate an IPsec\-VPN connection if the peer uses a non\-fixed egress IP address?

Yes, supported. However, if your peer gateway uses a non\-fixed egress IP, pay special attention to the following configuration requirements:


1. When [creating a customer gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway1), set the IP address to `0.0.0.0`.

2. When [creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1), fix the Negotiate Instantly parameter to "No".

   * Set the IKE version to **ikev1**.

   * Set the IKE negotiation mode to **aggressive**.

3. After configuration, the peer must initiate the negotiation request to the cloud VPN.

   Because the peer IP is not fixed, the cloud side cannot actively initiate negotiation requests. Even if traffic passes from the cloud to the peer, the cloud cannot start the negotiation.

4. If an IPsec\-VPN connection is interrupted, the peer must re\-initiate the negotiation request to re\-establish the connection.

5. If the peer has multiple non\-fixed egress IPs​ that need to initiate negotiation, create multiple IPsec\-VPN connections​ (one for each IP) to avoid conflicts. For procedure, see [Connecting a virtual private cloud to a data center (single non-fixed egress IP address)](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-a-data-center) and [Connecting a virtual private cloud to data centers (multiple non-fixed egress IP addresses)](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-a-data-center-1).


<span id=".5aaC5L2V5p-l55yLVFLnsbvlnotJUHNlY-i_nuaOpeeahOWFrOe9kUlQ5Zyw5Z2A77yf"></span>
## How can I view the EIP of a TR\-IPsec connection?

When an IPsec\-VPN connection is attached to a Transit Router (TR), the platform automatically assigns an Elastic IP Address (EIP) to serve as the cloud egress IP after the IPsec\-VPN connection is created.

**Procedure**


1. Log in to the VPN connection console, and select the region and project where the target IPsec\-VPN connection is located.

2. In the IPsec\-VPN connection list, click the name of the target IPsec\-VPN connection to enter the details page, and check the assigned EIP on the **Overview** tab.


<span id=".SVBzZWPov57mjqXphY3nva7kuoblgaXlurfmo4Dmn6XlkI7vvIzlpoLkvZXmn6XnnIvlgaXlurfmo4Dmn6Xkuovku7bkv6Hmga_vvJ8="></span>
## After configuring health checks for an IPsec\-VPN connection, how do I view the health check event information?

If you have configured health check for the IPsec\-VPN connection, you can view the health check event information in **the Cloud Monitor console \> Cloud Service Event**.

<span id=".5Li65LuA5LmISVBzZWPov57mjqXpmqfpgZPov57pgJrkuIDmrrXml7bpl7TlkI7lv73nhLbkuI3pgJrvvJ8="></span>
## Why did my IPsec tunnel stop working after being connected for a period of time?

This issue may occur after prolonged connectivity. Typically, resetting the IPsec\-VPN connection resolves it. For procedure, see [Reset IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Reset-IPsec-VPN-connection).

If the tunnel remains unavailable after resetting, troubleshoot based on the IPsec\-VPN connection's health check status and the associated event timestamps. If the issue persists after attempting these steps, submit a ticket.

<span id=".5piv5ZCm5pSv5oyB5p-l55yL5rWB6YePVG9wTueahOi1hOa6kOS_oeaBr--8n-WmguS9leafpeeci--8nw=="></span>
## Can I view the TopN resources by traffic? How?

Yes, supported.​ The location to view TopN traffic resource information varies depending on the resource type to which the IPsec\-VPN connection is attached.


|Resource type attached to IPsec\-VPN connection |View path |Description |
|---|---|---|
|VPN gateway |**Monitor \> IP traffic monitoring** of the VPN gateway |You can view the Top 50 resources by inbound/outbound bandwidth traffic for the VPN gateway, sorted in descending or ascending order. For procedure, see [Viewing monitoring data](https://docs.byteplus.com/en/docs/vpn/Viewing-monitoring-data#.5p-l55yL55uR5o6n5pWw5o2u). |
|Transit Router (TR) |**Monitor \> IP traffic monitoring** of the IPsec\-VPN connection |You can view the Top 50 resources by inbound/outbound bandwidth traffic for the IPsec\-VPN connection, sorted in descending or ascending order. For procedure, see [Viewing monitoring data](https://docs.byteplus.com/en/docs/vpn/Viewing-monitoring-data#.5p-l55yL55uR5o6n5pWw5o2u). |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">​IP Traffic Monitoring supports querying data from the last 7 days only, with a maximum query time range of 1 day (24 hours) per request.</div>


<span id="o70WK4I4"></span>
## Which devices support integration with BytePlus VPN Connect?

BytePlus VPN Connectt supports the RFC standards for both ikev1 and ikev2. In principle, any vendor device that complies with these standards can integrate with the BytePlus public cloud. You do not need to focus on specific device models. If your device can integrate with the BytePlus VPN due to standard compliance differences, contact your account manager.

<span id="weCxrGBw"></span>
## In a multi\-CIDR scenario, why are some CIDR blocks unreachable even though the IPsec\-VPN connection status is "Phase 2 negotiation successful"?

When using an IPsec\-VPN connection to enable connectivity between an on\-premises data center and a VPC, if the IPsec\-VPN connection uses **Protected Data Flows** with multiple CIDR blocks configured, protocol incompatibility between the VPN gateway and traditional vendor equipment (such as Cisco or H3C) may cause only one CIDR block to be reachable while others remain unreachable. We recommend using an on\-premises gateway device that supports the ikev2 RFC standards to establish the IPsec\-VPN connection.

<span id="dO6JK6AW"></span>
## How can I achieve multi\-CIDR connectivity if my on\-premises gateway device does not support ikev2 RFC standards?

If your on\-premises gateway device does not support ikev2, you can use ikev1 for the IPsec\-VPN connection and the on\-premises gateway.

With ikev1, a single IPsec\-VPN connection supports only one local subnet and one remote subnet. We recommend configuring the IPsec\-VPN connection to use **Destination Routing Mode**. On the peer gateway device, configure the protected data flows with a source of 0.0.0.0/0 and a destination of 0.0.0.0/0. Then, use BGP dynamic routing​ or static routing​ on both the VPN gateway and the on\-premises data center to control traffic forwarding.
