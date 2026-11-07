---
title: "Using a specified IP to communicate with the on-premises data center"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Connecting-to-a-data-center-using-a-specific-IP-address"
---

When an on\-premises data center requires communication with cloud resources, you can use the VPC NAT Gateway to allow only specified IP addresses from cloud resources for easy management and security.

<span id=".6IOM5pmv5LuL57uN"></span>
## Background

Resources within the Virtual Private Cloud (VPC) use designated IP addresses to access resources in the on\-premises data center.


* The on\-premises data center subnet CIDR block is 172.16.1.0/24, the interconnect IP is 10.0.0.2, and the IP address of a running server A is 172.16.1.10.

* The private network is named VPC\-A with a CIDR block of 192.168.1.0/16. The interconnect IP is 10.0.0.1.

   * Subnet 1 is named subnet\-A1 with a CIDR block of 192.168.1.0/24.

   * Subnet 2 is named subnet\-A2 with a CIDR block of 192.168.2.0/24.

   * Elastic Compute Service (ECS): ECS\-A1 IP address is 192.168.1.10, and the ECS\-A2 IP address is 192.168.2.20.


The diagram below illustrates this. To learn more about private VPC NAT Gateway route configuration details, see [Route configuration principles](https://docs.byteplus.com/en/docs/natgateway/Route-configuration-principles).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_edc81b053f5baf4a5c3144fd12061af2.png) </span>

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

Complete the following steps based on the background information before proceeding:


* Create a VPC with parameters consistent with that described in the Background section. For specific actions, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* Create ECS\-A1 (192.168.1.10) in subnet A1 of VPC\-A and ECS\-A2 (192.168.2.20) in subnet A2. For detailed steps, see [Purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* Create a CEN and add VPC\-A. For specific actions, see [Creating a CEN instance](https://docs.byteplus.com/en/docs/cen/CEN-instances-01).

* Configure a Direct Connect to enable communication between the on\-premises data center and VPC\-A. For procedure, see [Connecting an on-premises data center to a VPC via a single Direct Connect with static routing](https://docs.byteplus.com/en/docs/directconnect/Best-Practices-4).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6aqM6K-B5pys5ZywSURD5LiO5LqR5LiKVlBD5LqS6YCa"></span>
### Step 1: Verify connectivity between on\-premises data center and VPCs


1. Log in to server A whose IP address is 172.16.1.10.

2. Execute the `ping 192.168.1.10` command in the command line.

3. `Ping` success indicates connectivity between the on\-premises data center and cloud VPC\-A.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If <code>ping</code> fails, see <a href="https://docs.byteplus.com/en/docs/directconnect/Direct-Connect-gateway#.5bey5a6M5oiQ5LqR5LiK5LqR5LiL6YWN572u77yM5L2G572R57uc5LuN54S25LiN6YCa77yM5aaC5L2V5o6S5p-l77yf">Cloud\-to\-on\-premises configuration is complete, but the network is still not connected. How do I troubleshoot</a>.</div>


<span id=".5q2l6aqk5LqM77ya6YWN572u56eB572RTkFU572R5YWz"></span>
### Step 2: Configure the VPC NAT Gateway

<span id=".5Yib5bu656eB572RTkFU572R5YWz"></span>
#### 1. Create a VPC NAT Gateway

You can refer to this operation to create a VPC NAT Gateway.


1. Log in to the [VPC NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. Click **Create VPC NAT Gateway**.

4. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Billing method |Only supports pay\-as\-you\-go. |Pay\-as\-you\-go |
   |Regions |Select the region where the VPC NAT Gateway resides. |China (Beijing) |
   |Name |Enter the name of the VPC NAT Gateway. |VPC NAT Gateway\-A |
   |VPC |Select the VPC to which the VPC NAT Gateway belongs from the dropdown menu. |VPC\-A\|192.168.0.0/16 |
   |Subnet |Select a subnet from the dropdown list. Select the subnet where the IP address communicating with the data center is located. |subnet\-A100\|192.168.100.0/24 |
   |Specification |No specification required. |\- |
   |Affiliated project |Select the project to which the VPC NAT Gateway belongs. |default |
   |Tags |Add one or more user tags to the VPC NAT Gateway as needed. |nat:v1 |
   

5. Click **Confirm order**.

6. Follow the console guidance to review and accept Legal, and click **Buy now** to complete the operation.


<span id=".5re75Yqg5Lit6L2sSVA="></span>
#### 2. Add a NAT IP

You can refer to this operation to add a specified IP address as a NAT IP, which will be used later to communicate with the on\-premises data center.


1. In the VPC NAT Gateway list, click **Configure NAT IP** on the right side of VPC NAT Gateway\-A.

2. In the NAT IP tab, click **Add NAT IP**.

3. Enter the NAT IP name: nat\-ip\-x, select manual assignment, and enter the target private IP address (e.g., 192.168.100.66).

4. Click **Add** to complete the action.


<span id=".5Yib5bu6U05BVOinhOWImQ=="></span>
#### Create a SNAT rule


1. In the VPC NAT Gateway list, click the name of VPC NAT Gateway\-A.

2. Select the **SNAT rules** tab, then click **Create SNAT rule**.

3. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Name |Set the name of the SNAT rule. |SNAT\-X |
   |granularity |Select the granularity of the SNAT rule. |Subnet<br><br>192.168.1.0/24 |
   |NAT IP |Select the NAT IP address for the VPC NAT Gateway. |192.168.100.66\|nat\-ip\-x |
   

4. Click **OK** to complete the action.


<span id=".5Yib5bu6RE5BVOinhOWImQ=="></span>
#### Create DNAT rule


1. In the VPC NAT Gateway list, click the ellipsis icon \> Configure DNAT rule on the right side of VPC NAT Gateway\-A

2. On the DNAT entry tab, click Create DNAT entry

3. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Name |Enter the name of the DNAT rule. |dnat\-1 |
   |Agreement |Select protocol type. Supported protocols include TCP, UDP. |TCP |
   |Local IP and its port |Set the private IP address and port of the ECS instance. |192.168.2.20<br><br>22 |
   |NAT IP and port |Set the transit IP and its port for the VPC NAT Gateway. |nat\-ip\-x<br><br>22 |
   

4. Click **OK** to complete the action.

5. After creating the DNAT rule, you also need to allow the corresponding security group rule within VPC\-A.

   1. Log in to the[ ECS console](https://console.byteplus.com/ecs/instance).

   2. Click the ECS instance name, select the Security Group tab, and click the security group name.

   3. On the **Access rules \> Inbound** tab, add a rule. Set policy to Allow, protocol type to TCP/UDP, port range to Local IP ports, and source address to 0.0.0.0/0. For more details, see [Security Group overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview).


<span id=".5q2l6aqk5LiJ77ya6YWN572u6Lev55Sx"></span>
### Step 3: Configuring routing

<span id=".5YeG5aSH6Lev55Sx6KGo"></span>
#### 1. Prepare the route table

Create one custom route table and associate it with the subnet where the VPC NAT Gateway is located. The VPC NAT Gateway will route traffic to the CEN through the route table associated with its subnet.


1. Log in to the[ Route Table console](https://console.byteplus.com/vpc/routeTable).

2. In the top menu bar, select the Target Region and project. This example uses China (Beijing) and Default.

3. Click **Create Route Table**.

4. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Name |Enter the name of custom route table. |route\-X |
   |VPC |Select the VPC for the route table. |VPC\-A |
   

5. Click **Create** to complete configuration.

6. In the route table list, click **Associate Subnet** next to the newly created custom route table route\-X.

7. Select Subnet\-A100, and click **Associate** to complete the attachment.


<span id=".5rWB6YeP6Lev55Sx5Yiw56eB572RTkFU572R5YWz"></span>
#### 2. Route traffic to the VPC NAT Gateway

Since the Direct Connect (DC) Gateway is loaded into the CEN during preparations, the system route table automatically adds a route entry with destination CIDR block 172.16.1.0/24 and next hop as the CEN. You need to detach the DC Gateway to delete this route before adding a route with destination CIDR block 172.16.1.0/24 and next hop as the VPC NAT Gateway.

**3. Detach the network instance**


1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the top menu bar, select the target project.

3. Click the target CEN instance name.

4. Select the network instance tab and click **Detach** next to the target network instance list.

5. Click **Detach** to complete the action.


After detaching, VPC\-A's system route table no longer contains a route entry with the destination CIDR block 172.16.1.0/24.

**4. Add a route for the VPC NAT Gateway**


1. Log in to the[ Route Table console](https://console.byteplus.com/vpc/routeTable).

2. In the top menu bar, select the Target Region and project. This example uses China (Beijing) and Default.

3. In the route table list, click the system route table name of VPC\-A.

4. Select **Route entry \> Custom route** tab, and click **Add route**.

5. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Destination CIDR |Enter the subnet segment of the on\-premises data center. |172.16.1.0/24 |
   |Next Hop type |Select the Next Hop type. |NAT Gateway |
   |Next Hop |Select the next hop resource. |VPC NAT Gateway\-A |
   

6. Click **Create** to complete configuration.


<span id=".5rWB6YeP6Lev55Sx5Yiw5LqR5LyB5Lia572R"></span>
#### 5. Route traffic to CEN

Reload the DC Gateway to CEN (CEN). The custom route table route\-X automatically adds a route entry to CEN, routing VPC NAT Gateway traffic to CEN.

The destination CIDR 172.16.1.0/24 conflicts with the VPC NAT Gateway route in the system route table, so it will not be added.


1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the top menu bar, select the target project.

3. Click the target CEN instance name.

4. Select the Network Instances tab, then click to install network instances.

5. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Account |Select the account to which the DC Gateway belongs. |My account |
   |Regions |Select the region where the DC Gateway is located. |China (Beijing) |
   |Instance type |Select VPC type. |DC Gateway |
   |Network Instances |Select the DC Gateway based on the project filter. |dcg\-01 |
   

6. Click **Install** to complete the action.


In addition to the system default route entries, the system route table and custom route table contain route entries.


|Route table name |Associate a subnet |Destination CIDR |Next Hop |
|---|---|---|---|
|System route table for VPC\-A |Subnet\-A1 |172.16.1.0/24 |VPC NAT Gateway\-A |
|Custom route table of VPC\-A |Subnet\-A2 |172.16.1.0/24 |CEN\-X |


<span id=".5q2l6aqk5Zub77ya6aqM6K-B"></span>
### Step 4: Verification


<Tabs>
<Tab zoneid="KeJuNEOjet" title="Verify the SNAT entry">
<TabTitle>Verify the SNAT entry</TabTitle>

1. Log in to ECS\-A1 (192.168.1.10) and run the command `ping <Server A's IP address>`. This article runs `ping 172.16.1.10`.

2. If the `ping` succeeds, ECS\-A1 can access Server A through the VPC NAT Gateway's NAT IP address (192.168.100.66). If the `ping` fails, check the SNAT entry and related route configuration.


</Tab>
<Tab zoneid="ImCsVGbXxP" title="Verify the DNAT entry">
<TabTitle>Verify the DNAT entry</TabTitle>

1. Log in to on\-premises data center server A (172.16.1.10), then enter `ssh <NAT IP address of the DNAT entry> -p <NAT IP port of the DNAT entry>` in the command line. This article uses `ssh 192.168.100.66 -p 22`.

2. If the login page appears, it means server A in the on\-premises data center can access ECS\-A2. If the login page does not appear, check the DNAT entry, related route configuration, and whether the security group allows traffic.


</Tab>
</Tabs>


<span id=".6aqM6K-BU05BVOinhOWImQ=="></span>
####
