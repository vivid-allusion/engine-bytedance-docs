---
title: "IPsec-VPN quick start"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Quick-start"
---

By default, a Virtual Private Cloud (VPC) cannot communicate with your on\-premises data center. However, an IPsec\-VPN connection enables an encrypted tunnel between a VPC and your data center for secure encryption and transmission of data. BytePlus offers two options for establishing IPsec\-VPN tunnels: via VPN gateway and via Transit Router (TR). Choose the connection scenario based on your actual needs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This example uses static routing for the VPN Connect. To connect a VPC and an on\-premises data center via VPN Connect using dynamic routing, see the following documents:</div>



* <div data-tips="true" data-tips-type="default">IPsec\-VPN connection via VPN gateway: <a href="https://docs.byteplus.com/en/docs/vpn/connecting-a-vpc-to-multiple-data-centers-bgp-routing">Connecting a VPC to multiple data centers via IPsec\-VPN connection with dynamic routing</a>.</div>


* <div data-tips="true" data-tips-type="default">IPsec\-VPN connection via TR: <a href="https://docs.byteplus.com/en/docs/transitrouter/Best-Practices-02">Connecting VPCs to a data center through VPN Connect or Direct Connect</a>.</div>



<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Due to the business expansion requirements, a company planned to migrate some of its services to the purchased VPC (VPC1). After careful consideration, the company chose the IPsec\-VPN connection feature for its cost\-effectiveness and operational simplicity to seamlessly migrate its on\-premises services to the cloud.


* IPsec\-VPN connection via VPN gateway

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e1606be6587cf26f39c6424f471ae716.png) </span>

* IPsec\-VPN connection via Transit Router

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0a78ddc92cd16d75c7ee560716233071.png) </span>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


<Tabs>
<Tab zoneid="gkKc8IBkJL" title="IPsec-VPN connection via VPN gateway">
<TabTitle>IPsec-VPN connection via VPN gateway</TabTitle>

* You have created VPC1 and its subnets in a region closest to your data center. For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* The gateway device in your data center supports the IKE V1 or IKE V2 protocol.

* The gateway device in your data center has a static Elastic IP Address (EIP).

* The CIDR block of your data center is different from that of VPC1.


</Tab>
<Tab zoneid="PYXlTFmgcc" title="IPsec-VPN connection via TR">
<TabTitle>IPsec-VPN connection via TR</TabTitle>

* You have created VPC1 and its subnets in a region closest to your data center. For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* The gateway device in your data center supports the IKE V1 or IKE V2 protocol.

* The gateway device in your data center has a static EIP.

* The CIDR block of your data center is different from that of VPC1.

* You need to first create a TR  **(TR\-01)**   to associate with VPC1. For procedures, see [Creating a Transit Router instance](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01) and [Creating a VPC attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpc).


</Tab>
</Tabs>


<span id="o25f6eCp"></span>
## Procedure


<Tabs>
<Tab zoneid="nTyENEaC95" title="IPsec-VPN connection via VPN gateway">
<TabTitle>IPsec-VPN connection via VPN gateway</TabTitle>

1. [Create a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway): Create a VPN gateway required for a VPN Connect on VPC1, and enable IPsec\-VPN connection capability.

2. [Create a customer gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway): Create a customer gateway in the region to which VPC1 belongs, and register the peer gateway information to the cloud.

3. [Create an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection): Create an IPsec\-VPN connection on VPC1. The IPsec\-VPN connection is a communication tunnel established between the VPN gateway and the customer gateway.

4. [Configure routing](https://docs.byteplus.com/en/docs/vpn/Configuring-routes)

   * Configure routes on the VPN gateway to enable communication between VPC1 and the on\-premises data center.

   * Configure routes on the data center gateway to ​​enable communication between the data center and VPC1​​.

5. [Test connectivity](https://docs.byteplus.com/en/docs/vpn/Testing-connectivity): Log in to an Elastic Compute Service (ECS) instance that resides in VPC1 and is not associated with an EIP. Execute the `ping` command to ping the private IP address of any server that resides in the on\-premises data center and is covered by the IPsec\-VPN connection to verify the network connectivity.


</Tab>
<Tab zoneid="niyX5eulk9" title="IPsec-VPN connection via TR">
<TabTitle>IPsec-VPN connection via TR</TabTitle>

1. [Create a customer gateway](https://docs.byteplus.com/en/docs/vpn/Creating_a_Customer_Gateway): Create a customer gateway in the region to which VPC1 belongs, and register the peer gateway information to the cloud.

2. [Create an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating_an_IPsec-VPN_connection): Create an IPsec\-VPN connection. The IPsec\-VPN connection is a communication tunnel established between the TR and the customer gateway.

3. [Configure routing](https://docs.byteplus.com/en/docs/vpn/Configure_routing)

   * Configure routes on the TR to ​​enable communication between the TR and the on\-premises data center​​.

   * Configure routes on the data center gateway to ​​enable communication between the data center and the TR.

4. [Test connectivity](https://docs.byteplus.com/en/docs/vpn/Test_connectivity): Log in to an Elastic Compute Service (ECS) instance that resides in VPC1 and is not associated with an EIP. Execute the `ping` command to ping the private IP address of any server that resides in the on\-premises data center and is covered by the IPsec\-VPN connection to verify the network connectivity.


</Tab>
</Tabs>


&nbsp;

&nbsp;

&nbsp;
