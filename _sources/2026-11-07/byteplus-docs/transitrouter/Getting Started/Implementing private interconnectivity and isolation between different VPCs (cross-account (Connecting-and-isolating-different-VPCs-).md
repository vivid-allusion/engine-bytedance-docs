---
title: "Implementing private interconnectivity and isolation between different VPCs (cross-account, cross-region)"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Connecting-and-isolating-different-VPCs-across-accounts-and-Regions"
---

This section describes how to use Transit Routers (TRs) to implement interconnectivity between two VPCs (vpc01 and vpc02) and another VPC (vpc03) in different accounts and regions. After connecting, both vpc01 and vpc02 can communicate with vpc03 via the TR, but vpc01 and vpc02 cannot mutually communicate, as shown below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9597aa0681463d65bc34de86242329a9.png) </span>

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created three Virtual Private Clouds (VPCs) and their subnets. For procedure, see [Building an IPv4 VPC](https://docs.byteplus.com/en/docs/vpc/Building-an-IPv4-VPC).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Ensure that neither VPC contains conflicting subnets. That is, no duplicate or overlapping CIDR blocks exist.   </div>
   

* You have created Elastic Compute Service (ECS) instances in the three VPCs. For procedure, see [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id=".6Lev55Sx6KeE5YiS"></span>
## Routing planning

In a single TR instance, multiple network instances with the identical access destination can use the same TR route table to forward traffic.


* Within China (Guangzhou): Since both vpc01 and vpc02 only need to access vpc03, their traffic can share a single TR route table. However, the inter\-region attachment requires access to distinct destinations (both vpc01 and vpc02). Therefore, a separate TR route table is required to handle this traffic.

* Within China (Beijing): vpc03 and the inter\-region attachment require access to the same destinations (both vpc01 and vpc02). So only one TR route table is required.


In summary, at least three TR route tables are required to enable connectivity and isolation between different VPCs. The following figure illustrates the specific route planning.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0102253b417c64d5a66236232ff7be7.png) </span>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Routes in the VPC route tables illustrated above can be manually configured or automatically published. This example uses auto publishing.</div>


<span id=".6YWN572u5rWB56iL"></span>
## Configuration procedures


1. [Configure a TR instance in China (Guangzhou) (Account A)](https://docs.byteplus.com/docs/transitrouter/Connecting-and-isolating-different-VPCs-across-accounts-and-Regions): Use Account A to create a TR instance in China (Guangzhou), and create network instance attachments that connect to vpc01 and vpc02 respectively.

   1. **Create a TR instance**: Create a TR instance in China (Guangzhou).

   2. **Create a TR custom route table**: Create a custom route table for the TR instance to receive and forward network traffic along with the TR system route table.

   3. **Create a network instance attachment and configure routing**: Create two network instance attachments on the TR instance to connect the two VPCs in this region. On the TR side, configure association forwarding and route learning to control the traffic flow to and from these VPCs. On the VPC side, configure auto publishing to control flow direction.

   4. **View TR and VPC routes**: Check that the routes of the TR instance and two VPCs in the same region meet expectations.

2. [Configure a TR instance in China (Beijing) (Account A)](https://docs.byteplus.com/docs/transitrouter/Connecting-and-isolating-different-VPCs-across-accounts-and-Regions): Use Account A to create a TR instance in China (Beijing) and share it with Account B.

   1. **Create a TR instance**: Create a TR instance in China (Beijing).

   2. **Create instance sharing**: Create a sharing unit for the TR instance in China (Beijing) and share it with Account B.

3. [Accept the sharing invitation (Account B)](https://docs.byteplus.com/docs/transitrouter/Connecting-and-isolating-different-VPCs-across-accounts-and-Regions): Use Account B to accept the TR instance shared by Account A.

4. [Create a network instance attachment and configuring routing (Account B)](https://docs.byteplus.com/docs/transitrouter/Connecting-and-isolating-different-VPCs-across-accounts-and-Regions): Use Account B to create a network instance attachment on the shared TR instance, connecting the shared TR instance to vpc03 under my account. On the TR side, configure association forwarding and route learning to control the traffic flow to and from these VPCs. On the VPC side, configure auto publishing to control flow direction.

5. [Configure cross-region bandwidth (Account A)](https://docs.byteplus.com/docs/transitrouter/Connecting-and-isolating-different-VPCs-across-accounts-and-Regions): Create an inter\-region attachment to connect TR instances between regions.

   1. **Create a bandwidth package**: Create a bandwidth package to provide bandwidth resources for the inter\-region attachment.

   2. **Create an inter\-region attachment and configure routing**: Create an inter\-region attachment to connect the TR instances in the two regions above. Allocate bandwidth for the attachment. Configure association forwarding and route learning to implement route propagation between the two TR instances.

   3. **View TR and VPC routes**: Check that the routes of two TR instances in different regions and two VPCs under Account A meet expectations.

6. [View VPC routes (Account B)](https://docs.byteplus.com/docs/transitrouter/Connecting-and-isolating-different-VPCs-across-accounts-and-Regions): Use Account B to check that the route entries in the route table of vpc03 meet expectations.

7. [Verification](https://docs.byteplus.com/docs/transitrouter/Connecting-and-isolating-different-VPCs-across-accounts-and-Regions#.57uT5p6c6aqM6K-B): Run `ping` to verify the connectivity between ECS instances in different VPCs to ensure that the VPCs are connected and isolated as expected.


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedures

<span id=".5q2l6aqk5LiA77ya6YWN572u5Y2O5Y2XMe-8iOW5v-W3nu-8ieWcsOWfn-S4reeahFRS5a6e5L6L77yI6LSm5Y-3Qe-8iQ=="></span>
### Step 1: Configure a TR instance in China (Guangzhou) (Account A)

<span id=".5LiA44CB5Yib5bu6VFLlrp7kvos="></span>
#### I. Create a TR instance


1. Use Account A to log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter). 

2. In the top menu bar, select the target project and region.

3. Click **Create TR** and configure related parameters based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Region |Select a region closer to your service for shorter network delays and faster access. Cloud resources in different regions are isolated by default on private networks. |China (Guangzhou) |
   |Name |Type in the name for the TR instance to be created. |tr01 |
   |ASN |Specify a BGP ASN (Autonomous System Number) for the TR instance. Valid range: 64512\-65534 or 4200000000\-4294967294. Assign different ASNs for TR instances in different regions.<br><br>The TR automatically prepends its ASN to the AsPath attribute of routes published to other network instances. |64512 |
   |Multicast |Specify whether to enable multicast for the TR. [Learn more](https://docs.byteplus.com/docs/transitrouter/Multicast-Overview) |Disabled |
   |Affiliated Project |Select the project to which the TR instance belongs. |default |
   |Agreement |Follow the console guidance to review and accept the legal terms. |Check |
   

4. Click **Create** to complete the creation of the TR instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When you create a TR instance, the system automatically creates a system route table for it. Record the name of this system route table: tr01\-rtb\-sys. The following uses tr01\-rtb\-sys as an example.   </div>
   

<span id=".5LqM44CB5Yib5bu6VFLoh6rlrprkuYnot6_nlLHooag="></span>
#### Ⅱ. Create a TR custom route table


1. Click the name of the created TR instance.

2. In the zone below **Basic information**, select the **Route Table** tab.

3. Click **Create Route Table** to the right of the Route Table List, and type in tr01\-rtb\-set as the route table's name.

4. Click **Create** to complete the creation of the TR route table.


<span id=".5LiJ44CB5Yib5bu6572R57uc5a6e5L6L6L-e5o6l5bm26YWN572u6Lev55Sx"></span>
#### Ⅲ. Create a network instance attachment and configure routing

Create two network instance attachments to connect to vpc01 and vpc02 separately by the following steps.


1. In the section below **Basic information**, select the **Intra\-region attachments** tab.

2. Click **Create attachment**, and complete the basic configuration for the network instance attachment based on the table below.

   
   |Parameter |Description |Example value (Attach vpc01) |Example value (Attach vpc02) |
   |---|---|---|---|
   |**Basic information** ||||
   |TR |Defaults to the selected TR instance, requiring no manual configuration. |tr01 |tr01 |
   |Region |Defaults to the same region as the TR instance. No manual configuration required. |China (Guangzhou) |China (Guangzhou) |
   |Name |The name of the network instance attachment to be created. |attach\-vpc01 |attach\-vpc02 |
   |**Instance** ||||
   |Attachment type |Select the type for the network instance attachment to be created. |VPC |VPC |
   |VPC |Select the VPC instance to be connected. |vpc01 |vpc02 |
   |**Attachment point configuration** ||||
   |Availability Zone and Subnet |Select the entry point where TR connects to the VPC. Select the availability zone and then the subnet, and set the selected availability zone as the default availability zone. |Availability Zone A, subnet01 |Availability Zone A, subnet02 |
   

3. Complete the route configuration for the network instance attachment based on the table below.

   
   |Parameter |Description |Example value (Attach vpc01) |Example value (Attach vpc02) |
   |---|---|---|---|
   |Association forwarding |The TR will forward traffic from the related network instance based on the route table associated with this network instance attachment.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Take attach\-vpc01 as an example. The TR forwards traffic from vpc01 based on tr01\-rtb\-sys.</div><br><br><br> |Enabled, tr01\-rtb\-sys |Enabled, tr01\-rtb\-sys |
   |Route learning |The selected TR route table automatically learns the routes of the network instance and generates routes whose next hop is the corresponding network instance attachment.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Take attach\-vpc01 as an example. After enabling route learning, the TR route table (tr01\-rtb\-set) automatically generates routes whose destinations are vpc01 subnets and the next hop is attach\-vpc01.</div><br><br><br> |Enabled, tr01\-rtb\-set |Enabled, tr01\-rtb\-set |
   |Auto Publish Route |Enabling auto publishing will automatically synchronize routes from the TR route table associated with this network instance attachment to all route tables within the VPC. These synchronized routes are marked as system routes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Take attach\-vpc01 as an example. After enabling auto publishing, the system automatically synchronizes the routes from tr01\-rtb\-sys to all route tables within vpc01. These synchronized routes are system routes.</div><br><br><br> |Enabled |Enabled |
   

4. Click **Buy now** to complete the action.


<span id=".5Zub44CB5p-l55yLVFLlkoxWUEPot6_nlLE="></span>
#### IV. View TR and VPC routes


1. View routes of TR route tables (tr01\-rtb\-sys and tr01\-rtb\-set) in sequence.

   * Currently, no routes exist in tr01\-rtb\-sys.

   * The routes in tr01\-rtb\-set are listed in the following table.

      
      |Destination CIDR |Next Hop |Status |Route type |Attachment type |Instance |
      |---|---|---|---|---|---|
      |192.168.16.0/24 |attach\-vpc02 |Available |Route learning |VPC |vpc02 |
      |192.168.0.0/24 |attach\-vpc01 |Available |Route learning |VPC |vpc01 |
      

2. View routes of the vpc01 and vpc02 route tables in sequence to confirm no changes.

   Since the routes in tr01\-rtb\-sys are automatically published to the vpc01 and vpc02 route tables, routes in the vpc01 and vpc02 route tables are unchanged.


<span id=".5q2l6aqk5LqM77ya6YWN572u5Y2O5YyXMu-8iOWMl-S6rO-8ieWcsOWfn-S4reeahFRS5a6e5L6L77yI6LSm5Y-3Qe-8iQ=="></span>
### Step 2: Configure a TR instance in China (Beijing) (Account A)

<span id=".5LiA44CB5Yib5bu6VFLlrp7kvos="></span>
#### I. Create a TR instance


1. Back to the TR Instances page, and select the target project and region in the top menu bar.

2. Click **Create TR** and configure related parameters based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Region |Select a region closer to your service for shorter network delays and faster access. Cloud resources in different regions are isolated by default on private networks. |China (Beijing) |
   |Name |Type the name for the TR instance to be created. |tr02 |
   |ASN |Specify a BGP ASN for the TR instance. Valid range: 64512\-65534 or 4200000000\-4294967294. Assign different ASNs for TR instances in different regions.<br><br>The TR automatically prepends its ASN to the AsPath attribute of routes published to other network instances. |64513 |
   |Multicast |Specify whether to enable multicast for the TR. [Learn more](https://docs.byteplus.com/docs/transitrouter/Multicast-Overview) |Disable |
   |Affiliated Project |Select the project to which the TR instance belongs. |default |
   |Agreement |Follow the console guidance to review and accept the legal terms. |Checke |
   

3. Click **Create** to complete the creation of the TR instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When you create a TR instance, the system automatically creates a system route table for it. Record the name of this system route table: tr02\-rtb\-sys. The following uses tr02\-rtb\-sys as an example.   </div>
   

<span id=".5LqM44CB5Yib5bu65a6e5L6L5YWx5Lqr"></span>
#### II. Create instance sharing


1. Click the account avatar in the upper right corner.

2. Select **Tools \> Resource**.

3. In the left\-side navigation pane, select **Resource sharing \> Shared by me**.

4. In the top menu bar, select your target region.

5. On the **Shared unit** tab, click **Create shared unit** and configure the parameters based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Unit name |Type a name for the shared unit that is easy to identify. |Share TR |
   |Region |Region defaults to the region selected in the top menu bar. To modify, reselect the region in the top menu bar. |China (Beijing) |
   |product |Select the Transit Router \- TR instance. |Transit Router \- TR instance. |
   |Resource ID |Type in the ID of the TR to be shared, then search and check it. |Select the Transit Router (tr01) |
   

6. Click **Next** to associate sharing permissions.

   TR sharing permissions are system\-defined and cannot be modified. For default supported actions, see [Instructions](https://docs.byteplus.com/docs/transitrouter/Cross-account-Sharing-overview#T39M302D).

7. Click **Next** to associate shared users.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Resource user |Choose a method for resource sharing.<br><br><br>* **Allow sharing with any account**: Share the TR with any BytePlus root account.<br><br>* **Only allow sharing with enterprises and organizations**: Share the TR only with BytePlus root accounts in the same enterprise organization. |Allow sharing with any account |
   |User type |Select the root account. |Account |
   |User ID |Type the ID of Account B. |2100\*\*\*\*25 |
   

8. Click **Next** to confirm that the resources, associated permissions, and shared users are correct.

9. Click **Confirm** to complete the action.


<span id=".5q2l6aqk5LiJ77ya5o6l5Y-X5a6e5L6L5YWx5Lqr77yI6LSm5Y-3Qu-8iQ=="></span>
### Step 3: Accept sharing invitation (Account B)


1. Use Account B to log in to [the Resource management console](https://console.byteplus.com/resourcemanager/region:resource-manager+cn-beijing/resource_share/shared).

2. In the top menu bar, select the region to which the shared TR belongs.

3. Click **Accept** to the right of the shared unit to complete the action.

4. Click **Accept** to the right of the shared TR instance to confirm the sharing information.

5. Click **Accept** to complete the action.

   Upon acceptance, the status of this shared TR instance updates from **Pending acceptance** to **Accepted**.


<span id=".5q2l6aqk5Zub77ya5Yib5bu6572R57uc5a6e5L6L6L-e5o6l5bm26YWN572u6Lev55Sx77yI6LSm5Y-3Qu-8iQ=="></span>
### Step 4: Create a network instance attachment and configure routing (Account B)


1. On the TR instance list page, click the name of the created TR instance.

2. In the section below **Basic information**, select the **Intra\-region attachment** tab.

3. Click **Create attachment**, and complete the basic configuration for the network instance attachment based on the table below.

   
   |Parameter |Description |Example value (Attach vpc03) |
   |---|---|---|
   |**Basic information** |||
   |TR |Defaults to the selected TR instance, requiring no manual configuration. |tr02 |
   |Region |Defaults to the same region as the TR instance. No manual configuration required. |China (Beijing) |
   |Fee payer |Defaults to the same fee payer as the TR instance. No manual configuration required. |Network instance account |
   |Name |The name of the network instance attachment to be created. |attach\-vpc03 |
   |**Instance** |||
   |Attachment type |Select the type for the network instance attachment to be created. |VPC |
   |VPC |Select the VPC instance to be connected. |vpc03 |
   |**Attachment point configuration** |||
   |Availability Zone and Subnet |Select the entry point where TR connects to the VPC. Select the availability zone and then the subnet, and set the selected availability zone as the default availability zone. |Availability Zone A, subnet03 |
   

4. Complete the route configuration for the network instance attachment based on the table below.

   
   |Parameter |Description |Example value (Attach vpc03) |
   |---|---|---|
   |Association forwarding |The TR forwards traffic from vpc03 based on the route table (tr02\-rtb\-sys) associated with this network instance attachment.<br><br>At this point, the TR route table contains no routes and only specifies sources for traffic forwarding. To actually enable traffic forwarding, configure destinations for the TR route table via route learning or static routes. |Enabled, tr02\-rtb\-sys |
   |Route learning |The selected TR route table (tr02\-rtb\-sys) automatically learns the routes of vpc03, and generates entries with the destination as vpc03 subnets and the next hop as attach\-vpc03. |Enabled, tr02\-rtb\-sys |
   |Auto Publish Route |After enabling auto publishing, the system automatically synchronizes the routes from tr02\-rtb\-sys to all route tables within vpc03. These synchronized routes are system routes. |Enable |
   

5. Click **Buy now** to complete the action.

6. View the routes in tr02\-rtb\-sys, as shown in the table below.

   
   |Destination CIDR |Next Hop |Status |Route type |Attachment type |Instance |
   |---|---|---|---|---|---|
   |192.168.32.0/24 |attach\-vpc03 |Available |Route learning |VPC |vpc03 |
   

7. View routes in the vpc03 route table to confirm no changes.

   Since the routes in tr02\-rtb\-sys are automatically published to the vpc03 route table. This TR route table contains no routes whose Next Hop is not vpc03, so routes in the vpc03 route table are unchanged.


<span id=".5q2l6aqk5LqU77ya6YWN572u6Leo5Zyw5Z-f5bim5a6977yI6LSm5Y-3Qe-8iQ=="></span>
### Step 5: Configure inter\-region bandwidth (Account A)

<span id=".5LiA44CB5Yib5bu65bim5a695YyF"></span>
#### I. Create a bandwidth package


1. Use Account A to log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter). 

2. In the left\-side navigation pane, select **Bandwidth Package**.

3. Click **Create bandwidth package**, and configure the bandwidth package based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Billing method |The billing method for the bandwidth package to be created. Default: Subscription. |Subscription |
   |Name |Type the name for the bandwidth package to be created. |trbp01 |
   |**Bandwidth configuration** |||
   |Interoperability area |The bandwidth package requires interoperable local and peer areas. |China Mainland \- China Mainland |
   |bandwidth |Specify a bandwidth cap for the bandwidth package. Valid range: 2 to 10000. Unit: Mbps. |2Mbps |
   |Purchase time |Select the purchase duration for the bandwidth package. |1 month |
   |Automatic renewal |Specify whether to enable automatic renewal. By default, it is disabled. |Unchecked |
   |**More information** |||
   |Project |Specify the project to which the bandwidth package belongs. |default |
   

4. In the right\-side Configuration details box, follow the console guidance to review and accept the legal terms.

5. Click **Submit order** to complete the action.


<span id=".5LqM44CB5Yib5bu66Leo5Zyw5Z-f6L-e5o6l5bm26YWN572u6Lev55Sx"></span>
#### Ⅱ. Create an inter\-region attachment and configure routing


1. In the top menu bar, select the target project and region. The following example is a default project in China (Guangzhou).

2. In the left\-side navigation pane, select **Transit Router** and click the name of the target TR instance.

3. In the section below **Basic information**, select the **Inter\-region attachment** tab.

4. Click **Create inter\-region attachment** and configure basic information based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |TR |Defaults to the selected TR instance, requiring no manual configuration. |tr01 |
   |Region |Defaults to the same region as the TR instance. No manual configuration required. |China (Guangzhou) |
   |Name |The name for the inter\-region attachment to be created. |attach\-Inter\-region |
   |**Instance** |||
   |Attachment type |Inter\-region attachments only support TR instances. |TR |
   |Peer region |Regions that require connectivity across regions. |China (Beijing) |
   |Instance |Select the TR instance in the peer region based on the project. |tr02 |
   |Bandwidth Package |Specify whether to allocate bandwidth for the inter\-region attachment. If **Add to bandwidth package** is checked, select the bandwidth package based on the project and set the bandwidth. |Checked, trbp01, 2 Mbps |
   

5. Configure route information for the inter\-region attachment based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Local TR association forwarding |The TR forwards traffic from this inter\-region attachment based on the associated route table (tr01\-rtb\-sys).<br><br>Next, you need to configure the destination for this TR route table. |Enabled, tr01\-rtb\-set |
   |Peer TR association forwarding |The TR forwards traffic from this inter\-region attachment based on the associated route table (tr02\-rtb\-sys).<br><br>Next, you need to configure the destination for this TR route table. |Enabled, tr02\-rtb\-sys |
   |Local TR route learning |Enabling Local TR route learning means the specified Local TR route table will automatically learn the routes of Remote TR, and generate entries with the next hop setting as the inter\-region attachment. |Enabled, tr01\-rtb\-sys |
   |Peer TR route learning |Enabling Remote TR route learning means the specified Remote TR route table will automatically learn the routes of Local TR, and generate entries with the next hop setting as the inter\-region attachment. |Enabled, tr02\-rtb\-sys |
   

6. Click **Create** to complete the action.


<span id=".5LiJ44CB5p-l55yLVFLlkoxWUEPot6_nlLE="></span>
#### Ⅲ. View TR and VPC routes


1. View routes in TR route tables (tr01\-rtb\-sys and tr02\-rtb\-sys) in sequence, as shown in the table below.

   
   |Route table name |Destination CIDR |Next Hop |Status |Route type |Attachment type |Instance |
   |---|---|---|---|---|---|---|
   |tr01\-rtb\-sys |192.168.32.0/24 |attach\-Inter\-region |Available |Route learning |TR |tr02 |
   |tr02\-rtb\-sys |192.168.32.0/24 |attach\-vpc03 |Available |Route learning |VPC |vpc03 |
   ||192.168.0.0/24 |attach\-Inter\-region |Available |Route learning |TR |tr01 |
   ||192.168.16.0/24 |attach\-Inter\-region |Available |Route learning |TR |tr01 |
   

2. View the routes in the vpc01 and vpc02 route tables in sequence, as shown in the table below.

   
   |VPC route table |Destination CIDR |Status |Next Hop type |Next Hop |
   |---|---|---|---|---|
   |vpc01 |192.168.32.0/24 |Available |TR |tr01 |
   ||192.168.0.0/24 |Available |InnerSubnet |System default |
   ||100.64.0.0/10 |Available |System |System default |
   |vpc02 |192.168.32.0/24 |Available |TR |tr01 |
   ||192.168.16.0/24 |Available |InnerSubnet |System default |
   ||100.64.0.0/10 |Available |System |System default |
   


<span id=".5q2l6aqk5YWt77ya5p-l55yLVlBD6Lev55Sx77yI6LSm5Y-3Qu-8iQ=="></span>
### Step 6: View VPC routes (Account B)

View the routes in the vpc03 route table, as shown in the table below.


|Destination CIDR |Status |Next Hop type |Next Hop |
|---|---|---|---|
|192.168.0.0/20 |Available |TR |tr02 |
|192.168.16.0/20 |Available |Transit Router (TR) |tr02 |
|192.168.32.0/24 |Available |InnerSubnet |System default |
|100.64.0.0/10 |Available |System |System default |


<span id=".57uT5p6c6aqM6K-B"></span>
## Verification

The following verification steps take a Linux\-based ECS as an example:


1. Remotely log in to the ECS instance in vpc01. For procedure, see [Logging on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the `ping` command to connect the private IP addresses of respective ECS instances in vpc02 and vpc03, verifying network connectivity.

   * The ECS instances in vpc01 and vpc02 are mutually isolated and cannot ping each other.

   * The ECS instances in vpc01 and vpc03 can mutually communicate and ping successfully.

3. Similarly, remotely log in to the ECS instances in vpc02 and vpc03 to verify connectivity between vpc02, vpc03, and another VPC.
