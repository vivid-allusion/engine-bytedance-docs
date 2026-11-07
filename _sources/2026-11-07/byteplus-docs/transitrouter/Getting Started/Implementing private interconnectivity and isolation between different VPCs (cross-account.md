---
title: "Implementing private interconnectivity and isolation between different VPCs (cross-account, same region)"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Quick-start-04"
---

This topic describes how to use Transit Routers (TRs) to implement interconnectivity between two VPCs (vpc01 and vpc02) under Account A and another VPC (vpc03) under Account B in the same region. After connecting, both vpc01 and vpc02 can communicate with vpc03 via TR, but vpc01 and vpc02 cannot mutually communicate, as shown below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_58fc3c3c694937058ac92e2e6e169ef5.png) </span>

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created three Virtual Private Clouds (VPCs) and their subnets. For procedure, see [Building an IPv4 VPC](https://docs.byteplus.com/en/docs/vpc/Building-an-IPv4-VPC).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Ensure that neither VPC contains conflicting subnets. That is, no duplicate or overlapping CIDR blocks exist.   </div>
   

* You have created Elastic Compute Service (ECS) instances in the three VPCs. For procedure, see [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id=".6Lev55Sx6KeE5YiS"></span>
## Routing planning

A single TR instance can use the same route table to forward traffic from multiple network instances that share a common destination. Thus, in this example, the TR uses one route table for forwarding from vpc01/vpc02 to vpc03, and a separate route table for the return path from vpc03 to vpc01/vpc02. This design necessitates at least two route tables, as illustrated in the following diagram.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_456a0f1582f45dc1dd15724ca28a13e9.png) </span>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Routes in the VPC route tables illustrated above can be manually configured or automatically synchronized. This example uses auto publishing. </div>


<span id=".6YWN572u5rWB56iL"></span>
## Configuration procedures


1. [Step 1: Configure a TR instance (Account A)](https://docs.byteplus.com/docs/transitrouter/Quick-start-04#.5q2l6aqk5LiA77ya6YWN572uVFLlrp7kvovvvIjotKblj7dB77yJ): Use Account A to complete the following TR configuration.

   1. **Create a TR instance**: Create a TR instance to host the TR service.

   2. **Create a TR custom route table**: Create a custom route table to receive and forward network traffic along with the TR system route table.

   3. **Create a network instance attachment and configure routing**: Create two network instance attachments to connect the two VPCs under the same account. Configure association forwarding and route learning for those attachments.

   4. **View TR and VPC routes**: Check that the routes of the TR instance and two VPCs meet expectations.

2. [Create instance sharing (Account A)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-04?lang=zh#.5q2l6aqk5LqM77ya5Yib5bu65a6e5L6L5YWx5Lqr77yI6LSm5Y-3Qe-8iQ==): Use Account A to create a sharing unit and share the TR instance with Account B.

3. [Accept sharing invitation (Account B)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-04?lang=zh&TagIDs=2,105,104,95,94#.5q2l6aqk5LiJ77ya5o6l5Y-X5a6e5L6L5YWx5Lqr77yI6LSm5Y-3Qu-8iQ==): Use Account B to accept the TR instance shared by Account A.

4. [Create a network instance attachment and configure routing (Account B)](https://docs.byteplus.com/docs/transitrouter/Quick-start-04): Use Account B to create a network instance attachment on the shared TR instance, connecting the shared TR instance to vpc03 under this account. Configure association forwarding and route learning for it to automatically generate routes to vpc03 in the TR system route table.

5. [Configure association forwarding for the TR custom route table (Account A)](https://docs.byteplus.com/docs/transitrouter/Quick-start-04): Use Account A to configure association forwarding for the cross\-account network instance attachment, enabling traffic from vpc03 to be forwarded via the TR custom route table.

6. [Verification](https://docs.byteplus.com/docs/transitrouter/Quick-start-04#.57uT5p6c6aqM6K-B): Run `ping` to verify the connectivity between ECS instances in different VPCs to ensure that the VPCs are connected and isolated as expected.


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedures

<span id=".5q2l6aqk5LiA77ya6YWN572uVFLlrp7kvovvvIjotKblj7dB77yJ"></span>
### Step 1: Configure a TR instance (Account A)

<span id=".5LiA44CB5Yib5bu6VFLlrp7kvos="></span>
#### Ⅰ. Create a TR instance


1. Use Account A to log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. In the top menu bar, select the target project and region.

3. Click **Create TR** and configure related parameters based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Region |Select a region closer to your service for shorter network delays and faster access. Cloud resources in different regions are isolated by default on private networks. |China (Guangzhou) |
   |Name |Type in a name for the TR instance. |tr01 |
   |ASN |Specify a BGP ASN (Autonomous System Number) for the TR instance. Valid range: 64512\-65534 or 4200000000\-4294967294. Assign different ASNs for TR instances in different regions.<br><br>The TR automatically prepends its ASN to the AsPath attribute of routes published to other network instances. |64512 |
   |Multicast |Specify whether to enable multicast for the TR. [Learn more](https://docs.byteplus.com/docs/transitrouter/Multicast-Overview) |Unchecked |
   |Affiliated Project |Select the project to which the to\-be\-created TR instance belongs. |default |
   |Agreement |Follow the console guidance to review and accept Legal. |Checked |
   

4. Click **Create** to complete the action.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When you create a TR instance, the system automatically creates a system route table for it. Record the name of this system route table: rtb\-sys. The following uses rtb\-sys as an example.   </div>
   

<span id="7PiroQbt"></span>
#### Ⅱ. Create a TR custom route table


1. Click the name of the target TR instance.

2. In the section below **Basic information**, select the **Route Table** tab.

3. Click **Create Route Table** to the right of Route Table List, and type in rtb\-set as the route table name.

4. Click **Create** to complete the action.


<span id=".5LiJ44CB5Yib5bu6572R57uc5a6e5L6L6L-e5o6l5bm26YWN572uVFLot6_nlLE="></span>
#### Ⅲ. Create a network instance attachment and configure routing

Create two network instance attachments using the following steps. These will connect the TR instance to vpc01 and vpc02 under Account A separately.The configurations for these attachments are specified in the configuration table's Example value (Attach vpc01) and Example value (Attach vpc02) columns.


1. In the section below **Basic information**, select the **Intra\-region attachment** tab.

2. Click **Create attachment**, and complete the basic configuration for the network instance attachment based on the table below.

   
   |Parameter |Description |Example value (Attach vpc01) |Example value (Attach vpc02) |
   |---|---|---|---|
   |**Basic information** ||||
   |TR |Defaults to the selected TR instance, requiring no manual configuration. |tr01 |tr01 |
   |Region |Default to the same region as the TR instance. No manual configuration required. |China (Guangzhou) |China (Guangzhou) |
   |Name |The name of the network instance attachment to be created. |attach\-vpc01 |attach\-vpc02 |
   |**Instance** ||||
   |Attachment type |Select the type for the network instance attachment to be created. |VPC |VPC |
   |VPC |Select the VPC instance to be connected. |vpc01 |vpc02 |
   |**Attachment point configuration** ||||
   |Availability Zone and Subnet |Select the entry point where TR connects to the VPC. Select the availability zone and then the subnet, and set the selected availability zone as the default availability zone. |China (Guangzhou) A, subnet01 |Availability zone A, subnet02 |
   

3. Complete the route configuration for the network instance attachment based on the table below.

   
   |Parameter |Description |Example value (Attach vpc01) |Example value (Attach vpc02) |
   |---|---|---|---|
   |Association forwarding |The TR will forward traffic from the related network instance based on the route table associated with this network instance attachment.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Take attach\-vpc01 as an example. After enabling association forwarding, the TR forwards traffic from vpc01 based on rtb\-sys.</div><br><br><br> |Enabled, rtb\-sys |Enabled, rtb\-sys |
   |Route learning |After enabling route learning, the TR route table will automatically learn routes of the network instance, and generate entries with the destination as VPC subnets and the next hop as this network instance attachment.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Take attach\-vpc01 as an example. After enabling route learning, the TR route table (rtb\-set) automatically generates routes whose destinations are vpc01 subnets and the next hop is attach\-vpc01.</div><br><br><br> |Enabled, rtb\-set |Enabled, rtb\-set |
   |Auto Publish Route |Enabling auto publishing will automatically synchronize routes from the associated TR route table to all route tables within the selected VPC. These synchronized routes are marked as VPC system routes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Take attach\-vpc01 as an example. After enabling auto publishing, the system automatically synchronizes the routes from rtb\-sys to all route tables within vpc01. These synchronized routes are system routes.</div><br><br><br> |Enabled |Enabled |
   

4. Click **Buy now** to complete the action.


<span id=".5Zub44CB5p-l55yLVFLlkoxWUEPot6_nlLE="></span>
#### Ⅳ. View TR and VPC routes


1. View routes of TR route tables (rtb\-sys and rtb\-set) in sequence.

   * Currently, no routes exist in rtb\-sys.

   * The routes in rtb\-set are listed in the following table.

      
      |Destination CIDR |Next Hop |Status |Route type |Attachment type |Instance |
      |---|---|---|---|---|---|
      |192.168.0.0/24 |attach\-vpc01 |Available |Automatic learning |VPC |vpc01 |
      |192.168.16.0/24 |attach\-vpc02 |Available |Automatic learning |VPC |vpc02 |
      

2. View routes of the vpc01 and vpc02 route tables in sequence to confirm no changes.

   Since the routes in rtb\-sys are automatically published to the vpc01 and vpc02 route tables, routes in the vpc01 and vpc02 route tables are unchanged.


<span id=".5q2l6aqk5LqM77ya5Yib5bu65a6e5L6L5YWx5Lqr77yI6LSm5Y-3Qe-8iQ=="></span>
### Step 2: Create instance sharing (Account A)


1. Click the account avatar in the upper right corner.

2. Select **Tools \> Resource**.

3. In the left\-side navigation pane, select **Resource sharing \> Shared by me**.

4. In the top menu bar, select your target region.

5. On the **Shared unit** tab, click **Create shared unit** and configure the parameters based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Unit name |Type a name for the shared unit that is easy to identify. |Share TR |
   |Region |Region defaults to the region selected in the top menu bar. To modify, reselect the region in the top menu bar. |China (Guangzhou) |
   |product |Select the Transit Router \- TR instance. |Transit Router \- TR instance. |
   |Resource ID |Type in the ID of the TR to be shared, then search and check it. |Select the Transit Router (tr01) |
   

6. Click **Next** to associate sharing permissions.

   TR sharing permissions are system\-defined and cannot be modified. For default supported actions, see [Instructions](https://docs.byteplus.com/docs/transitrouter/Cross-account-Sharing-overview#T39M302D).

7. Click **Next** to associate shared users.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Resource user |Choose a method for resource sharing.<br><br><br>* **Allow sharing with any account**: Share the TR with any BytePlus root account.<br><br>* **Only allow sharing with enterprises and organizations**: Share the TR only with BytePlus root accounts in the same enterprise organization. |Allow sharing with any account |
   |User type |Select the root account. |main account |
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


1. On the TR instance list page, click the name of the shared TR instance.

2. In the section below **Basic information**, select the **Intra\-region attachment** tab.

3. Click **Create attachment**, and complete the basic configuration based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |TR |Defaults to the selected TR instance, requiring no manual configuration. |tr01 |
   |Region |Defaults to the same region as the TR instance. No manual configuration required. |China (Guangzhou) |
   |Fee payer |Defaults to the same fee payer as the TR instance. No manual configuration required. |Network instance account |
   |Name |The name for the network instance attachment to be created. |attach\-vpc03 |
   |**Instance** |||
   |Attachment type |Select the type for the network instance attachment to be created. |VPC |
   |VPC |Select the VPC instance to be connected. |vpc03 |
   |**Attachment point configuration** |||
   |Availability Zone and Subnet |Select the entry point where TR connects to the VPC. Select the availability zone and then the subnet, and set the selected availability zone as the default availability zone. |Availability zone A, subnet03 |
   

4. Complete the route configuration based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Association forwarding |If association forwarding is enabled, the TR forwards traffic from the network instance based on its system route table by default. You cannot specify other TR route tables.<br><br>In this example, traffic from vpc03 is forwarded based on the TR custom route table (rtb\-set), so the association forwarding is disabled. Next, you need to use Account A to configure association forwarding for this network instance attachment in the TR custom route table (rtb\-set). |Disabled |
   |Route learning |After you enable route learning, the TR system route table (rtb\-sys) automatically learns the routes of vpc03 and generates entries with the destination as vpc03 subnets and the next hop as attach\-vpc03. |Enabled, rtb\-sys |
   |Auto Publish Route |When you enable auto publishing, the system automatically synchronizes routes from the associated TR route table to all route tables within vpc03. These synchronized routes are marked as VPC system routes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">In this example, no routes are propagated to the vpc03 route table because the association forwarding is not enabled. Once you use Account A to configure a TR route table for attach\-vpc03 for association forwarding, the routes in this TR route table will be automatically propagated to the vpc03 route table.</div><br><br><br> |Enabled |
   

5. Click **Buy now** to complete the action.

6. View routes of TR route tables (rtb\-sys and rtb\-set) in sequence.

   * The routes in rtb\-set remain unchanged.

   * The routes in rtb\-set are listed in the following table.

      
      |Destination CIDR |Next Hop |Status |Route type |Attachment type |Instance |
      |---|---|---|---|---|---|
      |192.168.32.0/24 |attach\-vpc03 |Available |Automatic learning |VPC |vpc03 |
      

7. View routes in the vpc01, vpc02 and vpc03 route tables in sequence, as shown in the table below.

   * Since the network instance attachment does not enable association forwarding, no routes exist in the vpc03 route table.

   * Because vpc01 and vpc02 route tables automatically learn routes from rtb\-sys, the routes in vpc01 and vpc02 route tables are shown in the table below.

      
      |VPC route table |Destination CIDR |Status |Next Hop type |Next Hop |
      |---|---|---|---|---|
      |vpc01 |192.168.32.0/24 |Available |TR |tr01 |
      ||192.168.0.0/24 |Available |InnerSubnet |System default |
      ||100.64.0.0/10 |Available |System |System default |
      ||192.168.32.0/24 |Available |TR |tr01 |
      ||192.168.16.0/24 |Available |InnerSubnet |System default |
      ||100.64.0.0/10 |Available |System |System default |
      


<span id=".5q2l6aqk5LqU77ya5Li6VFLoh6rlrprkuYnot6_nlLHooajphY3nva7lhbPogZTovazlj5HvvIjotKblj7dB77yJ"></span>
### Step 5: Configure association forwarding for the TR custom route table (Account A)


1. Use Account A to log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the section below **Basic information**, select the **Route Table** tab.

4. Click the name of the TR custom route table (rtb\-set) and select the **Association forwarding** tab.

5. Click **Create association forwarding** and select the network instance attachment (vpc03).

6. Click **Create** to complete the action.

7. View routes of TR route tables (rtb\-sys and rtb\-set) in sequence to confirm no changes.

8. View the route entries of vpc03, as shown in the table below.

   
   |Destination CIDR |Status |Next Hop type |Next Hop |
   |---|---|---|---|
   |192.168.0.0/24 |Available |TR |tr01 |
   |192.168.16.0/24 |Available |TR |tr01 |
   |192.168.32.0/24 |Available |InnerSubnet |System default |
   |100.64.0.0/10 |Available |System |System default |
   


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation

The following verification steps take a Linux\-based ECS as an example:


1. Remotely log in to the ECS instance in vpc01. For procedure, see [Logging on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the `ping` command to connect the private IP addresses of respective ECS instances in vpc02 and vpc03, verifying network connectivity.

   * The ECS instances in vpc01 and vpc02 are mutually isolated and cannot ping each other.

   * The ECS instances in vpc01 and vpc03 can mutually communicate and can ping successfully.

3. Similarly, remotely log in to the ECS instances in vpc02 and vpc03 to verify connectivity between vpc02, vpc03, and another VPC.
