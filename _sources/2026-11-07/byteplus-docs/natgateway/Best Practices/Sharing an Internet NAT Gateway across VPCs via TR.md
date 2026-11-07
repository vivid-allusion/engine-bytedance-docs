---
title: "Sharing an Internet NAT Gateway across VPCs via TR"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Configuring-multiple-VPCs-to-share-an-Internet-NAT-Gateway-using-TR"
---

When multiple Virtual Private Clouds (VPCs) require internet access, you can configure a single Internet NAT Gateway for these VPCs to conserve Elastic IP Address (EIP) resources and reduce enterprise costs. This topic describes how to use Transit Router (TR) to enable multiple VPCs to share a single NAT Gateway for internet access.

<span id=".6IOM5pmv5LuL57uN"></span>
## Background

A company's business is deployed across three VPCs. As shown in the figure below, VPC\-A and VPC\-C share an Internet NAT Gateway, while VPC\-B does not use an Internet NAT Gateway.


* The CIDR block of VPC\-A is 172.16.0.0/16, and its Subnet\-A has the CIDR block 172.16.1.0/24.

* The CIDR block of VPC\-B is 192.168.0.0/16, and its Subnet\-B has the CIDR block 192.168.1.0/24.

* The CIDR block of VPC\-C is 10.0.0.0/16, and its Subnet\-C has the CIDR block 10.0.1.0/24.

* VPC\-A and VPC\-B can communicate with VPC\-C respectively, but VPC\-A and VPC\-B are isolated from each other.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_36e526f42beec42558e6516c46cbb054.png) </span>

The diagram above illustrates a single SNAT rule. In practice, you can create multiple SNAT and DNAT rules as needed.

ECS\-A can access the internet through the SNAT rule of Internet NAT Gateway NAT\-X.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Complete the following steps based on the background information before proceeding:


* Using the same BytePlus account, create three VPCs (the region is China (Beijing) in this example), ensuring the VPC parameters match those in the background introduction. For specific actions, see [Creating a Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* Create Elastic Compute Service (ECS) instances in each VPC subnet as follows, all without EIP addresses:​​​​ VPC\-A:​​ In Subnet\-A, create ​​ECS\-A​​ with private IP 172.16.1.11​​; VPC\-B:​​ In Subnet\-B, create ​​ECS\-B​​ with private IP 192.168.1.22​​; VPC\-C:​​ In Subnet\-C, create ​​ECS\-C​​ with private IP 10.0.1.33. For more information, see [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* Apply for one EIP not associated with any cloud resources. This example uses EIP\-X (180.XX.XX.44). For procedure, see [Applying for an EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5Lit6L2s6Lev55Sx5Zmo"></span>
### Step 1: Configure the Transit Router (TR)

Create a Transit Router instance and configure the relevant routes to enable communication between VPC\-A/VPC\-B and VPC\-C, while maintaining isolation between VPC\-A and VPC\-B.

This topic uses multiple VPCs under the same account and in the same region. You can refer to the following configuration steps, or see [Implementing private network interconnection and isolation between different VPCs (same account, same region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-02).

In actual usage, the following situations may exist:


* For multiple VPCs under the same account but in different regions, see [Implementing private network interconnection and isolation between different VPCs (same account, cross-region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-03).

* For multiple VPCs under different accounts but in the same region, see [Implementing private network interconnection and isolation between different VPCs (cross-account, same region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-04).

* For VPC\-A and VPC\-B under different accounts and in different regions, the operational procedure follows the same principles as [Implementing private network interconnection and isolation between different VPCs (same account, cross-region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-03) and [Implementing private network interconnection and isolation between different VPCs (cross-account, same region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-04).


<span id=".5Yib5bu65Lit6L2s6Lev55Sx5Zmo5a6e5L6L5Y-K5YW26Lev55Sx6KGo"></span>
#### Create TR instance and its route table


1. Log in to the [Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. In the left\-side navigation pane, click **Transit Router**, and enter the Transit Router console.

3. Click **Create TR**.

4. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Regions |Select the region for the Transit Router (TR) instance.​​ |China (Beijing) |
   |Name |Enter the name of the Transit Router instance. |TR\-X |
   |Project |Select the project for the Transit Router. |default |
   |Tags |Add one or more user tags to the Transit Router as needed. |No tags added |
   

4. Click **Create** to complete the creation of the TR instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Upon successful creation, the system automatically generates a default TR route table. Record its name. Take RouteTable\-default as an example.   </div>
   

5. On the Transit Router instances page, click the name of your target TR instance.

6. Select the **Route table** tab, then click **Create Route Table** next to the TR route table list.

7. Type the custom route table name: R\-Table\-X. Click **Create** to complete the custom TR route table creation.


<span id=".5Yib5bu6572R57uc5a6e5L6L6L-e5o6l"></span>
#### Create attachment

Follow the steps below to create ​​3 network instance connections​​ sequentially. Configure these connections using the parameters shown in ​​Configuration Example 1​​, ​​Configuration Example 2​​, and ​​Configuration Example 3​​ from the parameter table, respectively.


1. On the Transit Router instances page, click the name of your target TR instance.

2. On the **Intra\-region attachments** tab, click **Create attachment**.

3. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example value 1 |Example value 2 |Example value 3 |
   |---|---|---|---|---|
   |Transit Router |Default: The Transit Router instance you selected.​​ |TR\-X |TR\-X |TR\-X |
   |Regions |Default: Same as the region where the TR instance resides. |China (Beijing) |China (Beijing) |China (Beijing) |
   |Name |The name of the network instance attachment to be created. |Attach\-VPC\-A |Attach\-VPC\-B |Attach\-VPC\-C |
   |Network instance type |Select the type for the network instance attachment to be created. |VPC |VPC |VPC |
   |VPC |Select the VPC instance to be attached. |VPC\-A |VPC\-B |VPC\-C |
   |AZs and Subnets |Select the subnet in the Availability Zone where the attachment point resides. The subnet assigns a private IP address to the network interface of the attachment.​​ |Availability Zone A, Subnet\-A |Availability Zone A, Subnet\-B |Availability Zone A, Subnet\-C |
   |Associated forwarding |Enable association forwarding and select the destination Transit Router (TR) route table. When enabled, traffic originating from this network attachment will be forwarded based on the routing entries in its associated Transit Router (TR) route table.​​ |Enable; RouteTable\-default |Enable; RouteTable\-default |Enable; R\-Table\-X |
   |Route propagation |Enable route propagation and select the destination Transit Router (TR) route table. When enabled, the specified Transit Router (TR) route table automatically creates routing entries with destination CIDRs set to the subnets of the attached VPC, using the network attachment itself as the next hop.​​ |Enable; R\-Table\-X |Enable; R\-Table\-X |Enable; RouteTable\-default |
   

4. Click **Buy now** to complete the action.


At this point, the routing entries and association status for the two TR route tables are as follows:


|TR route table name |Destination CIDR |Next Hop |Associated forwarding |Description |
|---|---|---|---|---|
|RouteTable\-default |10.0.1.0/24 |Attach\-VPC\-C |Attach\-VPC\-A, Attach\-VPC\-B |Traffic destined for 10.0.1.0/24 received by the Transit Router from Attach\-VPC\-A and Attach\-VPC\-B will be forwarded to Attach\-VPC\-C. |
|R\-Table\-X |172.16.1.0/24 |Attach\-VPC\-A |Attach\-VPC\-C |The Transit Router will forward traffic destined for 172.16.1.0/24 received through Attach\-VPC\-C to Attach\-VPC\-A. |
||192.168.1.0/24 |Attach\-VPC\-B ||The Transit Router will forward traffic destined for 192.168.1.0/24 received through Attach\-VPC\-C to Attach\-VPC\-B. |


<span id=".6YWN572uVlBD6Lev55Sx6KGo"></span>
#### Configure a VPC route table


1. Log in to the [Route Table console](https://console.byteplus.com/vpc/routeTable).

2. In the left\-side navigation pane, click "Route table" to access the route table console. In the top menu bar, select the project and region.

3. In the route table list, search for the route tables using the target VPC IDs.

4. Click the target route table name.

5. On the **Route Entry \> Custom route** tab, click **Add route**.

   * Refer to the table below and add the following custom routes to the route tables of both VPC\-A and VPC\-B.

      
      |Parameter |Description |Example |
      |---|---|---|
      |Destination CIDR |Specify the CIDR block of VPC\-C. |10.0.0.0/16 |
      |Next Hop type |Select the Next Hop Resource Type for the route entry, which directs traffic destined for the destination CIDR block to the specified resource. |Transit Router |
      |Next Hop |Specify the specific resource for next hop. |TR\-X |
      

      After configuration, traffic from resources in VPC\-A and VPC\-B destined for 10.0.0.0/16 (VPC\-C) will be routed to Transit Router TR\-X.

   * Refer to the table below and add the following two custom routes to the route table of VPC\-C.

      
      |Parameter |Description |Example value 1 |Example value 2 |
      |---|---|---|---|
      |Destination CIDR |Specify the CIDR blocks of VPC\-A and VPC\-B respectively. |172.16.0.0/16 |192.168.0.0/16 |
      |Next Hop type |Select the Next Hop Resource Type for the route entry, which directs traffic destined for the destination CIDR block to the specified resource. |Transit Router |Transit Router |
      |Next Hop |Specify the specific resource for next hop. |TR\-X |TR\-X |
      

      After configuration, traffic from resources in VPC\-C destined for 172.16.0.0/16 (VPC\-A) and 192.168.0.0/16 (VPC\-B) will be routed to Transit Router TR\-X.

6. Click **Add** to complete the route configuration.

7. Verification. The following steps use Linux ECS as an example:

   1. Log in to the VPC\-A ECS instance ECS\-A (172.16.1.11). Verify whether it can communicate with the ECS\-B and ECS\-C in VPC\-B and VPC\-C by executing `ping 192.168.1.22` and `ping 10.0.1.33` in the command line. Expected results:

      * ECS instances in VPC\-A are isolated from those in VPC\-B, meaning ECS\-A and ECS\-B should not be able to ping each other.

      * ECS instances in VPC\-A can communicate with those in VPC\-C, meaning ECS\-A and ECS\-C should be able to ping each other.

   2. Similarly, log in to the ECS instances in VPC\-B and VPC\-C to verify the connectivity and isolation between VPC\-A, VPC\-B, and VPC\-C.


<span id=".5q2l6aqk5LqM77ya6YWN572u5YWs572RTkFU572R5YWz"></span>
### Step 2: Configure Internet NAT gateway

Through the following steps, you can create an Internet NAT Gateway in all\-pass mode within the VPC\-C.


1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select the target region and project. In this example, they are **China (Beijing)**  and **default**.

3. Click **Create NAT Gateway**.

4. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example value |
   |---|---|---|
   |Billing method |Supports pay\-as\-you\-go and subscription. |Pay\-as\-you\-go |
   |Regions |Select the region where the internet NAT gateway is located. |China (Beijing) |
   |Name |Set a name for the Internet NAT gateway. |NAT\-X |
   |Metering method |When the billing method is **Pay\-as\-you\-go**, select a metering method for the Internet NAT gateway. Supports [Pay-by-specification](https://docs.byteplus.com/en/docs/natgateway/Pay-as-you-go) and [Pay-by-CU](https://docs.byteplus.com/en/docs/natgateway/Pay-by-CU).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The metering method defaults to Pay\-by\-specification.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">With Pay\-by\-CU, you don't need to specify a specification. Performance scales dynamically based on demand, making it ideal for scenarios with significant traffic fluctuations.</div><br> |Pay\-by\-specification |
   |Specification |Select the specification of the Internet NAT gateway. |Small |
   |VPC |Select a VPC. |VPC\-C\|10.0.0.0/16 |
   |Subnet |Select a subnet from the dropdown list. |Subnet\-C \| 10.0.1.0/24 |
   |Project |Select the project to which the internet NAT gateway belongs as needed. |default |
   |Configuration mode |When the billing method is **Pay\-as\-you\-go**, select the configuration method for the Internet NAT Gateway.<br><br><br>* Manual configuration: After creation, you must manually associate an EIP and configure SNAT or DNAT entries.<br><br>* Auto\-configure (all\-pass mode): Automatically creates a 0.0.0.0/0 SNAT rule. |Automatic configuration (all\-pass mode) |
   |Gateway mode |Select the mode of the Internet NAT Gateway\-According to your networking scenario. The mode of an Internet NAT Gateway cannot be changed after creation. Proceed with caution.<br><br><br>* Internet egress is an IPv4 Gateway: Please select **Non\-passthrough mode.** <br><br>* Internet egress is an EIP: Please select **Pass\-through mode.**  |Pass\-through mode |
   |EIP |When the configuration method is set to **Automatic configuration**, select an EIP from the drop\-down list |EIP\-X |
   |Tags |Add one or more user tags to the Internet NAT gateway as needed. |No tags added |
   

5. Click **Confirm order**.

6. Follow the console guidance to review and accept Legal, and click **Buy now** to complete the operation.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the creation failed, see <a href="https://docs.byteplus.com/en/docs/natgateway/NAT-gateway-FAQ#.5Yib5bu65YWs572RTkFU572R5YWz5aSx6LSl5piv5LuA5LmI5Y6f5Zug77yf">Why did the Internet NAT Gateway creation fail</a>.   </div>
   

<span id=".5q2l6aqk5LiJ77ya6YWN572uTkFU572R5YWz55u45YWz6Lev55Sx"></span>
### Step 3: Configure NAT Gateway related routes

<span id=".6YWN572uVFLot6_nlLHooag="></span>
#### Configure TR route table


1. Log in to the [Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. In the left\-side navigation pane, click **Transit Router**, and enter the Transit Router console.

2. Click the name of the target TR instance.

3. Select the **Route table** tab, check the TR system route table RouteTable\-default, and the TR route table details page will display on the right.

4. On the **Route entry** tab, click **Create static route**.

5. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Route name |Enter the name of static route. |NAT\-Gateway |
   |Destination CIDR |Enter the destination CIDR block for the static route. |0.0.0.0/0 |
   |Blackhole routing |Choose whether the static route is a blackhole route. |None |
   |Next Hop |Select the attachment as the next hop. |Attach\-VPC\-C |
   

6. Click **Create** to complete the action.


<span id=".6YWN572uVlBD6Lev55Sx6KGo"></span>
#### Configure a VPC route table


1. Log in to the [Route Table console](https://console.byteplus.com/vpc/routeTable).

3. In the top menu bar, select the target project and region.

4. In the route table list, click the route table name of the VPC\-A.

5. On the **Route Entry \> Custom route** tab, click **Add route**.

6. To configure the related parameters, see the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Destination CIDR |Set the destination CIDR block for traffic routing. |0.0.0.0/0 |
   |Next Hop type |Select a resource type for the next hop of the route entry |Transit Router |
   |Next Hop |Select resources from the drop\-down menu based on the next hop type. |TR\-X |
   

6. Click **Create** to complete configuration.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If VPC\-B also needs to use an Internet NAT Gateway for internet access, you can choose from the following options as needed:</div>



* <div data-tips="true" data-tips-type="tip">Option 1: Add a route entry in VPC\-B's route table with the destination CIDR block 0.0.0.0/0 and the next hop TR\-X. In this case, both VPC\-A and VPC\-B share VPC\-C's Internet NAT Gateway for internet access. However, VPC\-A, VPC\-B, and VPC\-C are now interconnected, meaning VPC\-A and VPC\-B are no longer isolated from each other. You can use Network ACLs or Security Groups to control the traffic between VPC\-A and VPC\-B.</div>


* <div data-tips="true" data-tips-type="tip">Option 2: Create a separate Internet NAT Gateway in VPC\-B. This ensures that VPC\-A and VPC\-B remain isolated from each other.</div>



<span id=".5q2l6aqk5Zub77ya6aqM6K-B"></span>
### Step 4: Verification

Log in to ECS\-A (172.16.1.11) in VPC\-A, and execute `ping 114.114.114.114` in the command line.

If the `ping` is successful, it indicates that ECS\-A in VPC\-A can access the internet through VPC\-C Internet NAT Gateway, meaning VPC\-A ECSs can share VPC\-C Internet NAT Gateway.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the <code>ping</code> fails, see <a href="https://docs.byteplus.com/en/docs/natgateway/SNAT-entry-FAQ#.5bey6YWN572uU05BVOinhOWImeeahOS6keacjeWKoeWZqOaXoOazleiuv-mXruWFrOe9ke-8nw==">Why cannot Elastic Compute Service instances configured with SNAT entries be accessed over the internet</a>.</div>
