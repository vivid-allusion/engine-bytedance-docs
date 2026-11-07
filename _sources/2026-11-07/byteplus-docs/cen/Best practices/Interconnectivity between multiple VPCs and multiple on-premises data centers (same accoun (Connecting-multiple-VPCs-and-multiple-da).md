---
title: "Interconnectivity between multiple VPCs and multiple on-premises data centers (same account, cross-region)"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Connecting-multiple-VPCs-and-multiple-data-centers-same-account-across-Regions"
---

This topic explains how to enable mutual access between multiple Virtual Private Clouds (VPCs) in different regions and multiple on\-premises data centers under the same account.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The interconnectivity feature between multiple data centers is currently in beta stage. If you need a trial, please contact your account manager.</div>


<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

By default, different VPCs are logically isolated from each other, and VPCs cannot directly access resources over Direct Connect. Through Cloud Enterprise Network (CEN), network interconnection between VPC and Direct Connect can be realized, thereby enabling interconnected communication between a cloud network and a data center connected via Direct Connect.

This topic explains how to achieve interconnection between multiple VPCs in the cloud and multiple on\-premises data centers through CEN, as illustrated in the diagram below.

> The diagram displays sample configurations for each service. Modify these values according to your actual network architecture during implementation.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7e691ead064c0f454c71f11b6d37bed6.png) </span>

The relevant data for each resource in the diagram above is described below:


* Virtual Private Cloud vpc\-1: The Region is China (Beijing), the CIDR block of the subnet is `192.168.1.0/24`, and the private IP address of the Elastic Compute Service (ECS) ecs\-1 is `192.168.1.10`.

* vpc\-2: The Region is China (Shanghai), the CIDR block of the subnet is `192.168.2.0/24`, and the private IP address of the ecs\-2 is `192.168.2.10`.

* Direct Connect Gateway dcgw\-1: located in China (Beijing), the IP address is `10.0.0.1`.

* Direct Connect Gateway dcgw\-2: The Region is China (Shanghai), and the IP address is `172.16.4.1`.

* Data Center IDC1: Local gateway IP: 10.0.0.2, subnet CIDR block: `172.16.1.0/24`, server IP address: `172.16.1.10`.

* Data Center IDC2: Local gateway IP is 172.16.4.2, subnet CIDR block is `172.16.2.0/24`, server IP address is `172.16.2.10`.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created the required VPCs and their subnets. For detailed steps, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The subnet CIDR blocks of each VPC must not overlap or conflict. All existing route entries in each VPC route table must not conflict with the subnet routes after the Direct Connect connection is added.   </div>
   

* ECS instances have been created under each VPC. For detailed steps, see [Purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* The network planning data described in the [Scenario overview](https://docs.byteplus.com/en/docs/cen/Connecting-multiple-VPCs-and-multiple-data-centers-same-account-across-Regions#.5Zy65pmv5LuL57uN) has been obtained.


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedures

<span id=".5q2l6aqk5LiA77ya6YWN572u5LiT57q_6L-e5o6l"></span>
### Step 1: Configure Direct Connect connection


1. See [Accessing Direct Connect Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1) to activate two physical dedicated circuits, named DAS236_port131_conn and DAS237_port131_conn respectively.

2. Create Direct Connect gateway.

   Follow the steps below to create two Direct Connect Gateways named dcgw\-1 and dcgw\-2 respectively.

   1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/region:dc+cn-beijing/DirectConnectGateway).

   2. Click **Create DC Gateway** to create a DC Gateway with the following configuration.

      
      |Parameter |Value (Direct Connect Gateway 1) |Value (Direct Connect Gateway 2) |
      |---|---|---|
      |Regions |China (Beijing) |China (Shanghai) |
      |Name |dcgw\-1 |dcgw\-2 |
      |Agreement |Follow the console guidance to review and confirm the Legal |Follow the console guidance to review and confirm the Legal |
      

   3. Click **Buy now** to complete the action.

3. Create Virtual Interface.

   1. Log in to the [Direct Connect Virtual Interface console](https://console.byteplus.com/dc/region:dc+cn-beijing/VirtualInterface).

   2. Click **Create DC Virtual Interface** and see the following table to configure the virtual interface.

      
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
      

   3. Click **Create** to complete configuration.

4. Add static route.

   Follow the steps below to add static routes for the Direct Connect Gateways dcgw\-1 and dcgw\-2 respectively.

   3. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/region:dc+cn-beijing/DirectConnectGateway).

   4. In the Direct Connect gateway list, click the name of the target Direct Connect gateway.

   5. On the **Routing information** tab, click **Add static route** to configure the route entry.

      
      |Parameter |Value (Direct Connect Gateway 1) |Value (Direct Connect Gateway 2) |
      |---|---|---|
      |Destination CIDR |172.16.1.0/24 |172.16.2.0/24 |
      |Next Hop type |Direct Connect Virtual Interface |Direct Connect Virtual Interface |
      |Next Hop |vif\-1 |vif\-2 |
      

   3. Click **Add** to complete configuration.


<span id=".5q2l6aqk5LqM77ya5Yib5bu65LqR5LyB5Lia572R5a6e5L6L"></span>
### Step 2: Create CEN instance


1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. Click **Create CEN** and refer to the table below to configure the CEN.

   
   |Parameter |Value |
   |---|---|
   |Name |cen\-test |
   |Attaching a network instance |On |
   |Regions |China (Beijing) |
   |Instance type |VPC |
   |Network Instances |vpc\-1 |
   

3. Click **Create** to complete the action.


<span id=".5q2l6aqk5LiJ77ya5Yqg6L29572R57uc5a6e5L6L"></span>
### Step 3: Attach Network Instance

Follow these steps to load the vpc\-2 and Direct Connect Gateways dcgw\-1 and dcgw\-2 into the CEN Instance.


1. Click the target CEN instance name.

2. On the **Network Instances** tab, click **Attach Network Instance**.

3. Configure the relevant information for the network instance to be loaded. The table below uses the VPC\-2 as an example.

   
   |Parameter |Value |
   |---|---|
   |Regions |China (Shanghai) |
   |Instance type |VPC |
   |Network Instances |vpc\-2 |
   

4. Click **Attach** to complete the action.


<span id=".5q2l6aqk5Zub77ya6YWN572u6Leo5Zyw5Z-f5bim5a69"></span>
### Step 4: Configure cross\-region bandwidth


1. Create a bandwidth package.

   1. In the left\-side navigation pane, click **Bandwidth Package**.

   2. Click **Create BWP** and configure the relevant arguments as per the table below.

      
      |Parameter |Value |
      |---|---|
      |Billing method |Subscription |
      |Name |package\-1 |
      |Cloud Enterprise Network |cen\-test |
      |Interoperability area |China \- China |
      |Bandwidth |2Mbps |
      |Duration |1 month |
      

   3. Click **Confirm order** to proceed to the order details page.

   4. Follow the console guidance to review and accept Legal.

   5. Click **Buy now** and complete the payment according to the interface prompts.

   6. Click **Go to console** to view the successfully created Bandwidth Package.

2. Allocate inter\-region bandwidth.

   1. In the left\-side navigation pane, click **CEN Instances**.

   2. Click the target CEN instance name.

   3. On the **Inter\-region bandwidth** tab, click **Allocate inter\-region bandwidth**.

   4. Configure inter\-region bandwidth according to the table below.

      
      |Parameter |Value |
      |---|---|
      |Interconnected regions |China (Beijing) \- China (Shanghai) |
      |Bandwidth |2Mbps |
      

   5. Click **Allocate** to complete configuration.


<span id=".5q2l6aqk5LqU77ya6YWN572u5LqR5pyN5Yqh5Zmo5a6J5YWo57uE"></span>
### Step 5: Configure ECS security group

Follow the steps below to configure security group rules for the security groups associated with ecs\-1 and ecs\-2 respectively. The following steps use ecs\-1 as an example.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

2. In the top menu bar, select the region: China (Beijing).

3. In the left\-side navigation pane, click **Instances**. In the search bar on the instance page, select **Private IP address**, then input the private IP address of ecs\-1 to search and locate ecs\-1.

4. Click the ECS instance name **ecs\-1**.

5. On the **Security Group** tab, click **Configure** next to the security group name.

6. On the **Inbound rule** tab, click **Add rule**. Refer to the following table to configure inbound rules that allow access from the CIDR block of IDC1 and IDC2 for the target ECS instance.

   
   |Direction |Priority |Strategy |Protocol type |Port range |Source |Description |
   |---|---|---|---|---|---|---|
   |Inbound |1 |Allow |ALL |ALL |172.16.1.0/24 |Allow on\-premises IDC1 to access |
   |Inbound |1 |Allow |ALL |ALL |172.16.2.0/24 |Allow on\-premises IDC2 to access |
   

7. Click **Confirm** to complete the action.


<span id=".5q2l6aqk5YWt77ya6YWN572u5pys5Zyw5pWw5o2u5Lit5b-D6Lev55Sx"></span>
### Step 6: Configure data center routing

On the on\-premises IDC side, configure routes from the IDC to all VPCs that require connectivity. Specifically, create route entries with the destination address set to the VPC CIDR blocks and the next hop set to the local gateway interconnection IP in the physical connection interface.

The following configuration uses IDC1 as an example (IDC2 configuration is similar):


1. Log in to the local gateway of IDC1 and configure routes from IDC1 to the VPCs (vpc\-1, vpc\-2) and IDC2, using the following commands as a reference.

   ```JSON
   ip route 192.168.1.0 255.255.255.0 10.0.0.1
   ip route 192.168.2.0 255.255.255.0 10.0.0.1
   ip route 172.16.2.0 255.255.255.0 10.0.0.1
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Routing configuration commands may vary for gateway devices from different vendors. The commands below are provided for reference only.   </div>
   

2. (Optional) If the servers in the IDC are deployed on different devices than the IDC gateway, run the following commands to configure routes for connectivity between the IDC gateway and the servers.

   `route add default gw 10.0.0.2`

3. Log in to the server in the IDC (IP address: 172.16.1.10) and run the following command to add a default route pointing to the IDC gateway.

   `route add default gw 10.0.0.2`

4. Execute the command `ping 10.0.0.1` to test the connectivity between the Direct Connect Gateway and the local gateway.

   A successful ping response indicates that the cloud Direct Connect Gateway can communicate with the local gateway.


<span id=".5q2l6aqk5LiD77ya5rWL6K-V6L-e6YCa5oCn"></span>
### Step 7: Test connectivity


1. Log in to the ECS instance ecs\-1 in the vpc\-1. For detailed steps, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Run the `ping` command sequentially to test the connectivity between ecs\-1 and ecs\-2, IDC1, and IDC2.

   If the ping is successful, it indicates that ecs\-1 can communicate with ecs\-2, IDC1, and IDC2 respectively.

3. Log in to the ECS instance ecs\-2 in the vpc\-2. For detailed steps, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

4. Sequentially run the `ping` command to test the connectivity of ecs\-2 to IDC1 and IDC2.

   If the ping is successful, it indicates that ecs\-2 can communicate with IDC1 and IDC2 respectively.

5. Log in to the server in on\-premises data center IDC1 using its IP address.

6. Run the `ping` command to test connectivity between IDC1 and IDC2.

   If the ping is successful, it indicates that IDC1 and IDC2 can communicate with each other.
