---
title: "Resolve address conflicts in multi-VPC interconnection scenarios"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Resolving-address-conflicts-in-multiple-VPCs"
---

When using Cloud Enterprise Network or Transit Router to connect multiple VPCs, if overlapping CIDR blocks exist between different VPCs, you can use a VPC NAT Gateway to resolve address conflicts and enable private network resource communication.

<span id=".6IOM5pmv5LuL57uN"></span>
## Background introduction

Two VPCs from different business lines in a company need to communicate, but their communicating subnets overlap. Resolve IP address conflicts through the VPC NAT gateway.


* The name of the Virtual Private Cloud 1 is VPC\-A, and its CIDR block is 192.168.0.0/16.

   * The name of Subnet 1 is Subnet\-A1, and its subnet CIDR block is 192.168.1.0/24.

   * The name of Subnet 2 is Subnet\-A2, and its subnet CIDR block is 192.168.2.0/24.

   * The name of Subnet 3 is Subnet\-A100, and its subnet CIDR block is 192.168.100.0/24.

* The name of the Virtual Private Cloud 2 is VPC\-B, and its CIDR block is 192.168.0.0/16.

   * The name of Subnet 1 is Subnet\-B1, and its subnet CIDR block is 192.168.1.0/24.

   * The name of Subnet 2 is Subnet\-B2, and its subnet CIDR block is 192.168.2.0/24.

   * The name of Subnet 3 is Subnet\-B200, and its subnet CIDR block is 192.168.200.0/24.

* The IP address of ECS\-A1 is 192.168.1.11, ECS\-A2 is 192.168.2.30, ECS\-B1 is 192.168.1.22, and ECS\-B2 is 192.168.2.31.


The diagram below illustrates the content. For more details on VPC NAT Gateway route configuration, please refer to [Route configuration principles](https://docs.byteplus.com/en/docs/natgateway/Route-configuration-principles).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f50205e801debb54b676dff0e245ea63.png) </span>

To enable ECS\-A1 to access ECS\-B1, configure an SNAT rule for VPC\-A and a DNAT rule for VPC\-B. Similarly, to enable ECS\-B2 to access ECS\-A2, configure an SNAT rule for VPC\-B and a DNAT rule for VPC\-A.

This article demonstrates only ECS\-A1 accessing ECS\-B1.

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

Complete the following steps based on the background information before proceeding:


* Use the same BytePlus account to create two VPCs in China (Beijing), with their parameters consistent with the background introduction. For specific actions, see [Creating a Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* Create cloud servers ECS\-A1 (192.168.1.11) in subnet\-A1 and ECS\-A2 (192.168.2.30) in subnet\-A2 of VPC\-A; create ECS\-B1 (192.168.1.22) in subnet\-B1 and ECS\-B2 (192.168.2.31) in subnet\-B2 of VPC\-B. For more information, see [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures

<span id=".5q2l6aqk5LiA77ya6YWN572u56eB572RTkFU572R5YWz"></span>
### Step 1: Configure VPC NAT Gateway

<span id=".5Yib5bu65Lik5Liq56eB572RTkFU572R5YWz"></span>
#### 1. Create two VPC NAT Gateways

You can follow this procedure to create one VPC NAT Gateway each for VPC\-A and VPC\-B.


1. Log in to the  [VPC NAT Gateway console ](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. Click **Create VPC NAT Gateway**.

4. configure relevant parameters based on the table below.

   
   |Parameter |Explanation |This article uses the value (VPC\-A) |This article uses the value (VPC\-B) |
   |---|---|---|---|
   |Billing method |Only pay\-as\-you\-go billing is supported. |Pay\-as\-you\-go |Pay\-as\-you\-go |
   |Regions |Select the region where the VPC NAT gateway resides. |China (Beijing） |China (Beijing） |
   |Name |Enter the name of the VPC NAT Gateway. |VPC NAT Gateway\-A |VPC NAT Gateway\-B |
   |Virtual Private Cloud (VPC) |Select the VPC to which the VPC NAT Gateway belongs from the dropdown menu. |VPC\-A\|192.168.0.0/16 |VPC\-B\|192.168.0.0/16 |
   |Subnet |Select a subnet from the dropdown list. |Subnet\-A100\|192.168.100.0/24 |subnet\-B200\|192.168.200.0/24 |
   |Specification |No specification required. |\- |\- |
   |Affiliated Project |Select the project to which the VPC NAT Gateway belongs. |default |default |
   |Tags |Add one or more user tags to the VPC NAT Gateway as needed. |nat:v1 |nat:v2 |
   

5. Click **Buy now**.

6. Follow the console guidance to review and accept Legal, and click **Buy now** to complete the operation.


View the default NAT IP address in the VPC NAT Gateway list. The default NAT IP address for VPC\-A is 192.168.100.128, and the default NAT IP address for VPC\-B’s VPC NAT Gateway is 192.168.200.254.

<span id=".5Li6VlBDLUHnmoTnp4HnvZFOQVTnvZHlhbPliJvlu7pTTkFU6KeE5YiZ"></span>
#### 2. Create an SNAT rule for VPC\-A’s VPC NAT Gateway


1. In the VPC NAT Gateway list, click the name of the VPC NAT Gateway\-A to enter the details page.

2. Select the **SNAT rules** tab, then click **Create SNAT rule**.

3. configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Example Value |
   |---|---|---|
   |Name |Set the name of the SNAT rule. |SNAT\-X |
   |Granularity |Select the granularity of the SNAT rule. |Subnet<br><br>192.168.1.0/24 |
   |NAT IP |Select the NAT IP address of the VPC NAT Gateway. This article selects the default NAT IP address. |192.168.100.128\|nat\-default\-ip |
   

4. Click **OK** to complete the action.


<span id=".5Li6VlBDLULnmoTnp4HnvZFOQVTnvZHlhbPliJvlu7pETkFU6KeE5YiZ"></span>
#### 3. Create a DNAT rule for VPC\-B’s VPC NAT Gateway


1. In the VPC NAT Gateway list, click the name of private NAT Gateway\-B to enter the detail page.

2. Select the **DNAT rules** tab, and click **Create DNAT rule**.

3. configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Example Value |
   |---|---|---|
   |Name |Enter the name of the DNAT rule. |DNAT\-X |
   |Agreement |Select protocol type. Supported protocols include TCP, UDP. |TCP |
   |Local IP and Port |Set the private IP address and port of the pre\-configured Elastic Compute Service instance. |192.168.1.22<br><br>22 |
   |NAT IP address and port |Set the transit NAT IP address and its port for the VPC NAT Gateway. This article uses the default transit NAT IP address and its port. |192.168.200.254\|nat\-default\-ip<br><br>22 |
   

4. Click **OK** to complete the action.

5. After creating the DNAT rule, you must also allow the corresponding security group rules in VPC\-A.

   1. Log in to the ECS consoleECS console.

   2. Click the ECS instance name, select the Security Group tab, and click the security group name.

   3. On the **Access rules \> Inbound** tab, add a rule. Set policy to Allow, protocol type to TCP/UDP, port range to Local IP ports, and source address to 0.0.0.0/0. For more details, see [Security group overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview).


<span id=".5q2l6aqk5LqM77ya6YWN572uTkFU572R5YWz6Lev55Sx"></span>
### Step two: configure NAT Gateway routes

<span id=".5YeG5aSH6Lev55Sx6KGo"></span>
#### 1. Prepare route tables

Create two custom route tables and associate each with the subnet where the VPC NAT Gateway is deployed. The VPC NAT Gateway will route traffic through the route table associated with its subnet to the Cloud Enterprise Network or Transit Router.


1. Log in to the [Route Table Console](https://console.byteplus.com/vpc/routeTable).

2. In the top menu bar, select the target region and project. In this example, they are **China (Beijing)**  and **default**.

3. Click **Create Route Table**.

4. configure relevant parameters based on the table below.

   
   |Parameter |Explanation |This value is from the custom route table of VPC\-A |This article takes the value (VPC\-B’s Custom Route Table) |
   |---|---|---|---|
   |Name |Enter the name of custom route table. |route\-A |route\-B |
   |Virtual Private Cloud (VPC) |Select the VPC for the route table. |VPC\-A |VPC\-B |
   |Route entry |Use the default system route without manually adding routes. |\- |\- |
   |Affiliated Project |Select a route table entry. |default |default |
   

5. Click **OK** to complete the action.

6. In the route table list, click Attach Subnet next to the newly created custom route table route\-A.

7. Select Subnet\-A100, and click OK to complete the attachment.

8. Similarly, associate subnet\-B200 to the custom route table route\-B.


<span id=".5rWB6YeP6Lev55Sx5Yiw56eB572RTkFU572R5YWz77yI57O757uf6Lev55Sx6KGo77yJ"></span>
#### 2. route traffic to the VPC NAT Gateway (system route table)

Route traffic destined for the peer CIDR block to the VPC NAT Gateway:


* Route traffic from cloud resources in subnet\-A1 and subnet\-A2 destined for the peer network (192.168.200.0/24) to VPC NAT Gateway\-A.

* Route traffic from cloud resources in subnet\-B1 and subnet\-B2 destined for the peer network (192.168.100.0/24) to VPC NAT Gateway\-B.

1. In the Route Table List, click the system route table name of VPC\-A and VPC\-B.

2. Select **Route entry \> Custom route** tab, and click **Add route**.

3. configure relevant parameters based on the table below.

   
   |Parameter |Explanation |This article uses the system route table of VPC\-A as the value |Example Value (system route table of VPC\-B) |
   |---|---|---|---|
   |Destination CIDR |Enter the peer CIDR block. |192.168.200.0/24 |192.168.100.0/24 |
   |Next Hop type |Select the Next Hop type. |NAT Gateway |NAT Gateway |
   |Next Hop |Select the next hop resource. |VPC NAT Gateway\-A |VPC NAT Gateway\-B |
   

4. Click **Create** to complete configuration.


<span id=".5rWB6YeP6Lev55Sx6Iez5LqR5LyB5Lia572R5oiW5Lit6L2s6Lev55Sx5Zmo77yI6Ieq5a6a5LmJ6Lev55Sx6KGo77yJ"></span>
#### 3. Route traffic to Cloud Enterprise Network (CEN) or Transit Router (Custom Route Table)


* Cloud Enterprise Network (CEN): after configuring CEN, the custom route tables route\-A and route\-B automatically add route entries to CEN.

* Transit Router (TR): after configuring the transit router, you need to manually add route entries to the transit router in custom route tables route\-A and route\-B. See the following for details.


<span id=".5q2l6aqk5LiJ77ya6YWN572u5LqR5LyB5Lia572R5oiW5Lit6L2s6Lev55Sx5Zmo"></span>
### Step 3: Configure Cloud Enterprise Network or Transit Router


<Tabs>
<Tab zoneid="DBs0aZx6s4" title="Solution 1: Configure Cloud Enterprise Network (CEN)">
<TabTitle>Solution 1: Configure Cloud Enterprise Network (CEN)</TabTitle>

<span id="DxTXWJtO"></span>
#### Create CEN

You can create a Cloud Enterprise Network and attach the pre\-prepared Virtual Private Cloud VPC\-A through this operation.


1. login [Cloud Enterprise Network console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. Click **Create CEN**.

3. configure relevant parameters based on the table below.

   
   |**Parameter** |**Explanation** |**Example Value** |
   |---|---|---|
   |Name |Enter the name of CEN instance. |Cloud Enterprise Network (CEN)\-X |
   |Attaching a network instance |Whether to enable the switch for loading the network instance. |On |
   |Regions |Select the Region where the network instance resides. |China (Beijing） |
   |Instance type |Select the type of network instance. |Virtual Private Cloud (VPC) |
   |Network Instances |Select the Virtual Private Cloud instance. |VPC\-A |
   |Affiliated Project |Select the project to which the Cloud Enterprise Network belongs. |default |
   |Tags |Add one or more user tags to the Cloud Enterprise Network as needed. |cen：v1 |
   

4. Click **OK** to complete the action.


<span id="Bzd4J00A"></span>
#### 2. Load network instance


1. In the CEN Instances list, click the target CEN instance name.

2. Select the "network instance" tab and click the "Attach Network Instance" button.

3. configure relevant parameters based on the table below.

   
   |**Parameter** |**Explanation** |**Example Value** |
   |---|---|---|
   |Account |Select the account to which the network instance to be attached belongs. |My account |
   |Regions |Select the region where the network instance to be attached belongs. |China (Beijing） |
   |Instance type |Select the type of network instance. |Virtual Private Cloud (VPC) |
   |Network Instances |Select the Virtual Private Cloud instance. |VPC\-B |
   

4. Click "Disable" to complete loading.


A route entry is synchronized from the CEN instance to the custom route table of VPC\-A. The route entry points to 192.168.200.0/24 and the next hop is CEN\-X. The custom route table of VPC\-B automatically synchronizes the route entry with the destination 192.168.100.0/24 and the next hop set as CEN\-X.


|**Route table name** |**Associate a subnet** |**Destination CIDR** |**Next Hop** |
|---|---|---|---|
|System route table of VPC\-A |Subnet\-A1, Subnet\-A2 |192.168.200.0/24 |VPC NAT Gateway\-A |
|Custom route table of VPC\-A |Subnet\-A100 |192.168.200.0/24 |Cloud Enterprise Network\-X |
|System route table of VPC\-B |Subnet\-B1, Subnet\-B2 |192.168.100.0/24 |VPC NAT Gateway\-B |
|Custom route table of VPC\-B |Subnet\-B200 |192.168.100.0/24 |Cloud Enterprise Network\-X |



</Tab>
<Tab zoneid="q9LSfwuFJ6" title="Solution 2: Configure Transit Router (TR)">
<TabTitle>Solution 2: Configure Transit Router (TR)</TabTitle>

<span id="jrHuN32l"></span>
#### 1. Create a Transit Router instance and its TR route table


1. Log in [Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click **Create TR**.

3. configure relevant parameters based on the table below.

   
   |**Parameter** |**Explanation** |**Example Value** |
   |---|---|---|
   |Regions |Select the region for the Transit Router (TR) instance.​​ |China (Beijing） |
   |Name |Enter the name of the Transit Router instance. |Transit Router (TR)\-X |
   |Project |Select the project for the Transit Router instance. |default |
   

4. Click **Create** to complete the creation of the TR instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Upon successful creation, the system automatically generates a default TR route table. Record its name. Take RouteTable\-default as an example.   </div>
   

5. On the Transit Router instances page, click the name of your target TR instance.

6. Select the route table tab, click Create Route Table next to the TR route table list, and a window for creating a route table pops up.

7. Type the custom route table name: R\-Table\-X. Click **Create** to complete the custom TR route table creation.


<span id="vAtSCmMH"></span>
#### 2. create network instance connection

Follow these steps to create two network instance connections in sequence. The configurations for the two connections correspond to Example 1 and Example 2 in the parameter configuration table.


1. On the Transit Router instances page, click the name of your target TR instance.

2. On the Intra\-Region Attachment tab, click Create intra\-region attachments.

3. configure relevant parameters based on the table below.

   
   |**Parameter** |**Explanation** |**Example value 1** |**Example value 2** |
   |---|---|---|---|
   |Transit Router |Default: The Transit Router instance you selected.​​ |Transit Router (TR)\-X |Transit Router (TR)\-X |
   |Regions |Default: Same as the region where the TR instance resides. |China (Beijing） |China (Beijing） |
   |Name |The name of the network instance attachment to be created. |Attach\-VPC\-A |Attach\-VPC\-B |
   |Network instance type |Select the type for the network instance attachment to be created. |Virtual Private Cloud (VPC) |Virtual Private Cloud (VPC) |
   |Virtual Private Cloud (VPC) |Select the VPC instance to be attached. |VPC\-A |VPC\-B |
   |AZs and Subnets |Select the subnet in the Availability Zone where the attachment point resides. The subnet assigns a private IP address to the network interface of the attachment.​​ |AZ\-A, subnet\-A1 |AZ\-A, Subnet\-B1 |
   |Association forwarding |Enable association forwarding and select the destination Transit Router (TR) route table. When enabled, traffic originating from this network attachment will be forwarded based on the routing entries in its associated Transit Router (TR) route table.​​ |Enable; RouteTable\-default |Enable; R\-Table\-X |
   |Route Propagation |Enable route propagation and select the destination Transit Router (TR) route table. When enabled, the specified Transit Router (TR) route table automatically creates routing entries with destination CIDRs set to the subnets of the attached VPC, using the network attachment itself as the next hop.​​ |Enable; R\-Table\-X |Enable; RouteTable\-default |
   

4. Click **Migrate** to complete the action.


At this point, the routing entries and association status for the two TR route tables are as follows:


|**TR route table name** |**Destination CIDR** |Next Hop |**Association forwarding** |**Explanation** |
|---|---|---|---|---|
|RouteTable\-default |192.168.200.0/24 |Attach\-VPC\-B |Attach\-VPC\-A |Traffic to 192.168.200.0/24 received by the Transit Router (TR) from Attach\-VPC\-A will be forwarded to Attach\-VPC\-B. |
|R\-Table\-X |192.168.100.0/24 |Attach\-VPC\-A |Attach\-VPC\-B |The transit router forwards traffic destined for 192.168.100.0/24 received from Attach\-VPC\-B to Attach\-VPC\-A. |


<span id="Zq5AffAV"></span>
#### 3. route traffic to the transit router (custom route table)

Manually add route entries for custom route tables route\-A and route\-B to route traffic from VPC NAT Gateway\-A and VPC NAT Gateway\-B to the transit router.


1. In the route table list, click the target custom route table name.

2. On the **Route Entry \> Custom route** tab, click **Add route**.

   * Refer to the table below and add the following custom routes to the custom route table route\-A in VPC\-A.

   
   |**Parameter** |**Explanation** |**Example Value** |
   |---|---|---|
   |Destination CIDR |The input is the subnet B200 CIDR block of VPC\-B. |192.168.200.0/24 |
   |Next Hop type |Select the Next Hop Resource Type for the route entry, which directs traffic destined for the target CIDR block to the specified resource. |Transit Router |
   |Next Hop |Specify the specific next hop resource. |Transit Router (TR)\-X |
   

   * Refer to the table below and add the following custom routes to the custom route table route\-B in VPC\-B.

   
   |**Parameter** |**Explanation** |**Example Value** |
   |---|---|---|
   |Destination CIDR |Enter the CIDR block of subnet\-A100 in VPC\-A. |192.168.100.0/24 |
   |Next Hop type |Select the Next Hop Resource Type for the route entry, which directs traffic destined for the target CIDR block to the specified resource. |Transit Router |
   |Next Hop |Specify the specific next hop resource. |Transit Router (TR)\-X |
   

3. Click **Add** to complete the route configuration.


At this point, except for the system default route entries, the route entries for the four route tables are as follows:


|**Route table name** |**Associate a subnet** |**Destination CIDR** |**Next Hop** |
|---|---|---|---|
|VPC\-A system route table |Subnet\-A1 |192.168.200.0/24 |VPC NAT Gateway\-A |
|Custom route table of VPC\-A |Subnet\-A100 |192.168.200.0/24 |Transit Router (TR)\-X |
|System Route Table of VPC\-B |Subnet\-B1 |192.168.100.0/24 |VPC NAT Gateway\-B |
|Custom route table of VPC\-B |subnet\-B200 |192.168.100.0/24 |Transit Router (TR)\-X |



</Tab>
</Tabs>


<span id=".5q2l6aqk5Zub77ya6aqM6K-B"></span>
### Step 4: Verification


<Tabs>
<Tab zoneid="bRTvKAA10W" title="Verify SNAT rules">
<TabTitle>Verify SNAT rules</TabTitle>

1. Log in to the Elastic Compute Service instance ECS\-A1 (192.168.1.11) and execute the command `ping <NAT IP address of VPC NAT Gateway-B>`. This article uses the input `ping 192.168.200.254`.

2. If `ping` is successful, ECS\-A1 can access VPC NAT Gateway\-B. If `ping` fails, check the SNAT entry and related route configuration.


</Tab>
<Tab zoneid="ofYyzNRf2f" title="Verify the DNAT entry">
<TabTitle>Verify the DNAT entry</TabTitle>

1. Log in to the cloud server instance ECS\-A1 (192.168.1.11), enter `ssh <NAT IP address> -p <NAT IP port>` in the command line. Here enter `ssh 192.168.200.254 -p 22`.

2. Reaching the login page indicates ECS\-A1 in VPC\-A can access ECS\-B1 in VPC\-B. If the login page does not appear, please check the DNAT entry, related route configuration, and whether the security group allows traffic.


</Tab>
</Tabs>
