---
title: "Implementing interconnectivity between independent VPCs and a data center (same account, cross-region)"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Best-Practices-02"
---

This topic describes how to configure Transit Router (TR) for cross\-region connectivity under the same account, allowing different Virtual Private Clouds (VPCs) to access the same on\-premises data center while remaining isolated from each other.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

By integrating with VPN Connect or Direct Connect (DC) services, the TR flexibly enables interconnectivity and isolation between separate VPCs and an on\-premises data center.

In the diagram below, all cloud resources such as VPCs and TRs belong to the same account. Two VPCs in China (Guangzhou) can access the data center in China (Beijing) via TR, while the two VPCs cannot access each other.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f2a20aaaa01ae954957242db46f94c9a.png) </span>

<span id=".5pWw5o2u6KeE5YiS"></span>
## Data planning

Before configuration, plan the CIDR blocks, routes, and other data parameters for each network resource in the diagram as shown below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Routes in the VPC route tables illustrated below can be manually configured or automatically synchronized. This example uses auto publishing.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_20222f7ce67f164df62ff11e809437d5.png) </span>


* Virtual Private Cloud

   
   |Region |VPC |VPC CIDR block |Subnet name |Subnet availability zone |Subnet segment |ECS private IP |
   |---|---|---|---|---|---|---|
   |China (Guangzhou) |vpc01 |192.168.0.0/20 |subnet01 |Availability Zone A |192.168.0.0/24 |192.168.0.10 |
   ||vpc02 |192.168.16.0/20 |subnet01 |Availability Zone A |192.168.16.0/24 |192.168.16.10 |
   

* VPN Connect

   
   |Region |IPsec\-VPN connection |Customer gateway |Local Subnet |Remote Subnet |Pre\-shared key |
   |---|---|---|---|---|---|
   |China (Beijing) |ipsec01 |* Name: cgw01<br><br>* BGP ASN: 65000<br><br>* IP address: 12.XX.XX.10<br><br><br>> This IP address is the public IP address of a server in the on\-premises data center. |* 192.168.0.0/24<br><br>* 192.168.16.0/24<br><br><br>> This CIDR block should be configured as a subnet CIDR block of the VPC. |172.16.0.0/24<br><br>> This CIDR block should be configured as a subnet CIDR block of the on\-premises data center. |test@123 |
   

* Direct Connect

   
   |Region |DC Gateway |DC Connection |Name of the DC Virtual Interface |Cloud/Your gateway peer IP |Route type |BGP ASN |BGP key |
   |---|---|---|---|---|---|---|---|
   |China (Beijing) |dcg01 |DAS123_port308_conn |vif01 |* Cloud: 10.0.0.1/30<br><br>* Your: 10.0.0.2/30 |BGP |49600 |E0g5\*\*\*\*8go1 |
   

* Transit Router

   The route planning is illustrated above. For details, see [TR Route configuration planning](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-02).

* On\-premises data center

   
   |Region |Subnet |ECS name |Private IP address |Public IP address |
   |---|---|---|---|---|
   |China (Beijing) |172.16.0.0/24 |server01 |172.16.0.10 |12.XX.XX.10 |
   


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created necessary VPCs and their subnets. For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* You have created Elastic Compute Service (ECS) instances in all VPCs. For procedure, see [Purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* You have completed the following configuration based on the service type connecting to the on\-premises data center. For parameters, see [Data planning](https://docs.byteplus.com/en/docs/transitrouter/Best-Practices-02#.5pWw5o2u6KeE5YiS).

   * **VPN**: See [Creating a Customer Gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway1) and create a customer gateway (named cgw01) required for this scenario.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The IPsec\-VPN connection in this example uses dynamic routing, ensuring that your customer gateway supports BGP and that valid ASNs have been configured for associated resources and the customer gateway.      </div>
      

   * **DC**: Follow the first three steps in [Configuring a DC Connection](https://docs.byteplus.com/en/docs/directconnect/Quick-start#.6YWN572u5LiT57q_6L-e5o6l) to create a DC Connection, DC Gateway, and DC Virtual Interface. Then complete private route configuration in the on\-premises data center by seeing [Configuring on-premises routing](https://docs.byteplus.com/en/docs/directconnect/Configuring-a-local-route-and-testing-connectivity#.6YWN572u5pys5Zyw6Lev55Sx).



&nbsp;

* You have obtained the IP address of the server in the data center and ensured the server is properly operational.


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This example only covers required parameters. Leave other parameters at their default values.</div>


<span id=".5q2l6aqk5LiA77ya6YWN572u5Y2O5Y2XMe-8iOW5v-W3nu-8ieWcsOWfn-S4reeahFRS5a6e5L6L"></span>
### Step 1: Configure a TR instance in China (Guangzhou)

In this step, you need to create one TR instance, one custom route table and two network instance attachments for the TR. For procedure, see [Configure a TR instance in China (Guangzhou)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-03#.5q2l6aqk5LiA77ya6YWN572u5Y2O5Y2XMe-8iOW5v-W3nu-8ieWcsOWfn-S4reeahFRS5a6e5L6L).


1. Create a TR instance.

   Create a TR instance (named tr01) in China (Guangzhou) to host the TR service.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In this example, assign 64512 to tr01 as its ASN.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you create a TR instance, the system automatically creates a system route table for it to forward access traffic from vpc01 and vpc02 in the same region. The following uses tr01's system route table (named <strong>tr01\-rtb\-sys</strong>) as an example.   </div>
   

2. Create a TR custom route table.

   Create a custom route table (named tr01\-rtb\-set) for tr01 to forward access traffic from the inter\-region attachment.

3. Create a network instance attachment and configure routing

   Create two network instance attachments for tr01 (named attach\-vpc01 and attach\-vpc02) to connect with respective VPC instances (vpc01 and vpc02) in the same region.

4. View TR and VPC routes

   * tr01\-rtb\-sys contains no entries, while the routes in tr01\-rtb\-set are listed below.

      
      |Destination CIDR |Next Hop |Route status |Route type |Attachment type |Network instance |Route attribute |
      |---|---|---|---|---|---|---|
      |192.168.0.0/24 |attach\-vpc01 |Available |Route learning |VPC |vpc01 |\- |
      |192.168.16.0/24 |attach\-vpc02 |Available |Route learning |VPC |vpc02 |\- |
      

   * Since the routes in tr01\-rtb\-sys are automatically published to the vpc01 and vpc02 route tables, the routes in those tables remain unchanged.


<span id=".5q2l6aqk5LqM77ya6YWN572u5Y2O5YyXMu-8iOWMl-S6rO-8ieWcsOWfn-S4reeahFRS5a6e5L6L"></span>
### Step 2: Configure a TR instance in China (Beijing)


1. Create a TR instance.

   Create a TR instance (named tr02) in China (Beijing). For procedure, see [Creating a Transit Router instance](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In this example, assign 64513 to tr02 as its ASN.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you create a TR instance, the system automatically creates a system route table for it. The following uses tr02's system route table (named <strong>tr02\-rtb\-sys</strong>) as an example.   </div>
   

2. Create a network instance attachment.

   Create the appropriate network instance attachment based on the resource type connecting to the on\-premises data center. For procedure, see [Creating a VPN attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpn) or [Creating a DC Gateway attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-dc).

   
   <Tabs>
   <Tab zoneid="pGn5lyEDDM" title="Connect to the on-premises data center via VPN">
   <TabTitle>Connect to the on-premises data center via VPN</TabTitle>
   
   * Basic configuration
   
      
      |**Parameter** |**Description** |**Example** |
      |---|---|---|
      |Name |The name for the network instance attachment to be created. |attach\-ipsec01 |
      |Attachment type |Select the type for the network instance attachment to be created.<br><br>Select VPN and create a new IPsec\-VPN connection. |VPN Connect |
      |IPsec name |Type the name for the IPsec\-VPN connection to be created. |ipsec01 |
      |Specification |Select the instance type for the IPsec\-VPN connection, supporting **Default** and **Large**. Different specifications incur different IPsec instance fees. For fee details, see [IPsec-VPN connection billing](https://docs.byteplus.com/en/docs/vpn/IPsec-VPN-connection-billing).<br><br><br>* **Default specification** supports a bandwidth of 200 Mbps.<br><br>* **Large specification** supports a bandwidth of 1 Gbps.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The large specification is in the beta stage. If you need a trial, please contact your account manager.</div><br> |default |
      |Routing mode |Select routing mode. |Protected Data Flows |
      |Local Subnet |In this example, this parameter is configured as the subnet CIDR block of the VPC. |192.168.0.0/24, 192.168.16.0/24 |
      |Remote Subnet |In this example, this parameter is configured as the subnet CIDR block of the data center. |172.16.0.0/24 |
      |Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration. |Yes |
      |Routing propagation mode |Select the route propagation mode for the IPsec\-VPN connection. [Prerequisite](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1)<br><br>If you select Static routing, after the VPN attachment is created, configure the data center's CIDR block as the destination CIDR block and the VPN attachment as the next hop for the route by seeing [Creating a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05#.5Yib5bu66Z2Z5oCB6Lev55Sx). |Dynamic |
      |Customer gateway |Select an existing customer gateway. |cgw01 |
      |Tunnel CIDR block |The CIDR block where the local and peer tunnel IPs reside. |169.254.1.0/30 |
      |Local Tunnel IP |The local tunnel IP is the BGP address configured on the VPN gateway. |169.254.1.1 |
      |Peer Tunnel IP |The peer tunnel IP is the BGP address configured on the user device. |169.254.1.2 |
      |Pre\-shared key |Type the key used for IKE negotiation between both VPN devices. |test@123 |
      |Confirm key |Type Pre\-Shared Key again. |test@123 |
      |Project |Select the project to which the to\-be\-created TR instance belongs. |default |
      |Availability zone |Select the availability zone to provide VPN gateway service. |Availability Zone A |
      
   
   * Route configuration
   
      
      |**Parameter** |**Description** |**Example** |
      |---|---|---|
      |Association forwarding |If association forwarding is enabled, the traffic from the network instance will be forwarded based on the TR route table (tr02\-rtb\-sys). |Enabled, tr02\-rtb\-sys |
      |Route learning |After enabling route learning, the TR route table (tr02\-rtb\-sys) automatically learns routes of the selected network instance, and generates entries with the destination as data center's CIDR blocks and the next hop as this attachment (attach\-ipsec01). |Enabled, tr02\-rtb\-sys |
      
   
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">After the VPN attachment is created, complete the VPN configuration on the server in the on\-premises data center, ensuring it is consistent with the IPsec\-VPN connection settings. For parameters, see <a href="https://docs.byteplus.com/en/docs/transitrouter/Best-Practices-02#.5pWw5o2u6KeE5YiS">Data planning</a>.</div>
   
   
   
   </Tab>
   <Tab zoneid="SKMhZIZhrL" title="Connect to the on-premises data center via DC">
   <TabTitle>Connect to the on-premises data center via DC</TabTitle>
   
   Configure the basic information, network instance, and routing information for the network instance attachment based on the table below.
   
   
   |**Parameter** |**Description** |**Example** |
   |---|---|---|
   |**Basic information** |||
   |TR |Defaults to the selected TR instance, requiring no manual configuration. |tr02 |
   |Region |Defaults to the same region as the TR instance. No manual configuration required. |China (Beijing) |
   |Name |The name for the network instance attachment to be created. |attach\-dcg01 |
   |**Network instances** |||
   |Attachment type |Select the type for the network instance attachment to be created. |Direct Connect Gateway |
   |DC Gateway |Select the DC Gateway instance to be connected. |dcg01 |
   |**Route configuration** |||
   |Association forwarding |If association forwarding is enabled, the traffic from the network instance will be forwarded based on the TR route table (tr02\-rtb\-sys). |Enabled, tr02\-rtb\-sys |
   |Route learning |After enabling route learning, the TR route table (tr02\-rtb\-sys) automatically learns routes of the selected network instance. It generates entries with the destination as data center's subnets and the next hop as this network instance attachment (attach\-dcg01). |Enabled, tr02\-rtb\-sys |
   
   
   
   
   
   </Tab>
   </Tabs>
   

3. View tr02\-rtb\-sys, confirming that the route table has learned routes pointing to the data center from the DC or VPN.

   * When connecting to the data center via DC, tr02\-rtb\-sys should have learned the routes listed in the table below.

      
      |Destination CIDR |Next Hop |Route status |Route type |Attachment type |Network instance |Route attribute |
      |---|---|---|---|---|---|---|
      |172.16.0.0/24 |attach\-dcg01 |Available |Route learning |DC Gateway |dcg01 |49600 |
      

   * When connecting to the data center via VPN, tr02\-rtb\-sys should have learned the routes listed in the table below.

      
      |Destination CIDR |Next Hop |Route status |Route type |Attachment type |Network instance |Route attribute |
      |---|---|---|---|---|---|---|
      |172.16.0.0/24 |attach\-ipsec01 |Available |Route learning |VPN Connect |ipsec01 |65000 |
      

&nbsp;


<span id=".5q2l6aqk5LiJ77ya6YWN572u6Leo5Zyw5Z-f5bim5a69"></span>
### Step 3: Configure inter\-region bandwidth


1. Create a bandwidth package.

   Create a bandwidth package (named trbp01) to provide bandwidth resources for the inter\-region attachment. For procedure, see [Creating a TR bandwidth package](https://docs.byteplus.com/en/docs/transitrouter/TR-bandwidth-packages-01).

2. Create an inter\-region attachment.

   Create an inter\-region attachment to link the TR instance in China (Guangzhou) and the TR instance in China (Beijing). For procedure, see [Creating an inter-region attachment](https://docs.byteplus.com/en/docs/transitrouter/Inter-region-peering-attachments-01).

   This example uses the TR instance in China (Guangzhou), tr01, as Local TR to create an inter\-region attachment. Specific parameters are shown in the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Name |Type the name for the inter\-region attachment. |attach\-tr |
   |Bandwidth package |Add to the created bandwidth package (trbp01) and allocate bandwidth. |Checked, trbp01, 2 Mbps |
   |Local associated route table |Enable associated forwarding to allow the local TR instance (tr01) to forward access traffic from inter\-region attachment according to tr01\-rtb\-set. |Enabled, tr01\-rtb\-set |
   |Remote TR association forwarding |Enable associated forwarding to allow the peer TR instance (tr02) to forward access traffic from the inter\-region attachment according to tr02\-rtb\-sys. |Enabled, tr02\-rtb\-sys |
   |Local TR route learning |Enable route learning to allow tr01\-rtb\-sys to automatically learn routes from the peer TR route table (tr02\-rtb\-sys) associated with forwarding. |Enabled, tr01\-rtb\-sys |
   |Remote TR route learning |Enable route learning to allow the specified TR route table (tr02\-rtb\-sys) to automatically learn routes from the local TR route table (tr01\-rtb\-set) associated with forwarding. |Enabled, tr02\-rtb\-sys |
   

3. View TR and VPC routes

   * The routes in the TR route table (tr01\-rtb\-set) remain unchanged.

   * The routes in TR route tables (tr01\-rtb\-sys and tr02\-rtb\-sys) vary depending on the type of network resources connected to the data center.

      * When connecting to the data center via DC, tr02\-rtb\-sys should have learned the routes listed in the table below.

         
         |Route table name |Destination CIDR |Next Hop |Route status |Route type |Attachment type |Network instances |Route attribute |
         |---|---|---|---|---|---|---|---|
         |tr01\-rtb\-sys |172.16.0.0/24 |attach\-tr |Available |Route learning |TR |tr02 |64513,49600 |
         |tr02\-rtb\-sys |192.168.0.0/24 |attach\-tr |Available |Route learning |TR |tr01 |64512 |
         ||192.168.16.0/24 |attach\-tr |Available |Route learning |TR |tr01 |64512 |
         

      * When connecting to the data center via VPN, tr02\-rtb\-sys should have learned the routes listed in the table below.

         
         |Route table name |Destination CIDR |Next Hop |Route status |Route type |Attachment type |Network instance |Route attribute |
         |---|---|---|---|---|---|---|---|
         |tr01\-rtb\-sys |172.16.0.0/24 |attach\-tr |Available |Route learning |TR |tr02 |64513,65000 |
         |tr02\-rtb\-sys |192.168.0.0/24 |attach\-tr |Available |Route learning |TR |tr01 |64512 |
         ||192.168.16.0/24 |attach\-tr |Available |Route learning |TR |tr01 |64512 |
         

   * The system route tables of vpc01 and vpc02 have learned the routes to the data center's CIDR block from the TR, as shown in the table below.

      
      |Destination CIDR |Status |Next Hop type |Next Hop |
      |---|---|---|---|
      |172.16.0.0/24 |Available |TR |tr01 |
      


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation


1. Log in to the ECS instance in vpc01. For procedure, see [Logging on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging on to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Execute the `ping` command to connect to respective servers in vpc02 and the on\-premises data center. Verify that vpc01 communicates with the data center but not with vpc02.

3. Similarly, log in to the ECS instance in vpc02 and verify connectivity between vpc02 and the server in the data center.
