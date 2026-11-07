---
title: "Interconnection between multiple VPCs in the cloud and multiple on-premises data centers (Cross-account, same region)"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Interconnection-between-multiple-VPCs-and-multiple-data-centers-Cross-account-same-region"
---

This document explains how to enable mutual access between multiple cloud Virtual Private Clouds (VPCs) and on\-premises data centers under the same account and region.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The interconnectivity feature between multiple data centers is currently in beta stage. If you need a trial, please contact your account manager.</div>


<span id="dCPHWvnF"></span>
## Scenarios

By default, different VPCs are logically isolated from each other, and VPCs cannot directly access resources over Direct Connect connections. Through Cloud Enterprise Network (CEN), network interconnection between VPC and Direct Connect can be realized, thereby enabling interconnected communication between a cloud network and a data center connected via Direct Connect.

This topic explains how to achieve interconnection between multiple VPCs in the cloud and multiple on\-premises data centers through Cloud Enterprise Network (CEN), as illustrated in the diagram below.

> The diagram displays sample configurations for each service. Modify these values according to your actual network architecture during implementation.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eff7d0c7253d5e6a9247d281f9ee9229.png) </span>

<span id="p7Eip5VL"></span>
## Data planning


* **Account A**

   
   |Resource Type | |Resource name |CIDR block/IP address |
   |---|---|---|---|
   |Virtual Private Cloud (VPC) ||VPC\-1 |192.168.1.0/24 |
   |Subnet ||Subnet\-1 |192.168.1.0/26 |
   |Elastic Compute Service ||ECS\-1 |192.168.1.10 |
   |Direct Connect |DC Connection |DAS236_port131_conn |\-\- |
   ||Direct Connect Gateway |dcgw\-1 |\-\- |
   ||Direct Connect Virtual Interface |vif\-1 |* ​Local Gateway Interconnection IP: 10.0.0.1/30​​<br><br>* Your gateway peer IP: 10.0.0.2/30​​ |
   |Data Center ||IDC1 |* Local gateway IP: 10.0.0.2<br><br>* Subnet CIDR block: 172.16.1.0/24<br><br>* Server IP address: 172.16.1.10 |
   |Cloud Enterprise Network ||CEN\-X |\-\- |
   

* **Account B**

   
   |Resource Type | |Resource name |CIDR block/IP address |
   |---|---|---|---|
   |Virtual Private Cloud (VPC) ||VPC\-2 |192.168.2.0/24 |
   |Subnet ||Subnet\-2 |192.168.2.0/26 |
   |Elastic Compute Service ||ECS\-2 |192.168.2.10 |
   |Direct Connect Gateway |DC Connection |DAS237_port131_conn |\-\- |
   ||Direct Connect Gateway |dcgw\-2 |\-\- |
   ||Direct Connect Virtual Interface |vif\-2 |* Cloud gateway peer IP: 172.16.4.1/30<br><br>* Peer gateway interconnection IP: 172.16.4.2/30 |
   |Data Center ||IDC2 |* Local gateway IP: 172.16.4.2<br><br>* Subnet CIDR block: 172.16.2.0/24<br><br>* Server IP address: 172.16.2.10 |
   


<span id="zKZPu2cQ"></span>
## Preparations


1. Complete the registration of Account A and Account B. 

2. Log in to Account A and Account B separately, and based on the data from the planning section above:

   1. Create VPC and subnet. For detailed steps, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The subnet CIDR blocks of each VPC must not overlap or conflict. All existing route entries must not conflict with the subnet routes after the Direct Connect connection is added.      </div>
      

   2. Create ECS. For detailed steps, see [Purchasing an Elastic Compute Service](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   3. Configure the security group rules for your ECS instances to allow traffic from the IDC. For operations, see [Adding a security group access rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).

      
      |Direction |Priority |Strategy |Protocol type |Port range |Source |Description |
      |---|---|---|---|---|---|---|
      |Inbound |1 |Allow |ALL |ALL |172.16.1.0/24 |Allow on\-premises IDC1 to access |
      |Inbound |1 |Allow |ALL |ALL |172.16.2.0/24 |Allow on\-premises IDC2 to access |
      


<span id="SP3pBYPL"></span>
## Configuration procedures

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following section only describes essential parameters and their values. For parameters not mentioned, leave them as default.</div>


<span id="dGCwgefC"></span>
### Step 1: Configure DC and CEN for account A

<span id="bPHGqCwn"></span>
#### (1) Enable DC Connection


Using Account A, activate one physical connection DAS236_port131_conn by referring to [Create DC Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1).


<span id="lwubtjsp"></span>
#### (2) Create DC Gateway


   1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/region:dc+cn-beijing/DirectConnectGateway).

   2. In the top menu bar, select the region: China (Beijing).

   3. Click **Create DC Gateway**. Configure relevant parameters based on the table below.

      
      |Parameter |Explanation |Value |
      |---|---|---|
      |Regions |Select the region where the DC Gateway is deployed. It must match the region of the DC Connection. |China (Beijing) |
      |Name |Enter a name for the DC Gateway. |dcgw\-1 |
      |ASN |Set an ASN for the DC Gateway. |64512 |
      |Agreement |Follow the console guidance to review and accept Legal. |Follow the console guidance to review and confirm the Legal |
      

   4. Click **OK** to complete the action.


<span id="8bUE0HRY"></span>
#### (3) Create DC Virtual Interface


   1. Log in to the [DC Virtual Interface console](https://console.byteplus.com/dc/region:dc+cn-beijing/VirtualInterface) .

   2. Click **Create DC Virtual Interface**. Configure relevant parameters based on the table below.

      
      |Parameter |Explanation |Value |
      |---|---|---|
      |**Basic information** |||
      |Regions |Select the region for the DC Virtual Interface. It must be the same as the region to which the DC Connection and DC Gateway belong. |China (Beijing) |
      |Name |Enter a name of the DC Virtual Interface. |vif\-1 |
      |DC Connection |Filter the target DC Connection by project to associate with the Ethernet Virtual Interface. |DAS236_port131_conn |
      |Direct Connect Gateway |Filter the target DC Gateway by project to associate with the DC Virtual Interface. |dcgw\-1 |
      |**Interconnection information** | | |
      |IPv4 interconnect IP |Type the IPv4 interconnect IP. |* ​Local Gateway Interconnection IP: 10.0.0.1/30​​<br><br>* Your gateway peer IP: 10.0.0.2/30​​ |
      |VLAN ID |Set the VLAN ID for connecting to the data center. Range: 0–2999. |10 |
      |**Routing information** |||
      |Route type |Support two route types: BGP (recommended) and Static. |Static routes |
      

   3. Click **Create** to complete configuration.


<span id="JPcCojS5"></span>
#### (4) Add static route


Follow the steps below to add static routes for the Direct Connect Gateways dcgw\-1 and dcgw\-2 respectively.

   1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/region:dc+cn-beijing/DirectConnectGateway).

   2. In the Direct Connect gateway list, click the name of the target Direct Connect gateway.

   3. On the **Routing information** tab of the details page, click **Add static route entry** to configure the route entry.

      
      |Parameter |Explanation |Value |
      |---|---|---|
      |Destination CIDR |Input the target CIDR block. |172.16.1.0/24 |
      |Next Hop type |Select Next Hop type |Direct Connect Virtual Interface |
      |Next Hop |Select the next hop. |vif\-1 |
      

   4. Click **Create** to complete configuration.


<span id="k1TQihcm"></span>
#### (5) Create CEN instance


   1. Use account A to log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

   2. Click **Create CEN**. Configure relevant parameters based on the table below.

      
      |Parameter |Explanation |Value |
      |---|---|---|
      |Name |Enter the name of CEN instance. |CEN\-X |
      |Attaching a network instance |Enable the switch to attach a network instance under the same account to this CEN instance. Disabled by default. |On |
      |Regions |Select the region where the instance to be attached resides. |China (Beijing) |
      |Instance type |Supports attaching either Virtual Private Cloud or Direct Connect Gateway instances. |VPC |
      |Network Instances |Select the network instance to be attached. |VPC\-1 |
      

   3. Click **OK** to complete the action.


<span id="qJCXsmQS"></span>
### Step 2: Configure DC and CEN for account B

<span id="MYBDpk1t"></span>
####  **(1) Enable DC Connection**


Using Account B, activate one physical connection DAS237_port131_conn by referring to [Create DC Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1).


<span id="U15JdBvt"></span>
####  **(2) Create DC Gateway**


   1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/region:dc+cn-beijing/DirectConnectGateway).

   2. In the top menu bar, select the region China (Beijing).

   3. Click **Create DC Gateway**. Configure relevant parameters based on the table below.

      
      |Parameter |Explanation |Value (account B) |
      |---|---|---|
      |Regions |Select the region where the DC Gateway is deployed. It must match the region of the DC Connection. |China (Beijing) |
      |Name |Enter a name for the DC Gateway. |dcgw\-2 |
      |ASN |Set an ASN for the DC Gateway. |64513 |
      |Agreement |Follow the console guidance to review and accept Legal. |Follow the console guidance to review and confirm the Legal |
      

   4. Click **OK** to complete the action.


<span id="p1K89fk6"></span>
####  **(3) Create DC Virtual Interface**


   1. Log in to the [DC Virtual Interface console](https://console.byteplus.com/dc/region:dc+cn-beijing/VirtualInterface) .

   2. Click **Create DC Virtual Interface**. Configure relevant parameters based on the table below.

      
      |Parameter |Explanation |Value (account B) |
      |---|---|---|
      |**Basic information** | | |
      |Regions |Select the region for the DC Virtual Interface. It must be the same as the region to which the DC Connection and DC Gateway belong. |China (Beijing) |
      |Name |Enter a name of the DC Virtual Interface. |vif\-2 |
      |DC Connection/ |Filter the target DC Connection by project to associate with the Ethernet Virtual Interface. |DAS237_port131_conn |
      |Direct Connect Gateway |Filter the target DC Gateway by project to associate with the DC Virtual Interface. |dcgw\-2 |
      |**Interconnection information** | | |
      |IPv4 interconnect IP |Type the IPv4 interconnect IP. |* Cloud gateway peer IP: 172.16.4.1/30<br><br>* Peer gateway interconnection IP: 172.16.4.2/30 |
      |VLAN ID |Set the VLAN ID for connecting to the data center. Range: 0–2999. |20 |
      |**Routing information** |||
      |Route type |Support two route types: BGP (recommended) and Static. |Static routes |
      

   3. Click **Create** to complete configuration.


<span id="h8q1HpZ0"></span>
####  **(4) Add static route**


Follow the steps below to add static routes for the Direct Connect Gateways dcgw\-1 and dcgw\-2 respectively.

   1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/region:dc+cn-beijing/DirectConnectGateway).

   2. In the Direct Connect gateway list, click the name of the target Direct Connect gateway.

   3. On the **Routing information** tab of the details page, click **Add static route entry** to configure the route entry.

      
      |Parameter |Explanation |Value (dcgw\-2 of account B) |
      |---|---|---|
      |Destination CIDR |Input the target CIDR block. |172.16.2.0/24 |
      |Next Hop type |Select Next Hop type |Direct Connect Virtual Interface |
      |Next Hop |Select the next hop. |vif\-2 |
      

   4. Click **Create** to complete configuration.


<span id="7QbhnTle"></span>
#### (5) Account authorization


You can refer to this procedure to grant Account A the permissions to operate resources under Account B. Specifically, this allows Account A's CEN\-X to load Account B's VPC\-2 and Direct Connect Gateway dcgw\-2.

   1. Authorize VPC

      1. Log in to the VPC consoleVPC console using Account B.

      2. In the top menu bar, select the region "China (Beijing)".

      3. Click the VPC name "VPC\-2". In the **CEN cross\-account authorization** tab, click **CEN cross\-account authorization**.

      4. Enter the ID of Account A and the ID of the CEN instance "CEN\-X". Click **Migrate** to complete the action.

   2. Authorize Direct Connect Gateway

      1. Log in to [Direct Connect Gateway console](https://console.byteplus.com/dc/region:dc+cn-beijing/DirectConnectGateway) with Account B.

      2. In the top menu bar, select your target region.

      3. Click the name of the target DC Gateway. In the **CEN cross\-account authorization** tab, click **CEN cross\-account authorization**.

      4. Enter the Account ID to which the CEN belongs and the CEN instance ID to be authorized. Click **Migrate** to complete the action.


<span id="flsa6kiV"></span>
### Step 3: Install Network Instance

Follow the steps below to attach the VPC vpc\-2 and the Direct Connect Gateways dcgw\-1 and dcgw\-2 to the CEN instance.


1. Log in to the CEN console using **Account A**.

2. Click the target CEN instance name.

3. On the **Network Instances** tab, click **Attach Network Instance**.

4. Configure the relevant information for the network instance to be loaded. The table below uses the VPC\-2 as an example.

   
   |Parameter |Explanation |Value 1 |Value 2 |Value 3 |
   |---|---|---|---|---|
   |Account |Select the account to which the network instance belongs. |My account |Cross\-account<br><br>Account B |Cross\-account<br><br>Account B |
   |Regions |Select the region where the network instance resides. |China (Beijing) |China (Beijing) |China (Beijing) |
   |Instance type |Select the type of network instance. |Direct Connect Gateway |VPC |Direct Connect Gateway |
   |Network Instances |Select a network instance. |dcgw\-1 |VPC\-2 |dcgw\-2 |
   

5. Click **Install** to complete the action.


<span id="aimXr9Hh"></span>
### Step 4: Configure data center routing

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


<span id="Wt0Dbp5q"></span>
## Verification


1. Log in to ECS\-1 in VPC\-1. For detailed steps, see [Logging into a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging into a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Run the `ping` command sequentially to test the connectivity between ECS\-1 and ECS\-2, IDC1, IDC2.

   If ping is successful, it indicates that ECS\-1 has established connectivity with ECS\-2, IDC1, and IDC2, respectively.

3. Log in to ECS\-2 in VPC\-2. For detailed steps, see [Logging into a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging into a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

4. Run the `ping` command sequentially to test the connectivity between ECS\-2 and IDC1, IDC2.

   If the ping is successful, it indicates that ECS\-2 can communicate with IDC1 and IDC2 respectively.

5. Log in to the server in on\-premises data center IDC1 using its IP address.

6. Run the `ping` command to test connectivity between IDC1 and IDC2.

   If the ping is successful, it indicates that IDC1 and IDC2 can communicate with each other.
