---
title: "Interconnectivity between multiple VPCs and multiple on-premises data centers (same account, same region)"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Connecting-a-virtual-private-cloud-to-multiple-data-centers-Same-Account-and-Same-Region"
---

This topic explains how to enable mutual access between multiple Virtual Private Clouds (VPC) and on\-premises data centers under the same account and region.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The interconnectivity feature between multiple data centers is currently in beta stage. If you need a trial, please contact your account manager.</div>


<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

By default, different VPCs are logically isolated from each other, and VPCs cannot directly access resources over Direct Connect connections. Through Cloud Enterprise Network (CEN), network interconnection between VPC and Direct Connect can be realized, thereby enabling interconnected communication between a cloud network and a data center connected via Direct Connect.

This topic explains how to achieve interconnection between multiple VPCs in the cloud and multiple on\-premises data centers through Cloud Enterprise Network (CEN), as illustrated in the diagram below.

> The diagram displays sample configurations for each service. Modify these values according to your actual network architecture during implementation.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a9e110d6553327d2654942577269c8ad.png) </span>

All resources in the diagram above are located in the China (Beijing) region. Other data annotations in the diagram are explained below:


* vpc\-1: The subnet CIDR block is `192.168.1.0/24`, and the private IP address of Elastic Compute Service (ECS) ecs\-1 is `192.168.1.10`

* Private Network vpc\-2: The CIDR block of the subnet is `192.168.2.0/24`, and the private IP address of ecs\-2 is `192.168.2.10`

* Direct Connect Gateway dcgw\-1: IP address is `10.0.0.1`

* Direct Connect Gateway dcgw\-2: IP address is `172.16.4.1`

* Data Center IDC1: Local gateway IP: `10.0.0.2`, subnet CIDR block: `172.16.1.0/24`, server IP address: `172.16.1.10`

* Data Center IDC2: Local gateway IP is `172.16.4.2`, subnet CIDR block is `172.16.2.0/24`, server IP address is `172.16.2.10`


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created the required VPCs and their subnets. For detailed steps, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The subnet CIDR blocks of each VPC must not overlap or conflict. All existing route entries must not conflict with the subnet routes after the Direct Connect connection is added.   </div>
   

* Elastic Compute Service (ECS) instances have been created under each VPC and security group inbound rules have been added to allow access from the CIDR block of a data center. For detailed steps, see [Purchasing an ECS](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) and [Adding a security group rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).

* The network planning data described in the [Scenario introduction](https://docs.byteplus.com/en/docs/cen/Connecting-a-virtual-private-cloud-to-multiple-data-centers-Same-Account-and-Same-Region#.5Zy65pmv5LuL57uN) has been obtained.


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedures

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following section only describes essential parameters and their values. For parameters not mentioned, leave them as default.</div>


<span id=".5q2l6aqk5LiA77ya6YWN572u5LiT57q_6L-e5o6l"></span>
### Step 1: Configure Direct Connect connection


1. Refer to [Accessing Direct Connect Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1) to activate two physical dedicated circuits, named DAS236_port131_conn and DAS237_port131_conn respectively.

2. Create Direct Connect gateway.

   Follow the steps below to create two Direct Connect Gateways named dcgw\-1 and dcgw\-2 respectively.

   1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/region:dc+cn-beijing/DirectConnectGateway).

   2. In the top menu bar, select the region China (Beijing).

   3. Click **Create DC Gateway**.

   4. Configure relevant parameters based on the table below.

      
      |Parameter |Value (Direct Connect Gateway 1) |Value (Direct Connect Gateway 2) |
      |---|---|---|
      |Regions |China (Beijing) |China (Beijing) |
      |Name |dcgw\-1 |dcgw\-2 |
      |Agreement |Follow the console guidance to review and confirm the Legal |Follow the console guidance to review and confirm the Legal |
      

   5. Click **OK** to complete the action.

3. Create Virtual Interface.

   1. Log in to the [DC Virtual Interface console](https://console.byteplus.com/dc/region:dc+cn-beijing/VirtualInterface).

   2. Click **Create DC Virtual Interface**.

   3. Configure relevant parameters based on the table below.

      
      |Parameter |Value (Direct Connect Virtual Interface 1) |Value (Direct Connect Virtual Interface 2) |
      |---|---|---|
      |**Basic information** |||
      |Regions |China (Beijing) |China (Beijing) |
      |Name |vif\-1 |vif\-2 |
      |DC Connection |DAS236_port131_conn |DAS237_port131_conn |
      |Direct Connect Gateway |dcgw\-1 |dcgw\-2 |
      |**Interconnection information** |||
      |IPv4 interconnect IP |* ​Local Gateway Interconnection IP: 10.0.0.1/30​​<br><br>* Your gateway peer IP: 10.0.0.2/30​​ |* Cloud gateway peer IP: 172.16.4.1/30<br><br>* Peer gateway interconnection IP: 172.16.4.2/30 |
      |VLAN ID |10 |20 |
      |**Routing information** |||
      |Route type |Static routes |Static routes |
      

   4. Click **Create** to complete configuration.

4. Add static route.

   Follow the steps below to add static routes for the Direct Connect Gateways dcgw\-1 and dcgw\-2 respectively.

   1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/region:dc+cn-beijing/DirectConnectGateway).

   2. In the Direct Connect gateway list, click the name of the target Direct Connect gateway.

   3. On the **Routing information** tab of the details page, click **Add static route entry** to configure the route entry.

      
      |Parameter |Value (dcgw\-1) |Value (dcgw\-2) |
      |---|---|---|
      |Destination CIDR |172.16.1.0/24 |172.16.2.0/24 |
      |Next Hop type |Direct Connect Virtual Interface |Direct Connect Virtual Interface |
      |Next Hop |vif\-1 |vif\-2 |
      

   3. Click **Add** to complete configuration.


<span id=".5q2l6aqk5LqM77ya5Yib5bu65LqR5LyB5Lia572R5a6e5L6L"></span>
### Step 2: Create CEN instance


1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. Click **Create CEN**.

3. Configure relevant parameters based on the table below.

   
   |Parameter |Value |
   |---|---|
   |Name |cen\-test |
   |Attaching a network instance |On |
   |Regions |China (Beijing) |
   |Instance type |VPC |
   |Network Instances |vpc\-1 |
   

4. Click **Create** to complete the action.


<span id=".5q2l6aqk5LiJ77ya5Yqg6L29572R57uc5a6e5L6L"></span>
### Step 3: Attach Network Instance

Follow the steps below to attach the VPC vpc\-2 and the Direct Connect Gateways dcgw\-1 and dcgw\-2 to the CEN instance.


1. Click the target CEN instance name.

2. On the **Network Instances** tab, click **Attach Network Instance**.

3. Configure the relevant information for the network instance to be loaded. The table below uses the VPC\-2 as an example.

   
   |Parameter |Value |
   |---|---|
   |Account |My account |
   |Regions |China (Beijing) |
   |Instance type |VPC |
   |Network Instances |vpc\-2 |
   

4. Click **Attach** to complete the action.


<span id=".5q2l6aqk5Zub77ya6YWN572u5LqR5pyN5Yqh5Zmo5a6J5YWo57uE"></span>
### Step 4: Configure ECS Security Group

Follow the steps below to configure security group rules for the security groups associated with ecs\-1 and ecs\-2 respectively.


1. Log in to the ECS consoleECS console.

2. In the top menu bar, select the region: China (Beijing).

3. In the left\-side navigation pane, click **Instances**. On the instances page, select **Private IP address** in the search bar, input the target ECS instance's IP address, and search for the target ECS.

4. Click the name of the target ECS.

5. On the **Security Group** tab, click **Configure** next to the name of the security group to enter the access rules page.

6. On the **Inbound rule** tab, click **Add rule**. Refer to the following table to configure inbound rules that allow access from the CIDR block of IDC1 and IDC2 for the target ECS instance.

   
   |Direction |Priority |Policy |Protocol type |Port range |Source |Description |
   |---|---|---|---|---|---|---|
   |Inbound |1 |Allow |ALL |ALL |172.16.1.0/24 |Allow on\-premises IDC1 to access |
   |Inbound |1 |Allow |ALL |ALL |172.16.2.0/24 |Allow on\-premises IDC2 to access |
   

7. Click **Confirm** to complete the action.


<span id=".5q2l6aqk5LqU77ya6YWN572u5pys5Zyw5pWw5o2u5Lit5b-D6Lev55Sx"></span>
### Step 5: Configure Data Center Routing

On the on\-premises data center, configure routes from the IDC to all cloud VPCs that require interconnection. This involves creating route entries with the cloud VPCs as the destination addresses and the local gateway interconnection IP in the virtual interface as the next hop.

The following configuration uses IDC1 as an example (IDC2 configuration is similar):


1. Log in to the IDC1 gateway (gateway IP: 10.0.0.2) and configure routes from IDC1 to the cloud VPCs and the on\-premises IDC2 by referring to the following commands.

   ```Plain Text
   ip route 192.168.1.0 255.255.255.0 10.0.0.1
   ip route 192.168.2.0 255.255.255.0 10.0.0.1
   ip route 172.16.2.0 255.255.255.0 10.0.0.1
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Routing configuration commands may vary for gateway devices from different vendors. For specific configurations, consult your device vendor.   </div>
   

2. (Optional) If the servers in the IDC are deployed on different devices than the IDC gateway, run the following commands to configure routes for connectivity between the IDC gateway and the servers.

   `route add default gw 10.0.0.2`

3. Log in to the server in the IDC (IP address: 172.16.1.10) and run the following command to add a default route pointing to the IDC gateway.

   ```Plain Text
   route add default gw 10.0.0.2
   ```
   

4. Execute the command `ping 10.0.0.1` to test the connectivity between the Direct Connect Gateway and the local gateway.

   If data packets are returned after executing the command, it indicates that the cloud\-based Direct Connect Gateway can communicate with the local gateway.


<span id=".5q2l6aqk5YWt77ya5rWL6K-V6L-e6YCa5oCn"></span>
### Step 6: Test connectivity


1. Log in to the Elastic Compute Service (ECS) instance ecs\-1 in the vpc\-1. For detailed steps, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Run the `ping` command sequentially to test the connectivity between ecs\-1 and ecs\-2, IDC1, and IDC2.

   If the ping is successful, it indicates that ecs\-1 can communicate with ecs\-2, IDC1, and IDC2 respectively.

3. Log in to the Elastic Compute Service (ECS) instance ecs\-2 in the vpc\-2. For detailed steps, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

4. Sequentially run the `ping` command to test the connectivity of ecs\-2 to IDC1 and IDC2.

   If the ping is successful, it indicates that ecs\-2 can communicate with IDC1 and IDC2 respectively.

5. Log in to the server in on\-premises data center IDC1 using its IP address.

6. Run the `ping` command to test connectivity between IDC1 and IDC2.

   If the ping is successful, it indicates that IDC1 and IDC2 can communicate with each other.
