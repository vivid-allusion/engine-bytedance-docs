---
title: "Private network egress best practices"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Private-network-egress-best-practices"
---

<span id="L8VvQcoK"></span>
## Scenarios

By leveraging the private network egress, Claw instances can directly access cloud services or on\-premises data center services over the private network without traversing the public network, ensuring more secure and controllable access.

<span id="8gPrOMSD"></span>
## Data planning


* **ArkClaw**

   
   |Resource type |Resource name |CIDR block/IP address |Remark |
   |---|---|---|---|
   |VPC |The console does not display an explicit name for this VPC. In this topic, it is referred to as VPC\-arkClaw. |192.168.1.0/24 |It is specified upon ArkClaw Space activation and cannot be modified afterward. |
   

* **VPC for private network egress**

   You can reuse an existing Virtual Private Cloud (VPC), but we recommend creating a dedicated VPC for the private network egress to facilitate permission isolation and easier operations and maintenance.

   
   |Resource type |Resource name |CIDR block/IP address |Remark |
   |---|---|---|---|
   |VPC |VPC\-X |172.16.0.0/24 |The VPC specified for the private network egress. The subnet mask must be /28 or shorter​. Each subnet reserves 6 IP addresses​ for use by ArkClaw Enterprise. Reserve these addresses when planning your available IP range. |
   |Subnet |Subnet\-A |172.16.0.0/25 ||
   ||Subnet\-B |172.16.0.128/25 ||
   

* **Enterprise** ** services**

   * VPC services

      
      |Resource type |Resource name |CIDR block/IP address |Remark |
      |---|---|---|---|
      |VPC |VPC\-Service |172.16.1.0/24 |For hosting cloud\-based enterprise services. |
      |Subnet |Subnet\-Service |172.16.1.0/25 |The subnet where the ECS is located. |
      |ECS |ECS\-A |172.16.1.11 |For enterprise service deployment. |
      ||ECS\-B |172.16.1.22 |For enterprise service deployment. |
      ||ECS\-C |172.16.1.33 |For enterprise service deployment. |
      

   * On\-premises data center services

      
      |Resource type |Resource name |CIDR block/IP address |Remark |
      |---|---|---|---|
      |Data center |Unnamed |10.0.0.0/8 |\-\- |
      |Server |Server\-A |10.0.1.11 |For enterprise service deployment. |
      ||Server\-B |10.0.1.22 |For enterprise service deployment. |
      ||Server\-C |10.0.1.33 |For enterprise service deployment. |
      

* **Interconnection between VPC for private network egress and enterprise services​** 

   
   |Scenario |Communication mode |Description |
   |---|---|---|
   |Interconnect the VPC for private network egress with cloud VPCs |TR (recommended) |Suitable for complex networking scenarios. |
   ||CEN |Suitable for simple networking scenarios. |
   |Interconnect the VPC for private network egress with on\-premises data centers |CEN + DC |Suitable for scenarios with high bandwidth and simple networking. |
   ||TR + DC (recommended) |Suitable for scenarios with high bandwidth and complex networking. |
   ||TR + VPN |Suitable for scenarios requiring quick deployment. |
   


<span id="kZpni4v8"></span>
## Before you begin


* Follow the data planning outlined above to create the VPC, subnet, and Elastic Compute Service (ECS). For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC), [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet), and [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* Set up on\-premises data center services based on the data planning above.


<span id="fmPqBdum"></span>
## Procedure

<span id="rI8EuxdV"></span>
### Step 1: Create a VPC to associate with the private network egress


1. Log in to [the VPC console](https://console.byteplus.com/vpc/vpc).

2. Click "Create VPC **"** .

3. Select the root account to which the VPC belongs. Configure the basic information and CIDR block according to the table below.

   
   |**Parameter** |**Description** |**Sample value** |
   |---|---|---|
   |Region |Select the region where the VPC is located. Private networks are isolated across regions. We recommend selecting a region closer to your business to reduce latency. |China (Beijing) |
   |Name |Enter the name for the VPC. |vpc\-X |
   |IPv4 CIDR |Set the IPv4 CIDR block for the VPC. Modification is not supported after the VPC is created. |172.16.0.0/24 |
   |IPv6 CIDR |Specify whether to assign an IPv6 CIDR block to the VPC. |Disable |
   

4. Configure the subnet parameters according to the table below.

   
   |**Parameter** |**Description** |**Sample value** |**Sample value** |
   |---|---|---|---|
   |Availability zone |Select the availability zone where the subnet is located. Subnets within the same VPC can communicate with each other across availability zones (AZs) over the private network. Cross\-AZ deployment provides disaster recovery capability. Same\-AZ deployment reduces latency. |Availability Zone A |Availability Zone B |
   |Name |Enter the name of the subnet. |subnet\-A |subnet\-B |
   |IPv4 CIDR |Set the subnet's CIDR block.<br><br><br>* The CIDR block must fall within the VPC range and must not overlap with other subnets.<br><br>* The first two IPs and the last IP of each subnet are reserved by the system​ (used as the network address, gateway, and broadcast address, respectively).<br><br>* The private network egress occupies 6 IP addresses. The CIDR block cannot be modified after the subnet is created. |172.16.0.0/25 |172.16.0.128/25 |
   

   Click "+Add Subnet **"**  to create more than one subnet at the same time.

5. Click "Create **"**  to complete configuration.


<span id="jQJPuOH9"></span>
### Step 2: Activate the space

Activate the space using one of the methods described in the [Quick Start for Space activation](https://docs.byteplus.com/en/docs/ArkClaw/Quick_start_guide).

<span id="lFvdPHJI"></span>
### Step 3: Configure private network egress


1. Log in to the [ArkClaw Enterprise Edition console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. On the Network Configuration page, click the "Configuration" tab.

4. Click "Edit" to the right of "Private network egress."

5. In the Private network egress section, configure the private network information based on the table below.

   
   |Configuration item |Description |**Sample value** |
   |---|---|---|
   |Configure private network egress |Specify whether to enable private network egress.<br><br><br>* After enabling the private network egress, ArkClaw instances communicate with enterprise services over the private network, ensuring more secure and controllable access.<br><br>* If disabled, no additional parameters need to be configured. |Enable |
   |**Basic information** |||
   |VPC |Select the VPC created in Step 1. |VPC\-X |
   |Availability zone and subnet |Select the two availability zones and subnets to which the private network egress belongs. Subnets are used to allocate private IP addresses for the private network egress. Private network egress will occupy 6 private IP addresses in each subnet to ensure access performance. |* Availability Zone A, Subnet\-A, 172.16.0.0/25<br><br>* Availability Zone B, Subnet\-B, 172.16.0.128/25 |
   |Security group |Select the security group associated with the private network egress. You can configure up to 4 groups simultaneously.<br><br><br>* Only outbound security group rules take effect for the private network egress.<br><br>* When private network egress instances are deployed across two availability zones, they share the same security group configuration. For more information, see [Security group overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview). |Default |
   |**Specify access destination** |||
   |Specify destination IP range |Enter the IP address or CIDR block where your enterprise services are located.<br><br><br>* The specified addresses or blocks must not fall within the following ranges: `100.64.0.0/10`, `224.0.0.0/4`, `127.0.0.0/8`, `0.0.0.0/0`, `240.0.0.0/4`, `192.18.0.0/15`, `33.0.0.0/8`, `66.0.0.0/8`, `9.0.0.0/8`, and `169.254.0.0/16`.<br><br>* You can specify up to 50 entries at a time. Separate multiple addresses or blocks with commas (,).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">To meet internal security/compliance policies or for the ArkClaw scientific internet access scenario, set the destination IP range to the following CIDR blocks for steering traffic.</div><br><br><br><div data-tips="true" data-tips-type="default"><code>1.0.0.0/8</code><code>, </code><code>2.0.0.0/7</code>, <code>4.0.0.0/6</code>, <code>8.0.0.0/5</code>, <code>16.0.0.0/4</code>, <code>32.0.0.0/3</code>, <code>64.0.0.0/2</code>, and <code>128.0.0.0/1</code></div><br><br><br> |172.16.1.0/24, 10.0.0.0/8 |
   

6. Click "OK" to complete the action.


<span id="BEGO3lnF"></span>
### Step 4: Interconnect the VPC for private network egress with enterprise services​


* **Interconnect the VPC for private network egress with ** **cloud** ** VPCs**

   * **Transit Router (TR)**  ** (recommended)** 

      * [Implementing private interconnectivity and isolation between different VPCs (same account, same region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-02)

      * [Implement private connectivity and segmentation between VPCs (same account, cross-region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-03)

      * [Implement private connectivity and segmentation between VPCs (cross-account, same region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-04)

      * [Implement private connectivity and segmentation between VPCs (cross-account, cross-region)](https://docs.byteplus.com/en/docs/transitrouter/Connecting-and-isolating-different-VPCs-across-accounts-and-Regions)

   * **Cloud Enterprise Network (CEN)** 

      * [Virtual Private Cloud interconnection (same account and same region)](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-within-the-same-account-and-Region-01)

      * [Virtual Private Cloud interconnection (same account, cross-region)](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-within-the-same-account-01)

      * [Virtual Private Cloud interconnection (cross-account, same region)](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-accounts-within-the-same-Region)

      * [Virtual Private Cloud interconnection (cross-account and cross-region)](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-and-accounts)

* **Interconnect the VPC for private network egress with on\-premises data centers**

   * **VPN + TR**

      For procedure, see [IPsec-VPN connection via Transit Router](https://docs.byteplus.com/en/docs/vpn/Creating_a_Customer_Gateway).

   * **Direct Connect (DC) + TR (recommended)** 

      * Same account & same region: [Achieving interconnectivity and isolation between VPCs and an on-premises data center](https://docs.byteplus.com/en/docs/6979/1127486)

      * Cross\-region: [Implementing interconnectivity between independent VPCs and a data center (same account, cross-region)](https://docs.byteplus.com/en/docs/transitrouter/Best-Practices-02?lang=en)

      * Cross\-account: [Implementing interconnectivity between independent VPCs and a data center (cross-account, same region)](https://docs.byteplus.com/en/docs/transitrouter/Interconnectivity-between-VPCs-and-idc-cross-account-sameregion?lang=en)

      * Cross\-account & cross\-region: [Implementing interconnectivity between independent VPCs and a data center (cross-account, cross-region)](https://docs.byteplus.com/en/docs/transitrouter/Interconnectivity-between-VPCs-and-idc-cross-account-interregion?lang=en)

   * **DC + ** **CEN**

      * [Interconnectivity between multiple VPCs and multiple on-premises data centers (same account, same region)](https://docs.byteplus.com/en/docs/cen/Connecting-a-virtual-private-cloud-to-multiple-data-centers-Same-Account-and-Same-Region)

      * [Interconnectivity between multiple VPCs and multiple on-premises data centers (same account, cross-region)](https://docs.byteplus.com/en/docs/cen/Connecting-multiple-VPCs-and-multiple-data-centers-same-account-across-Regions)

      * [Interconnection between multiple VPCs in the cloud and multiple on-premises data centers (Cross-account, same region)](https://docs.byteplus.com/en/docs/cen/Interconnection-between-multiple-VPCs-and-multiple-data-centers-Cross-account-same-region)

      * [Interconnection between multiple VPCs in the cloud and multiple on-premises data centers (Cross-account, cross-region)](https://docs.byteplus.com/en/docs/cen/Interconnection-between-multiple-VPCs-and-multiple-data-centers-Cross-account-cross-region)


<span id="oCUA24RQ"></span>
## Verification: Test connectivity


1. Log in to the [ArkClaw Enterprise Edition console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Claws".

3. In the "Instances \> Employee Claw" tab, click "More \> Terminal" to the right of the target employee.

4. Execute the ` ping <server IP address, e.g., 172.16.1.11> `command in the command line to verify that you can access the enterprise service server's IP address.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b9414542f644c2d7590138dcf0ba961a.png) </span>


&nbsp;
