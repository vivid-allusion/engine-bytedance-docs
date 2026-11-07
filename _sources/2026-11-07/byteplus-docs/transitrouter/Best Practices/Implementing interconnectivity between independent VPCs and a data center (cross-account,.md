---
title: "Implementing interconnectivity between independent VPCs and a data center (cross-account, same region)"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Interconnectivity-between-VPCs-and-idc-cross-account-sameregion"
---

This topic describes how to configure Transit Router (TR) for cross\-account connectivity in the same region, allowing different Virtual Private Clouds (VPCs) to access the same on\-premises data center while remaining isolated from each other.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

A company has deployed two VPCs in Region A. Both VPCs need to share the VPN Connect or Direct Connect (DC) resources owned by another account to access an on\-premises data center. The two VPCs themselves must remain isolated from each other. This scenario can be implemented using TR, as illustrated in the following diagram.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_054fc04f4184054a4afebe1122060790.png) </span>

<span id=".5pWw5o2u6KeE5YiS"></span>
## Data planning


* Select a region that is closest to the geographical location of the data center for VPN or DC. This example selects China (Beijing).

* Before configuration, plan the CIDR blocks, routes, and other parameters for the network resources shown in the topology diagram.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Routes in the VPC route tables illustrated below can be manually configured or automatically synchronized. This example uses auto publishing.</div>


&nbsp;

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9199c5e84b7a48519708fab9c3d9f4e1.png) </span>


* Virtual Private Cloud

   
   |Region |Account |Resource type |VPC CIDR block |CIDR block |Subnet information |
   |---|---|---|---|---|---|
   |China (Beijing) |Account A |VPC |vpc01 |192.168.0.0/20 |\-\- |
   ||||vpc02 |192.168.16.0/20 |\-\- |
   |||Subnet |subnet01 |192.168.0.0/24 |* Affiliated availability zone: Availability Zone A<br><br>* ECS private IP: 192.168.0.10 |
   ||||subnet02 |192.168.16.0/24 |* Availability zone: Availability Zone A<br><br>* ECS private IP: 192.168.16.10 |
   

* VPN Connect

   
   |Region |Account |Resource type |Resource name |IP address/CIDR block |Routing information |
   |---|---|---|---|---|---|
   |China (Beijing) |Account B |IPsec\-VPN connection |ipsec01 |* Tunnel CIDR block: 169.254.1.0/30<br><br>   * Local Tunnel IP: 169.254.1.1<br><br>   * Peer Tunnel IP: 169.254.1.2<br><br>* Pre\-shared key: test@123 |\-\- |
   |||Customer Gateway |cgw01 |IP address: 12.XX.XX.10<br><br>> This IP address is the public IP address of a server in the on\-premises data center. |BGP ASN: 65000 |
   

* Direct Connect

   
   |Region |Account |Resource type |Resource name |Interconnection information (IPv4) |Routing information |
   |---|---|---|---|---|---|
   |China (Beijing) |Account B |DC Connection |DAS123_port308_conn |\-\- |\-\- |
   |||DC Gateway |dcg01 |\-\- |\-\- |
   |||Virtual Interface |vif01 |* Cloud gateway IP: 10.0.0.1/30​​<br><br>* Your gateway IP: 10.0.0.2/30​​ |* Route type: BGP<br><br>* BGP ASN: 49600<br><br>* BGP key: E0g5\*\*\*\*8go1 |
   

* Transit Router

   For detailed route planning, see [TR Route configuration planning](https://docs.byteplus.com/docs/transitrouter/Route-tables-02).

   
   |Region |Account |Resource type |Resource name |Routing information |
   |---|---|---|---|---|
   |China (Beijing) |Account A |TR instance |tr01 |ASN: 64512 |
   |||Intra\-region VPC attachment |* attach\-vpc01<br><br>* attach\-vpc02 |* Association forwarding: tr01\-rtb\-sys<br><br>* Route learning: tr01\-rtb\-set<br><br>* Auto publishing: On |
   |||Intra\-region VPN attachment |attach\-ipsec01 |* Association forwarding: tr01\-rtb\-set<br><br>* Route learning: tr01\-rtb\-sys |
   |||Intra\-region DC Gateway attachment |attach\-dcg01 |* Association forwarding: tr01\-rtb\-set<br><br>* Route learning: tr01\-rtb\-sys |
   |||TR route table |* tr01\-rtb\-sys<br><br>* tr01\-rtb\-set |\-\- |
   

* Data center

   
   |Subnet |Server name |Private IP address |EIP |
   |---|---|---|---|
   |172.16.0.0/24 |server01 |172.16.0.10 |12.XX.XX.10 |
   


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created necessary VPCs and their subnets. For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* You have created Elastic Compute Service (ECS) instances in the VPCs. For procedure, see [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* You have completed the following configuration based on the service type connecting to the on\-premises data center. For parameters, see [Data planning](https://docs.byteplus.com/docs/transitrouter/Best-Practices-02#.5pWw5o2u6KeE5YiS).

   * **VPN**: See [Creating a Customer Gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway1) and create a customer gateway (named cgw01) required for this scenario.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The IPsec\-VPN connection in this example uses dynamic routing, ensuring that your customer gateway supports BGP and that valid ASNs have been configured for associated resources and the customer gateway.      </div>
      

   * **DC**: Follow the first three steps in [Configuring a DC Connection](https://docs.byteplus.com/en/docs/directconnect/Quick-start#.6YWN572u5LiT57q_6L-e5o6l) to create a DC Connection, DC Gateway, and DC Virtual Interface, and then complete private route configuration in the on\-premises data center by seeing [Configuring on-premises routing](https://docs.byteplus.com/en/docs/directconnect/Configuring-a-local-route-and-testing-connectivity#.6YWN572u5pys5Zyw6Lev55Sx).

* You have obtained the IP address of the server in the data center and ensured the server is properly operational.

* You have enabled the resource sharing feature to proactively share TR capabilities. If not enabled, please contact your account manager.


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedures

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This example only covers required parameters. Leave other parameters at their default values.</div>


<span id=".5q2l6aqk5LiA77ya6YWN572u5Y2O5Y2XMe-8iOW5v-W3nu-8ieWcsOWfn-S4reeahFRS5a6e5L6L"></span>
### Step 1: Configure a TR instance (Account A)


1. [Create a TR instance](http://volcengine.com/docs/6979/2116745?lang=zh&TagIDs=2%2C105%2C104%2C95%2C94): Create a TR instance to host the TR service.

   
   |Parameters |Description |Example |
   |---|---|---|
   |Region |Select a region closer to your service for shorter network delays and faster access. |China (Beijing) |
   |Name |Type a name for easy identification. |tr01 |
   |ASN |An Autonomous System (AS) is a network unit on the internet with a unified routing policy, composed of one or more networks and identified by a unique Autonomous System Number (ASN). Specify a private ASN for the TR instance from the range of 64512–65534 or 4200000000–4294967294.<br><br>After being assigned with an ASN, the TR automatically prepends the ASN to the AsPath attribute of routes published from it to other network instances. |64512 |
   |Agreement |Follow the console guidance to review and accept Legal. |Check |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When you create a TR instance, the system automatically creates a system route table for it (e.g., named tr01\-rtb\-sys). In this example, this system route table is used to forward traffic from vpc01 and vpc02.​   </div>
   

2. [Create a TR custom route table](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-03?lang=zh): Create a custom route table (named tr01\-rtb\-set) for tr01 to forward traffic from the cross\-account VPN/DC.

3. [Create a VPC attachment and configure routing](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpc?lang=zh): Create two VPC attachments (named attach\-vpc01 and attach\-vpc02) for tr01, respectively connecting to VPC instances (vpc01 and vpc02).

   
   |Parameters |Description |Example<br><br>(Attach vpc01) |Example<br><br>(Attach vpc02) |
   |---|---|---|---|
   |Name |Type a name for easy identification. |attach\-vpc01 |attach\-vpc02 |
   |Attachment type |Select the type for the network instance attachment to be created. |VPC |VPC |
   |VPC |Select the VPC instance to be connected. |vpc01 |vpc02 |
   |Availability Zone and Subnet |Select the entry point where TR connects to the VPC. Select the availability zone and then the subnet, and set the selected availability zone as the default availability zone. |Availability Zone A; subnet01 |Availability Zone A;subnet02 |
   |Association forwarding |The TR will forward traffic from the related network instance based on the route table associated with this network instance attachment.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Take attach\-vpc01 as an example. After enabling association forwarding, the TR forwards traffic from vpc01 based on tr01\-rtb\-set.</div><br> |Enabled; tr01\-rtb\-sys |Enabled; tr01\-rtb\-sys |
   |Route learning |After enabling route learning, the TR route table will automatically learn routes of the network instance, and generate entries with the destination as VPC subnets and the next hop as this network instance attachment.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Take attach\-vpc01 as an example. After enabling route learning, the TR route table (tr01\-rtb\-sys) automatically generates routes whose destinations are vpc01 subnets and the next hop is attach\-vpc01. That is, routes pointing to vpc01 are configured in tr01\-rtb\-set.</div><br> |Enabled; tr01\-rtb\-set |Enabled; tr01\-rtb\-set |
   |Auto Publish Route |Enabling auto publishing will automatically synchronize routes from the associated TR route table to all route tables within the selected VPC. These synchronized routes are marked as system routes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Take attach\-vpc01 as an example. After enabling auto publishing, the system automatically synchronizes the routes from tr01\-rtb\-set to all route tables within vpc01. These synchronized routes are system routes. That is, routes pointing to the TR are configured in the vpc01 route tables.</div><br> |Enable |Enable |
   

4. View TR and VPC routes

   * tr01\-rtb\-sys contains no entries, while the routes in tr01\-rtb\-set are listed below.

      
      |Destination CIDR |Next Hop |Status |Route type |Connection type |Network instance |Route attributes |
      |---|---|---|---|---|---|---|
      |192.168.0.0/24 |attach\-vpc01 |Available |Automatic learning |VPC |vpc01 |\- |
      |192.168.16.0/24 |attach\-vpc02 |Available |Automatic learning |VPC |vpc02 |\- |
      

   * Since the routes in tr01\-rtb\-sys are automatically published to the vpc01 and vpc02 route tables, routes in the vpc01 and vpc02 route tables are unchanged.


<span id=".5q2l6aqk5LqM77ya6YWN572u5Y2O5YyXMu-8iOWMl-S6rO-8ieWcsOWfn-S4reeahFRS5a6e5L6L"></span>
### Step 2: Initiate cross\-account TR sharing (Account A)


1. Log in to [the Resource management console](https://console.byteplus.com/resourcemanager/region:resource-manager+cn-beijing/resource_share/owned).

2. Click **Create shared unit** and configure the basic information based on the table below.

   
   |Parameters |Description |Example |
   |---|---|---|
   |Unit name |Type in a name for the shared unit. |Shared TR |
   |Region |Region defaults to the region selected in the top menu bar. To modify, reselect the region in the top menu bar. |China (Beijing) |
   |product |Select the Transit Router \- TR instance. |Transit Router \- TR instance. |
   |Resource ID |Type in the ID of the TR to be shared, then search and check it. |Check the target TR |
   

3. Click **Next** to associate sharing permissions.

   TR sharing permissions are system\-defined and cannot be modified. For default supported actions, see [Instructions](https://docs.byteplus.com/docs/transitrouter/Cross-account-Sharing-overview#T39M302D).

4. Click **Next** to associate shared users.

   
   |Parameters |Description |Example |
   |---|---|---|
   |Resource user |Choose a method for resource sharing.<br><br><br>* **Allow sharing with any account**: Share the TR with any BytePlus root account.<br><br>* **Only allow sharing with enterprises and organizations**: Share the TR only with BytePlus root accounts in the same enterprise organization. |Allow sharing with any account |
   |User type |Select the root account. |main account |
   |User ID |Type the ID of Account B. |2100\*\*\*\*25 |
   

5. Click **Add** to specify resource users.

6. Click **Next** to confirm that the resources, associated permissions, and shared users are correct.

7. Click **Confirm** to complete the action.


<span id=".5q2l6aqk5LqM77ya6YWN572u5Y2O5YyXMu-8iOWMl-S6rO-8ieWcsOWfn-S4reeahFRS5a6e5L6L"></span>
### Step 3: Configure a cross\-account network instance attachment (Account B)


1. Accept a sharing invitation.

   1. Log in to [the Resource management console](https://console.byteplus.com/resourcemanager/region:resource-manager+cn-beijing/resource_share/shared).

   2. In the top menu bar, select the region to which the shared TR belongs.

   3. Click **Accept** on the right of the shared unit to complete the action.

2. Create a cross\-account network instance attachment: Create the appropriate network instance attachment based on the resource type connecting the data center. For procedure, see [Creating a VPN attachment](https://docs.byteplus.com/docs/transitrouter/Attachments-vpn) or [Creating a DC Gateway attachment](https://docs.byteplus.com/docs/transitrouter/Attachments-dc).

   
   <Tabs>
   <Tab zoneid="pGn5lyEDDM" title="Connect to the data center via VPN">
   <TabTitle>Connect to the data center via VPN</TabTitle>
   
   * Basic configuration
   
      
      |**Parameter** |**Description** |**Example** |
      |---|---|---|
      |TR |Defaults to the selected TR instance, requiring no manual configuration. |tr01 |
      |Region |Defaults to the same region as the TR instance. No manual configuration required. |China (Beijing) |
      |Fee payer |Defaults to the same fee payer as the TR instance. No manual configuration required. |Network instance account |
      |Name |Type a name for easy identification. |attach\-ipsec01 |
      |Attachment type |Select VPN and create a new IPsec\-VPN connection. |VPN |
      |IPsec name |Type the name for the IPsec\-VPN connection to be created. |ipsec01 |
      |Specification |Bandwidth caps vary by specification. The **default** specification has a bandwidth cap of 200 Mbps.​ For higher bandwidth, see [Creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1) to adapt. |default |
      |Routing |Select routing mode. |Destination routing |
      |Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration. |Yes |
      |Route propagation mode |Select the route propagation mode for the IPsec\-VPN connection.<br><br><br>* Dynamic routing: No manual configuration is required for the TR routes after the VPN attachment is created.<br><br>* Static routing: After the VPN attachment is created successfully, manually configure routes on the TR side (setting the destination CIDR block to the data center CIDR block, and the next hop to this VPN attachment). For procedure, see [Create a static route](https://docs.byteplus.com/docs/transitrouter/Route-tables-05#.5Yib5bu66Z2Z5oCB6Lev55Sx). |Dynamic routing |
      |Customer Gateway |Select an existing customer gateway. |cgw01 |
      |Tunnel CIDR block |The CIDR block where the local and peer tunnel IPs reside. |169.254.1.0/30 |
      |Local Tunnel IP |Configure the BGP address on the BytePlus VPN service. |169.254.1.1 |
      |Peer Tunnel IP |Configure the BGP address on the customer gateway device. |169.254.1.2 |
      |Pre\-shared key |Type the key used for IKE negotiation between both VPN devices. |test@123 |
      |Confirm key |Type the Pre\-Shared Key again. |test@123 |
      |Zone |Select the availability zone for VPN. |AZ\-A |
      
   
   * Route configuration
   
      
      |**Parameters** |**Description** |**Example** |
      |---|---|---|
      |Association forwarding |This example uses the TR route table (tr01\-rtb\-set) to forward traffic from the data center. Enabling association forwarding will result traffic being forwarded via tr01\-rtb\-sys. Therefore, association forwarding is disabled. |Disable |
      |Route learning |After enabling route learning, the TR system route table (tr01\-rtb\-sys) automatically learns routes of the selected network instance, and generates entries with the destination as data center's CIDR blocks and the next hop as this network instance attachment (attach\-ipsec01). |Enable |
      
   
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">After the VPN attachment is created, complete the VPN configuration on the server in the on\-premises data center, ensuring it is consistent with the IPsec\-VPN connection settings. For parameters, see <a href="https://docs.byteplus.com/docs/transitrouter/Best-Practices-02#.5pWw5o2u6KeE5YiS">Data planning</a>.</div>
   
   
   OP
   
   
   </Tab>
   <Tab zoneid="SKMhZIZhrL" title="Connect to the data center via DC">
   <TabTitle>Connect to the data center via DC</TabTitle>
   
   Configure the basic information, network instance, and routing information for the network instance attachment based on the table below.
   
   
   |**Parameter** |**Description** |**Example** |
   |---|---|---|
   |**Basic information** |||
   |TR |Defaults to the selected TR instance, requiring no manual configuration. |tr01 |
   |Region |Default to the same region as the TR instance. No manual configuration required. |China (Beijing) |
   |Fee payer |Default to the same fee payer as the TR instance. No manual configuration required. |Network instance account |
   |Name |Type a name for easy identification. |attach\-dcg01 |
   |**Network instance** |||
   |Attachment type |Select the type for the network instance attachment to be created. |DC Gateway |
   |DC Gateway |Select the DC Gateway instance to be connected. |dcg01 |
   |**Route configuration** |||
   |Association forwarding |This example uses the TR route table (tr01\-rtb\-set) to forward traffic from the data center. Enabling association forwarding will result traffic being forwarded via tr01\-rtb\-sys. Therefore, association forwarding is disabled. |Disable |
   |Route learning |After enabling route learning, the TR system route table (tr01\-rtb\-sys) automatically learns routes of the selected network instance, and generates entries with the destination as data center's subnets and the next hop as this network instance attachment (attach\-dcg01). |Enable |
   
   
   
   
   
   </Tab>
   </Tabs>
   


<span id="qRBFWReo"></span>
## Step 4: Create association forwarding (Account A)


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name (tr01) of the target TR instance.

3. In the zone below **Basic information**, select the **Route Table** tab.

4. Select the target route table (tr01\-rtb\-set) and click the **Associated forwarding** tab.

5. Click **Create association forwarding** and complete the configuration based on the table below.

   * **Attachment type**: Select the intra\-region attachment.

   * **Network instance attachment**: Select based on the type of cloud resource that connects to your on\-premises data center.

      * Select attach\-ipsec01 when connecting to the on\-premises data center via VPN.

      * Select attach\-dcg01 when connecting to the on\-premises data center via DC.

6. Click **Create**.

7. View TR and VPC routes

   * The TR route table (tr01\-rtb\-sys) has learned the route entries pointing to the data center CIDR block from the DC or VPN.

      * When the data center is connected via DC, tr01\-rtb\-sys should have learned the routes listed in the table below.

         
         |Destination CIDR |Next Hop |Status |Route type |Connection type |Network instance |Route attributes |
         |---|---|---|---|---|---|---|
         |172.16.0.0/24 |attach\-dcg01 |Available |Automatic learning |DC Gateway |dcg01 |49600 |
         

      * When connecting the data center via VPN, tr01\-rtb\-sys should have learned the routes listed in the table below.

         
         |Destination CIDR |Next Hop |Status |Route type |Connection type |Network instance |Route attributes |
         |---|---|---|---|---|---|---|
         |172.16.0.0/24 |attach\-ipsec01 |Available |Automatic learning |VPN |ipsec01 |65000 |
         

   * The route tables of vpc01 and vpc02 have learned the routes to the data center's CIDR block from the TR, as shown in the table below.

      
      |Destination CIDR |Status |Next Hop type |Next Hop |
      |---|---|---|---|
      |172.16.0.0/24 |Available |TR |tr01 |
      


<span id="1h2gS7ym"></span>
### 

<span id=".5q2l6aqk5LiJ77ya6YWN572u6Leo5Zyw5Z-f5bim5a69"></span>
### Result validation


1. Log in to the ECS instance in vpc01. For procedure, see [Logging on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging on to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Execute the `ping` command to connect to respective servers in vpc02 and the on\-premises data center, verifying that vpc01 communicates with the data center but not with vpc02.

3. Similarly, log in to the ECS instance in vpc02 and verify connectivity between vpc02 and the server in the data center.
