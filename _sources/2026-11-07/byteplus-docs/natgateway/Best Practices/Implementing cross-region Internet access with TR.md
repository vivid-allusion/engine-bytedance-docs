---
title: "Implementing cross-region Internet access with TR"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Implement-cross-domain-Access-to-Internet-with-Transit-Router"
---

This topic describes how to enable cross\-region Internet access through the Internet NAT Gateway and Transit Router (TR).

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

If your business requires Internet access between a domestic on\-premises data center and business in other regions, you can use the networking solution in this topic for smooth networking.

> In the figure below, region A and region B are used as examples; you can select the actual business regions as needed.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_82fa402391fbd692754cb60a1682b13c.png) </span>

<span id=".5pWw5o2u6KeE5YiS"></span>
## Data planning

Before configuration, plan the CIDR blocks, routes, and other data parameters for each network resource in the diagram as shown below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ee58138f73df8a6b9ec15c9f889a4199.png) </span>


* On\-premises data center

   
   |Region |CIDR block |Server information |||
   |---|---|---|---|---|
   |||Name |Private IP address |Public IP address |
   |Region A |172.16.0.0/24 |server01 |172.16.0.10 |101.XX.XX.10 |
   

* Direct Connect

   
   |Region |DC Gateway |DC Connection |Name of the DC Virtual interface |Cloud/Your gateway peer IP |Route details |||
   |---|---|---|---|---|---|---|---|
   ||||||Topic |BGP ASN |BGP key |
   |Region A |dcg01 |DAS123_port308_conn |vif01 |* Cloud: 10.0.0.1/30<br><br>* Your: 10.0.0.2/30 |BGP |49600 |E0g5\*\*\*\*8go1 |
   

* Transit Router

   The route planning is illustrated above. For details, see [TR Route configuration planning](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-02).

* Virtual Private Cloud

   
   |Region |VPC |VPC CIDR block |Subnet details |||
   |---|---|---|---|---|---|
   ||||Subnet name |Available zone |Subnet CIDR block |
   |Region B |vpc01 |192.168.0.0/20 |subnet01 |Availability zone A |192.168.0.0/24 |
   

* NAT Gateway

   
   |Region |VPC |Subnet |Elastic IP Address |
   |---|---|---|---|
   |Region B |vpc01 |subnet01 |* eip01: 101.XX.XX.10<br><br>* eip02: 101.XX.XX.11 |
   


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created necessary VPCs and their subnets. For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* You have connected the on\-premises data center to the cloud through Direct Connect, including configurations on both the Direct Connect side and private routing on the on\-premises data center side. For detailed steps, see the first three steps in [Configure a DC connection](https://docs.byteplus.com/en/docs/directconnect/Quick-start#.6YWN572u5LiT57q_6L-e5o6l) and [Configure on-premises routing](https://docs.byteplus.com/en/docs/directconnect/Configuring-a-local-route-and-testing-connectivity#.6YWN572u5pys5Zyw6Lev55Sx), respectively.

* You have applied for 2 public IPs within region B. For detailed steps, see [Applying for an EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).

* You have obtained the IP address of the server in the data center and ensured the server is properly operational.

* If you want to use the Chinese mainland–Asia Pacific bandwidth package, ensure you have completed the cross\-border business permission application. For detailed steps, see [Cross-border application](https://docs.byteplus.com/en/docs/6405/79179).


<span id=".6YWN572u5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5Lit6L2s6Lev55Sx5Zmo"></span>
### Step 1: Configure TR


1. Configure the TR in region A.

   1. Follow the procedure in [Creating a Transit Router instance](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01) to create a TR instance.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The system automatically creates a system route table simultaneously. This article uses tr01\-rtb\-sys as an example.      </div>
      

   2. Follow the procedure in [Creating a DC Gateway attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-dc) to create a network instance attachment, connecting the cloud\-linked on\-premises data center.

      * Enable associated forwarding and route learning when creating the attachment.

      * After creating the attachment, view the TR route table to confirm the on\-premises data center route has been learned.

2. Configure the TR in region B.

   1. Follow the procedure in [Creating a Transit Router instance](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01) to create a TR instance.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The system automatically creates a system route table simultaneously. This article uses tr02\-rtb\-sys as an example.      </div>
      

   2. See [Creating a VPC attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpc) to create a network instance attachment that connects the private network in region B.

      * When creating the attachment, associated forwarding, route learning, and route synchronization are all enabled.

      * After creating the attachment, check the TR route table to confirm the VPC routes are learned, and check the VPC route table to confirm the TR routes are learned.

3. Configure inter\-region bandwidth

   1. See [Creating a bandwidth package](https://docs.byteplus.com/en/docs/transitrouter/TR-bandwidth-packages-01) to create a bandwidth package.

   2. See [Creating an inter-region attachment](https://docs.byteplus.com/en/docs/transitrouter/Inter-region-peering-attachments-01) to create an attachment connecting the cloud IDC connected by tr01 and the cloud VPC connected by tr02.

      * When creating the attachment, select the bandwidth package created in the previous step, and enable associated forwarding and route learning.

      * After creating the attachment, check the TR route tables of both regions to confirm the routes from the peer TR are learned.


<span id=".5q2l6aqk5LqM77ya6YWN572u5YWs572RTkFU572R5YWz"></span>
### Step 2: Configure Internet NAT gateway

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If only the on\-premises data center needs accelerated access to cross\-region services, configure only the SNAT rules of the Internet NAT gateway.</div>


* <div data-tips="true" data-tips-type="tip">If only cross\-region internet clients need to access domestic services, configure only the DNAT rules of the internet NAT gateway.</div>


1. See [Create NAT Gateway](https://docs.byteplus.com/en/docs/natgateway/Creating-an-Internet-NAT-gateway) to create an internet NAT gateway and automatically configure the SNAT rules.

   * When configuring SNAT rules, select **Auto configuration** for configuration mode and choose **101.XX.XX.10 | eip01** as the public IP.

   * If SNAT rules are not required, select **manual configuration** for configuration mode.

2. See Associating Elastic IP to associate eip02 with the NAT gateway.

3. See Creating DNAT entries to configure a DNAT entry, allowing cross\-region internet clients to access IDC services through the NAT gateway. The following table describes the configuration parameters of the DNAT rules.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Name |Customize the rule name as needed. |dnat |
   |Protocol |Select protocol type. The SSH remote login service used in this topic only supports the TCP protocol. |TCP |
   |Private IP |Enter the private IP address and service port of the server in the data center. |172.16.0.10, 80 |
   |EIP |Select the public IP bound to the Internet NAT Gateway and its port receiving requests from the internet.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">DNAT and SNAT entries linked to the same public IP may cause service contention. To configure both SNAT and DNAT entries simultaneously, use different public IPs for each.</div><br> |101.XX.XX.11 \| eip02, 80 |
   


<span id=".5q2l6aqk5LiJ77ya6YWN572uVFLovazlj5HlhaznvZHmtYHph4_nmoTot6_nlLE="></span>
### Step 3: Configure routing on the TR to forward internet traffic

See [Create a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05#.5Yib5bu66Z2Z5oCB6Lev55Sx) to add route entries to the TR route table tr02\-rtb\-sys, forwarding internet traffic to the local Virtual Private Cloud. Route entries are shown in the table below.


|Route name |Destination CIDR |Blackhole route |Next Hop type |Next Hop |
|---|---|---|---|---|
|Internet traffic forwarding |0.0.0.0/0 |None |Network instance attachment |attach\-vpc01 |


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation

<span id=".6aqM6K-BSURD5Lit5pyN5Yqh5Zmo5Y-v5q2j5bi46K6_6Zeu55uu5qCH572R57uc"></span>
### Verify that the server in the data center can access the target network normally


1. Log in to the server in the data center.

2. Execute the command `ping 8.8.8.8` to verify connectivity.

   If the return result appears as shown below, the network is reachable.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_345e65aa1d7c85ac73fc0903b5cb0a3b.png) </span>


<span id=".6aqM6K-B6Leo5Z-f5YWs572R5a6i5oi356uv5Y-v5q2j5bi46K6_6ZeuSURD5YaF5Lia5Yqh"></span>
### Verify that clients from across domains on the internet can normally access services within the data center


1. Log in to any internet client across domains.

2. Execute the command `ssh <EIP configured in DNAT rule> -p <EIP port configured in DNAT rule>` to verify connectivity.

   The network is reachable if the login page can be accessed normally.
