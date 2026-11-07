---
title: "Implementing interconnectivity between independent VPCs and a data center (cross-account, cross-region)"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Interconnectivity-between-VPCs-and-idc-cross-account-interregion"
---

This topic describes how to configure Transit Router (TR) for cross\-account, cross\-region connectivity, allowing different Virtual Private Clouds (VPCs) to access the same on\-premises data center while remaining isolated from each other.

<span id="DseT8cGw"></span>
## Scenarios

A company has deployed two VPCs in Region A. Both VPCs need to share the VPN Connect or Direct Connect (DC) resources owned by another account in Region B to access the on\-premises data center, while the two VPCs themselves must remain isolated from each other.​ ​​This scenario can be implemented using TR, as illustrated in the following diagram.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5024c308f2d9d223a61e1675354c4a4e.png) </span>

<span id="MEfFHBYl"></span>
## Data planning


* Select a region that is closest to the geographical location of the data center for VPN or DC. This example selects China (Beijing).

* Before configuration, plan the CIDR blocks, routes, and other parameters for the network resources shown in the topology diagram.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Routes in the VPC route tables illustrated below can be manually configured or automatically synchronized. This example uses auto publishing.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c421d182201e3573342318640f18f4e2.png) </span>


* Virtual Private Cloud

   
   |Region |Account |Resource type |VPC CIDR block |CIDR block |Subnet information |
   |---|---|---|---|---|---|
   |China (Guangzhou) |Account A |VPC |vpc01 |192.168.0.0/20 |\-\- |
   ||||vpc02 |192.168.16.0/20 |\-\- |
   |||Subnet |subnet01 |192.168.0.0/24 |* Affiliated availability zone: AZ\-A<br><br>* ECS private IP: 192.168.0.10 |
   ||||subnet02 |192.168.16.0/24 |* Affiliated availability zone: AZ\-A<br><br>* ECS private IP: 192.168.16.10 |
   

* VPN Connect

   
   |Region |Account |Resource type |Resource name |IP address/CIDR block |Routing information |
   |---|---|---|---|---|---|
   |China (Beijing) |Account B |IPsec\-VPN connection |ipsec01 |* Tunnel CIDR block: 169.254.1.0/30<br><br>   * Local Tunnel IP: 169.254.1.1<br><br>   * Peer Tunnel IP: 169.254.1.2<br><br>* Pre\-shared key: test@123 |\-\- |
   |||Customer gateway |cgw01 |IP address: 12.XX.XX.10<br><br>> This IP address is the public IP address of a server in the on\-premises data center. |BGP ASN: 65000 |
   

* Direct Connect

   
   |Region |Account |Resource type |Resource name |Interconnection information (IPv4) |Routing information |
   |---|---|---|---|---|---|
   |China (Beijing) |Account B |DC Connection |DAS123_port308_conn |\-\- |\-\- |
   |||DC Gateway |dcg01 |\-\- |\-\- |
   |||Virtual Interface |vif01 |* ​Local Gateway Interconnection IP: 10.0.0.1/30​​<br><br>* Your gateway peer IP: 10.0.0.2/30​​ |* Route type: BGP<br><br>* BGP ASN: 49600<br><br>* BGP key: E0g5\*\*\*\*8go1 |
   

* Transit Router

   For detailed route planning, see [TR Route configuration planning](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-02).

   
   |Region |Account |Resource type |Resource name |Routing information |
   |---|---|---|---|---|
   |China (Guangzhou) |Account A |TR instance |tr01 |ASN: 64512 |
   |||Intra\-region VPC attachment |* attach\-vpc01<br><br>* attach\-vpc02 |* Association forwarding: tr01\-rtb\-sys<br><br>* Route learning: tr01\-rtb\-set<br><br>* Auto publishing: On |
   |||TR route table |* tr01\-rtb\-sys<br><br>* tr01\-rtb\-set |\-\- |
   |\-\- ||Inter\-region attachment |attach\-tr |* Local association forwarding: tr01\-rtb\-set<br><br>* Peer association forwarding: tr02\-rtb\-sys<br><br>* Local route learning: tr01\-rtb\-sys<br><br>* Peer route learning: tr02\-rtb\-sys |
   |China (Beijing) |Account B |TR instance |tr02 |ASN: 64513 |
   |||Intra\-region VPN attachment |attach\-ipsec01 |* Association forwarding: tr02\-rtb\-sys<br><br>* Route learning: tr02\-rtb\-sys |
   |||Intra\-region DC Gateway attachment |attach\-dcg01 |* Association forwarding: tr02\-rtb\-sys<br><br>* Route learning: tr02\-rtb\-sys |
   |||TR route table |tr02\-rtb\-sys |\-\- |
   

* Data center

   
   |Subnet |ECS name |Private IP address |Public IP address |
   |---|---|---|---|
   |172.16.0.0/24 |server01 |172.16.0.10 |12.XX.XX.10 |
   


<span id="UBtZMJa5"></span>
## Prerequisites


* You have created necessary VPCs and their subnets. For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* You have created Elastic Compute Service (ECS) instances in all VPCs. For procedure, see [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* You have completed the following configuration based on the service type connecting to the on\-premises data center. For parameters, see [Data planning](https://docs.byteplus.com/en/docs/transitrouter/Best-Practices-02#.5pWw5o2u6KeE5YiS).

   * **VPN**: See [Creating a Customer Gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway1) and create a customer gateway (named cgw01) required for this scenario.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The IPsec\-VPN connection in this example uses dynamic routing, ensuring that your customer gateway supports BGP and that valid ASNs have been configured to associated resources and the customer gateway.      </div>
      

   * **DC**: Follow the first three steps in [Configuring a DC Connection](https://docs.byteplus.com/en/docs/directconnect/Quick-start#.6YWN572u5LiT57q_6L-e5o6l) to create a DC Connection, DC Gateway, and DC Virtual Interface, and then complete private route configuration in the on\-premises data center by seeing [Configuring on-premises routing](https://docs.byteplus.com/en/docs/directconnect/Configuring-a-local-route-and-testing-connectivity#.6YWN572u5pys5Zyw6Lev55Sx).

* You have obtained the IP address of the server in the data center and ensured the server is properly operational.


<span id="KQWV0ng3"></span>
## Configuration procedures

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This example only covers required parameters. Leave other parameters at their default values.</div>


<span id="f7A2PnUU"></span>
### Step 1: Configure a TR instance in China (Guangzhou) (Account A)


1. [Create a TR instance](http://volcengine.com/docs/6979/2116745?lang=zh&TagIDs=2%2C105%2C104%2C95%2C94): Create a TR instance to host the TR service.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Regions |Select a region closer to your service for shorter network delays and faster access. |China (Guangzhou) |
   |Name |Type a name for easy identification. |tr01 |
   |ASN |An Autonomous System (AS) is a network unit on the internet with a unified routing policy, composed of one or more networks and identified by a unique Autonomous System Number (ASN). Specify a private ASN for the TR instance from the range of 64512–65534 or 4200000000–4294967294.<br><br>After being assigned with an ASN, the TR automatically prepends the ASN to the AsPath attribute of routes published from it to other network instances. |64512 |
   |Agreement |Follow the console guidance to review and accept Legal. |Check |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you create a TR instance, the system automatically creates a system route table for it (e.g., named tr01\-rtb\-sys). In this example, this system route table is used to forward traffic from the cross\-region TR instance (tr02).​   </div>
   

2. [Create a TR custom route table](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-03?lang=zh): Create a custom route table (named tr01\-rtb\-set) for tr01 to forward traffic from vpc01 and vpc02.

3. [Create a VPC attachment and configure routing](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpc?lang=zh): Create two VPC attachments (named attach\-vpc01 and attach\-vpc02) for tr01, respectively connecting to VPC instances (vpc01 and vpc02).

   
   |Parameter |Description |Example<br><br>(Attach vpc01) |Example<br><br>(Attach vpc02) |
   |---|---|---|---|
   |Name |Type a name for easy identification. |attach\-vpc01 |attach\-vpc02 |
   |Attachment type |Select the type for the network instance attachment to be created. |VPC |VPC |
   |VPC |Select the VPC instance to be connected. |vpc01 |vpc02 |
   |Availability Zone and Subnet |Select the entry point where TR connects to the VPC. Select the availability zone and then the subnet, and set the selected availability zone as the default availability zone. |Availability Zone A; subnet01 |Availability Zone A; subnet02 |
   |Association forwarding |The TR will forward traffic from the related network instance based on the route table associated with this network instance attachment.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Take attach\-vpc01 as an example. After enabling association forwarding, the TR forwards traffic from vpc01 based on tr01\-rtb\-sys.</div><br> |Enabled, tr01\-rtb\-sys |Enabled, tr01\-rtb\-sys |
   |Route learning |After enabling route learning, the TR route table will automatically learn routes of the network instance, and generate entries with the destination as VPC subnets and the next hop as this network instance attachment.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Take attach\-vpc01 as an example. After enabling route learning, the TR route table (tr01\-rtb\-set) automatically generates routes whose destinations are vpc01 subnets and the next hop is attach\-vpc01. That is, routes pointing to vpc01 are configured in tr01\-rtb\-set.</div><br> |Enabled, tr01\-rtb\-set |Enabled, tr01\-rtb\-set |
   |Auto Publish Route |Enabling auto publishing will automatically synchronize routes from the associated TR route table to all route tables within the selected VPC. These synchronized routes are marked as system routes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Take attach\-vpc01 as an example. After enabling auto publishing, the system automatically synchronizes the routes from tr01\-rtb\-sys to all route tables within vpc01. These synchronized routes are system routes. That is, routes pointing to the TR are configured in the vpc01 route tables.</div><br> |Check |Check |
   

4. View TR and VPC routes

   * tr01\-rtb\-sys contains no entries, while the routes in tr01\-rtb\-set are listed below.

      
      |Destination CIDR |Next Hop |Route status |Route type |Attachment type |Network Instances |Route attribute |
      |---|---|---|---|---|---|---|
      |192.168.0.0/24 |attach\-vpc01 |Available |Route learning |VPC |vpc01 |\- |
      |192.168.16.0/24 |attach\-vpc02 |Available |Route learning |VPC |vpc02 |\- |
      

   * Since the routes in tr01\-rtb\-set are automatically published to the vpc01 and vpc02 route tables, routes in the vpc01 and vpc02 route tables are unchanged.


<span id="98z57nCJ"></span>
### Step 2: Configure the TR instance in China (Beijing) (Account B)


1. [Create a TR instance](http://volcengine.com/docs/6979/2116745?lang=zh&TagIDs=2%2C105%2C104%2C95%2C94): Create a TR instance to host the TR service.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Regions |Select a region closer to your service for shorter network delays and faster access. |China (Beijing) |
   |Name |Type a name for easy identification. |tr02 |
   |ASN |An Autonomous System (AS) is a network unit on the internet with a unified routing policy, composed of one or more networks and identified by a unique Autonomous System Number (ASN). Specify a private ASN for the TR instance from the range of 64512–65534 or 4200000000–4294967294.<br><br>After being assigned with an ASN, the TR automatically prepends the ASN to the AsPath attribute of routes published from it to other network instances. |64513 |
   |Agreement |Follow the console guidance to review and accept Legal. |Check |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you create a TR instance, the system automatically creates a system route table for it (e.g., named tr02\-rtb\-sys). In this example, this system route table is used to forward traffic from the cross\-region TR instance (tr01) and the on\-premises data center.​   </div>
   

2. Create a network instance attachment: Create the appropriate network instance attachment based on the resource type connecting the data center. For procedure, see [Creating a VPN attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpn) or [Creating a DC Gateway attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-dc).

   
   <Tabs>
   <Tab zoneid="tRfTRpkJY2" title="Connect to the data center via VPN">
   <TabTitle>Connect to the data center via VPN</TabTitle>
   
   * Basic configuration
   
      
      |**Parameter** |**Description** |**Example** |
      |---|---|---|
      |Name |Type a name for easy identification. |attach\-ipsec01 |
      |Attachment type |Select VPN and create a new IPsec\-VPN connection. |Virtual Private Network (VPN) |
      |IPsec name |Type the name for the IPsec\-VPN connection to be created. |ipsec01 |
      |Specification |Bandwidth caps vary by specification. The **default** specification has a bandwidth cap of 200 Mbps.​ For higher bandwidth, see [Creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1) to adapt. |default |
      |Routing mode |Select routing mode. |Destination routing |
      |Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration. |Yes |
      |Routing propagation mode |Select the route propagation mode for the IPsec\-VPN connection.<br><br><br>* Dynamic routing: No manual configuration is required for the TR routes after the VPN attachment is created.<br><br>* Static routing: After the VPN attachment is created successfully, manually configure routes on the TR side (setting the destination CIDR block to the data center CIDR block, and the next hop to this VPN attachment). For procedure, see [Create a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05#.5Yib5bu66Z2Z5oCB6Lev55Sx). |Dynamic |
      |Customer gateway |Select an existing customer gateway. |cgw01 |
      |Tunnel CIDR block |The CIDR block where the local and peer tunnel IPs reside. |169.254.1.0/30 |
      |Local Tunnel IP |Configure the BGP address on the BytePlus VPN service. |169.254.1.1 |
      |Peer Tunnel IP |Configure the BGP address on the customer gateway device. |169.254.1.2 |
      |Pre\-shared key |Type the key used for IKE negotiation between both VPN devices. |test@123 |
      |Confirm key |Type Pre\-Shared Key again. |test@123 |
      |Availability zone |Select the availability zone for VPN. |Availability zone A |
      
   
   * Route configuration
   
      
      |**Parameter** |**Description** |**Example** |
      |---|---|---|
      |Association forwarding |If association forwarding is enabled, the traffic from the network instance will be forwarded based on the TR route table (tr02\-rtb\-sys). |Enabled, tr02\-rtb\-sys |
      |Route learning |After enabling route learning, the TR route table (tr02\-rtb\-sys) automatically learns routes of the selected network instance, and generates entries with the destination as data center's CIDR blocks and the next hop as this attachment (attach\-ipsec01). |Enabled, tr02\-rtb\-sys |
      
   
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">After the VPN attachment is created, complete the VPN configuration on the server in the on\-premises data center, ensuring it is consistent with the IPsec\-VPN connection settings. For parameters, see <a href="https://docs.byteplus.com/en/docs/transitrouter/Best-Practices-02#.5pWw5o2u6KeE5YiS">Data planning</a>.</div>
   
   
   
   </Tab>
   <Tab zoneid="PzLHgHQZlc" title="Connect to the data center via DC">
   <TabTitle>Connect to the data center via DC</TabTitle>
   
   Configure the basic information, network instance, and routing information for the network instance attachment based on the table below.
   
   
   |**Parameter** |**Description** |**Example** |
   |---|---|---|
   |**Basic information** |||
   |TR |Defaults to the selected TR instance, requiring no manual configuration. |tr02 |
   |Regions |Defaults to the same region as the TR instance. No manual configuration required. |China (Beijing) |
   |Name |The name for the network instance attachment to be created. |attach\-dcg01 |
   |**Network Instances** |||
   |Attachment type |Select the type for the network instance attachment to be created. |Direct Connect Gateway |
   |Direct Connect Gateway |Select the DC Gateway instance to be connected. |dcg01 |
   |**Route configuration** |||
   |Association forwarding |If association forwarding is enabled, the traffic from the network instance will be forwarded based on the TR route table (tr02\-rtb\-sys). |Enabled, tr02\-rtb\-sys |
   |Route learning |After enabling route learning, the TR route table (tr02\-rtb\-sys) automatically learns routes of the selected network instance, and generates entries with the destination as data center's subnets and the next hop as this network instance attachment (attach\-dcg01). |Enabled, tr02\-rtb\-sys |
   
   
    
   
   
   </Tab>
   </Tabs>
   

3. View TR and VPC routes

   * The TR route table (tr02\-rtb\-sys) has learned the route entries pointing to the data center CIDR block from the DC or VPN.

      * When connecting the data center via DC, tr02\-rtb\-sys should have learned the routes listed in the table below.

         
         |Destination CIDR |Next Hop |Route status |Route type |Attachment type |Network Instances |Route attribute |
         |---|---|---|---|---|---|---|
         |172.16.0.0/24 |attach\-dcg01 |Available |Route learning |DC Gateway |dcg01 |49600 |
         

      * When connecting to the data center via VPN, tr02\-rtb\-set should have learned the routes listed in the table below.

         
         |Destination CIDR |Next Hop |Route status |Route type |Attachment type |Network Instances |Route attribute |
         |---|---|---|---|---|---|---|
         |172.16.0.0/24 |attach\-ipsec01 |Available |Route learning |IPsec\-VPN connection |ipsec01 |65000 |
         

   * Routes of vpc01 and vpc02 remain unchanged.


<span id="2lzCBNnx"></span>
### Step 3: Configure cross\-region bandwidth (Account A)

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The cross\-account, cross\-region bandwidth costs are billed to the user who creates the bandwidth package. Select the appropriate account based on your actual scenario. This example selects Account A.​</div>



1. Create a bandwidth package.

   Create a bandwidth package (named trbp01) to provide bandwidth resources for the inter\-region attachment. For procedure, see [Creating a TR bandwidth package](https://docs.byteplus.com/en/docs/transitrouter/TR-bandwidth-packages-01).

2. Create an inter\-region attachment.

   1. On the TR list page, click the name (tr01) of the target TR instance.

   2. In the section below **Basic information**, select the **Inter\-region attachment** tab.

   3. Click **Create inter\-region attachment** and configure the related parameters based on the table below.

      
      |Parameter |Description |Example |
      |---|---|---|
      |Name |Type the name for the inter\-region attachment. |attach\-tr |
      |Account type |Select based on the account ID of the peer TR. The peer TR instance to be connected in this example belongs to Account B. |Cross\-account |
      |Peer Account ID |In cross\-account scenarios, you must provide the account ID of the peer TR. |ID of account B |
      |Peer Region |Regions that require connectivity across regions. |China (Beijing) |
      |Instance |Select the TR instance in the peer region based on the project. |tr02 |
      |TR bandwidth package |Add to the created bandwidth package and allocate bandwidth. |Checked, trbp01, 2 Mbps |
      |Local associated route table |Enable associated forwarding to allow the local TR instance (tr01) to forward access traffic from inter\-region attachment according to tr01\-rtb\-set. |Enabled, tr01\-rtb\-set |
      |Remote TR association forwarding |Enable associated forwarding to allow the peer TR instance (tr02) to forward access traffic from the inter\-region attachment according to tr02\-rtb\-sys. |Enabled, tr02\-rtb\-sys |
      |Local TR route learning |Enable route learning to allow tr01\-rtb\-set automatically learn routes from the peer TR route table (tr02\-rtb\-sys) associated with forwarding. |Enabled, tr01\-rtb\-sys |
      |Remote TR route learning |Enable route learning to allow the specified TR route table (tr02\-rtb\-sys) to automatically learn routes from the local TR route table (tr01\-rtb\-set) associated with forwarding. |Enabled, tr02\-rtb\-sys |
      

   4. Click **Create** to complete the action.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">After creating the cross\-account inter\-region attachment, the status will be <strong>Pending peer acceptance</strong>. During this status, both the TR and VPC routes remain unchanged.      </div>
      

<span id="4Vxqmk46"></span>
## Step 4: Accept the cross\-account inter\-region attachment (Account B)


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name (tr02) of the target TR instance.

3. In the section below **Basic information**, select the **Inter\-region attachment** tab.

4. Click **Accept** to the right of the target cross\-account inter\-region attachment and confirm the resource information.

5. Click **Accept** to complete the action.

6. View TR and VPC routes

   * The TR route table (tr02\-rtb\-sys) has learned the routes as shown in the table below from the peer TR (tr01).

      
      |Destination CIDR |Next Hop |Route status |Route type |Attachment type |Network Instances |Route attribute |
      |---|---|---|---|---|---|---|
      |192.168.0.0/24 |attach\-tr01 |Available |Route learning |TR |tr01 |64512 |
      |192.168.16.0/24 |attach\-tr01 |Available |Route learning |TR |tr01 |64512 |
      

   * The routes in tr01\-rtb\-set remain unchanged.

   * The route entries learned by the TR route table (tr01\-rtb\-sys) vary depending on the type of network resources connected to the data center.

      * When connecting the data center via DC, tr01\-rtb\-set should have learned the routes listed in the table below.

         
         |Destination CIDR |Next Hop |Route status |Route type |Attachment type |Network Instances |Route attribute |
         |---|---|---|---|---|---|---|
         |172.16.0.0/24 |attach\-tr |Available |Route learning |TR |tr02 |64513,49600 |
         

      * When connecting to the data center via VPN, tr01\-rtb\-set should have learned the routes listed in the table below.

         
         |Destination CIDR |Next Hop |Route status |Route type |Attachment type |Network Instances |Route attribute |
         |---|---|---|---|---|---|---|
         |172.16.0.0/24 |attach\-tr |Available |Route learning |TR |tr02 |64513,65000 |
         

   * The system route tables of vpc01 and vpc02 have learned the routes to the data center's CIDR block from the TR, as shown in the table below.

      
      |Destination CIDR |Status |Next Hop type |Next Hop |
      |---|---|---|---|
      |172.16.0.0/24 |Available |TR |tr01 |
      


<span id="HwwHZ9Mi"></span>
### Result validation


1. Log in to the ECS instance in vpc01. For procedure, see [Logging on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging on to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Execute the `ping` command to connect to respective servers in vpc02 and the on\-premises data center, verifying that vpc01 communicates with the data center but not with vpc02.

3. Similarly, log in to the ECS instance in vpc02 and verify connectivity between vpc02 and the server in the data center.
